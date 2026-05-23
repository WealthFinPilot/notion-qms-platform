# Sous-système Formation et Onboarding RH

## Problème adressé

Dans un laboratoire accrédité, la compétence du personnel est une exigence tracée (ISO/IEC 17025 §6.2). Trois douleurs concrètes motivent ce sous-système :

- **Onboarding non reproductible** — chaque arrivée repart d'une liste informelle, dépendante de la mémoire d'une personne-clé.
- **Compétences non tracées** — pas de preuve consolidée de qui a suivi quoi, ni à quel niveau.
- **Certificats expirés non détectés** — les qualifications individuelles (par exemple une carte d'inspection) périment sans alerte.

La réponse : un parcours **standardisé par type de poste**, automatisé de l'inscription à l'approbation, avec preuve de qualification datée.

## Architecture du sous-système

Quatre bases, reliées en cascade, portent le sous-système (toutes dans Back End ▸ Gestion RH ▸ Formations) :

| Base | Rôle | Relations clés |
|---|---|---|
| **Nos Formations** | Catalogue / parcours (la racine) | ↔ Modules-Formations, ↔ Inscriptions (Répondant) |
| **Modules-Formations** | Briques pédagogiques rattachées à un *Type de poste* — la « trousse » | → Type de poste, → Master Documentations, ↔ Nos Formations, ← Instances |
| **Instances de formations** | Sessions programmées (date, lieu, participants) | → Modules-Formations, ↔ Inscriptions |
| **Inscriptions aux formations** | Inscription individuelle (par personne) — l'unité de suivi | → Nos Formations, → Instances, → Master Documentations |

La logique « trousse par type de poste » se lit ainsi : un *Module-Formation* est marqué `Obligatoire`, porte un `Ordre de passage` et un délai `Jours après embauche`, et pointe vers un `Type de poste`. À l'embauche, le système sélectionne les modules obligatoires du poste du nouvel arrivant et calcule les échéances — l'onboarding devient une conséquence déterministe du type de poste, pas une liste manuelle.

> Convention technique notable : *Instances de formations* expose des compteurs préfixés `n8n__` (`n8n__Créées`, `n8n__Ignorées`, `n8n__Inscriptions générées`, `n8n__Dernière exécution`). C'est la trace d'exécution du webhook d'inscription, directement lisible dans la base — utile pour auditer un run sans ouvrir n8n.

## Flux d'onboarding automatisé

Déclencheur : bouton **⚡ Inscription d'entrée** sur *Master Employés* (webhook WF 12).

1. Lecture du *Type de poste* du nouvel employé.
2. Sélection des *Modules-Formations* marqués `Obligatoire` pour ce poste.
3. Calcul des échéances via `Jours après embauche`.
4. Création des *Inscriptions* correspondantes, par personne.

Résultat : un parcours d'intégration identique d'un employé à l'autre pour un même poste, échéancé automatiquement.

## Flux formation continue

Déclencheur : bouton **⚡+ Programmer** sur *Modules-Formations*, ou planification automatique via **WF 14** (quotidien, 01h00, pour les modules à périodicité `Tout les ? (jours)`).

1. Création d'une *Instance de formation* (date début / fin, format, lieu, plateforme, formateur, documents joints).
2. **⚡ Inscrire les participants** (sur *Instances*) génère en masse les *Inscriptions* ; le résultat du run est tracé via les compteurs `n8n__*`.
3. **⚡ Créer une tâche** (sur *Inscriptions*, webhook WF 16) pousse la formation en tâche RACI dans *Master Tâches* pour suivi opérationnel.
4. L'employé suit la formation puis **⚡ Terminer ma formation** : `État` passe à *Terminé*, `Date complété` et `Date d'obtention` sont renseignées, `Verification` est activée, et la `Date de péremption` est posée si un certificat est attendu.
5. **Approbation** : bouton réservé à l'Approbateur RH pour valider la complétion.

Les formations individuelles hors catalogue (certifications personnelles, cartes spécialisées) entrent par le formulaire **Ajouter une formation personnelle** sur *Inscriptions* (champ `Formation indv`).

## Workflows WF 12 à 16 — automatisations dédiées

| WF | Rôle dans le cycle | Déclencheur (JSON) |
|---|---|---|
| WF 12 | Onboarding : génère les inscriptions obligatoires par type de poste | Webhook (bouton *Inscription d'entrée*) |
| WF 13 | Maintient la cohérence instances ↔ inscriptions sur commande | Webhook |
| WF 14 | Programme périodiquement les instances des modules récurrents | **Planifié, quotidien 01h00** |
| WF 15 | Inscription individuelle hors session de masse | Webhook |
| WF 16 | Crée la tâche RACI de formation dans Master Tâches | Webhook (bouton *Créer une tâche*) |

Détail technique et bases impactées : [docs/02-workflows-n8n.md](02-workflows-n8n.md). À noter : WF 14 est **planifié** et non événementiel — c'est l'équivalent d'un scan appliqué à la formation continue.

## Boutons Notion et webhooks

| Bouton | Base | WF associé | Action | Cible |
|---|---|---|---|---|
| ⚡ Inscription d'entrée | Master Employés | WF 12 | Onboarding par type de poste | Inscriptions |
| ⚡+ Programmer | Modules-Formations | (création directe) / WF 14 | Crée une instance | Instances |
| ⚡ Inscrire les participants | Instances | WF 12 / 13 | Génère les inscriptions en masse | Inscriptions |
| ⚡ Créer une tâche | Inscriptions | WF 16 | Pousse en tâche RACI | Master Tâches |
| ⚡ Terminer ma formation | Inscriptions | — | Clôture, date complété, péremption | Inscriptions |
| Approbation | Inscriptions | — | Validation finale RH | Inscriptions |

## Dashboard RH

Les bases *Nos Formations* et *Instances* exposent des indicateurs dérivés par formule / rollup : **En cours**, **Progression**, **Objectif** et **Prix Total $** (somme via `Répondant → Inscriptions → Total $`). Pour l'approbateur, ils donnent une lecture immédiate de l'avancement par formation et par session.

Limite reconnue : plusieurs de ces indicateurs reposent sur des formules dont la chaîne de dépendances est longue (jusqu'à 5 rollups / formules en cascade) ; une évolution du schéma demande de vérifier la cohérence de toute la chaîne. La synthèse recommande aussi d'ajouter un workflow planifié de relance **avant** la `Date de péremption` des certificats individuels — équivalent fonctionnel du WF 02 appliqué au personnel — actuellement absent.

## Lien ISO/IEC 17025 §6.2

Le sous-système contribue aux exigences de personnel :

- **§6.2.2** — exigences de compétence documentées (trousse par type de poste).
- **§6.2.3** — compétence effective (suivi d'exécution et complétion).
- **§6.2.5 a-f** — procédures et enregistrements (inscriptions, certificats, dates).
- **§6.2.6** — autorisations spécifiques (certificats avec date de péremption).

Posture : contribution à la traçabilité des compétences, sans garantie de conformité globale.

> Note de cohérence normative : la clause Personnel est numérotée **§6.2** dans l'édition 2017 (le renvoi §5.2 de certaines sources correspond à l'édition antérieure).

## Diagramme

[diagrams/hr-onboarding-cycle.mmd](../diagrams/hr-onboarding-cycle.mmd).

## Captures

Catégorie `rh-formation` du [MANIFEST](../screenshots/MANIFEST.md) — **toutes marquées `[ANONYMIZE]`** (noms d'employés, suivis individuels) :

- `rh-formation_rh.png` — page d'accueil du hub RH.
- `rh-formation_exemple-d-espace-de-formation.png` — espace de formation personnel (vidéo + bouton de validation).
- `rh-formation_espace-personnel-de-suivis-des.png` — suivi personnel des inscriptions.
- `rh-formation_programmation-des-instances-de-formation.png` — programmation des instances (bouton d'automatisation des inscriptions).
- `rh-formation_suivis-global-des-formations.png` — suivi global avec barres de progression.
- `rh-formation_gestion-des-modules-de-formations.png` — gestion des modules (la trousse par poste).
