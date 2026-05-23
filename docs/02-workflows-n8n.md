# Workflows n8n

> Source prioritaire de ce document : les fichiers JSON exportés des workflows (`Source/Notion synthèse/Workflows/`). Lorsque le JSON contredit la synthèse, le JSON fait foi et la divergence est signalée.

## Philosophie d'automatisation

Le système combine deux régimes d'automatisation complémentaires :

- **Scans planifiés (batch)** — un `Schedule Trigger` lit périodiquement une base source (équipements, certificats, tâches récurrentes, calendrier qualité), compare les échéances et **produit des tâches** dans *Master Tâches*. C'est le régime « pousse les échéances vers l'action ».
- **Webhooks événementiels (temps réel)** — un bouton Notion ou un changement d'état appelle un webhook n8n qui **réagit** : génération de PO, mise à jour de statut, versionnage documentaire, inscription de formation. C'est le régime « réagit au clic utilisateur ».

Ce choix *batch + temps réel* est ce qui permet au système de couvrir à la fois les obligations récurrentes (qu'on oublie) et les actions ponctuelles (qu'on déclenche). Tous les scans planifiés délèguent la création de tâche à un **sous-workflow** dédié (`WF 0x.0y`) et journalisent leur exécution via un sous-workflow commun *Logger - Send to Notion*, qui écrit dans la base *Archives - n8n Logs* (run ID, durée, actions OK/échec).

Trois observations factuelles tirées de l'export :

1. **Identité technique partagée.** Tous les workflows s'authentifient à Notion via une seule credential nommée `Notion API` (les sous-workflows d'archivage WF 05.0x ajoutent une credential `Notion Header` pour les appels HTTP directs à l'API Notion). Aucun secret en clair n'apparaît dans les nœuds extraits.
2. **API Notion en direct.** Au-delà du nœud `Notion` natif, les workflows appellent fréquemment l'API REST Notion en `httpRequest` (`/v1/pages/...`, `/v1/blocks/...`) — typiquement pour manipuler le contenu de page (blocs) que le nœud natif ne couvre pas.
3. **État de l'export.** Les scans planifiés (WF 01-05 et WF 08) sont `active: false` dans l'export, tandis que les workflows événementiels et de formation (WF 06, 07, 09-16) sont `active: true`. C'est l'état du fichier fourni, pas nécessairement l'état de production.

## Vue d'ensemble

| # | Nom (JSON) | Groupe | Déclencheur | Bases impactées (extraites du JSON) |
|---|---|---|---|---|
| 01 | WorkFlow 01 — Scan parc équipements | Scan planifié | Planifié, mensuel 04h00 | Master Equipements, Types de tâche, Départements, Master Tâches |
| 01.01 | Création tâche complexe Maintenance / Déviation (RACI) | Sous-workflow | Appelé par WF 01 | Master Tâches |
| 01.02 | Création tâche complexe Calibration (RACI) | Sous-workflow | Appelé par WF 01 | Master Tâches |
| 02 | WorkFlow 02 — Scan certificats fournisseurs | Scan planifié | Planifié, mensuel 04h00 | Certificats Fournisseurs, Master Fournisseurs |
| 02.01 | Création tâche vérification certificats | Sous-workflow | Appelé par WF 02 | Master Tâches |
| 03 | WorkFlow 03 — Scan tâches récurrentes | Scan planifié | Planifié, mensuel 04h00 | Tâches Récurrentes, Types de tâche, Départements, Master Tâches |
| 03.01 | Créer une tâche récurrente | Sous-workflow | Appelé par WF 03 | Master Tâches |
| 04 | WorkFlow 04 — Scan calendrier qualité | Scan planifié | Planifié, mensuel 04h00 | Calendrier Qualité, Types de tâche |
| 04.01 | Création tâche liée à un évènement qualité | Sous-workflow | Appelé par WF 04 | Master Tâches |
| 05 | WorkFlow 05 — Archivage Master Tâches | Scan planifié | Planifié, mensuel 04h00 | Master Tâches, Certificats, Types de tâche, Départements |
| 05.01 | Archive tâche Qualité | Sous-workflow | Appelé par WF 05 | Archives Qualité |
| 05.02 | Archive tâche Certificat | Sous-workflow | Appelé par WF 05 | Archives Contrôle Certificats |
| 05.03 | Archive tâche Équipement | Sous-workflow | Appelé par WF 05 | Archives Contrôles des Équipements |
| 05.04 | Archive tâche custom (diverses) | Sous-workflow | Appelé par WF 05 | Archives des Tâches |
| 06 | WorkFlow 06 — MAJ échéanciers | Webhook événementiel | Webhook POST (chemin nommé `wf06/validate`) | Master Tâches, objets sources (équipement / certificat / qualité), Archives - n8n Logs |
| 07 | WorkFlow 07 — Génération PO sur demande | Webhook événementiel | Webhook POST (bouton Check out) | Demandes d'achat, Bons de Commande, Master Fournisseurs, Départements |
| 08 | WorkFlow 08 — Génération PO planifiés | Scan planifié | Planifié (intervalle par défaut, non spécifié dans le JSON) | Demandes d'achat, Bons de Commande, Master Fournisseurs, Départements |
| 09 | WorkFlow 09 — Suivi PO | Webhook événementiel | Webhook POST | Demandes d'achat, Magasin |
| 10 | WorkFlow 10 — Update statut Magasin | Webhook événementiel | Webhook POST | Magasin |
| 11 | WorkFlow 11 — MAJ documentation | Webhook événementiel | Webhook POST (bouton Nouvelle Version) | Master Documentations Entreprise |
| 12 | WorkFlow 12 — Onboarding par type de poste | Formation / Onboarding | Webhook POST (2 webhooks) | Master Employés, Nos Formations, Modules-Formations, Instances, Inscriptions, Documentations |
| 13 | WorkFlow 13 — MAJ formations sur commande | Formation / Onboarding | Webhook POST | Instances, Inscriptions |
| 14 | WorkFlow 14 — Programmation des modules | Formation / Onboarding | Planifié, quotidien 01h00 | Modules-Formations |
| 15 | WorkFlow 15 — Inscription individuelle | Formation / Onboarding | Webhook POST | Nos Formations, Modules-Formations, Inscriptions, Type de poste, Documentations |
| 16 | WorkFlow 16 — Tâche de formation (RACI) | Formation / Onboarding | Webhook POST | Master Tâches, Inscriptions, Master Employés, Départements |

> **Divergences signalées.**
> - La synthèse présente WF 01-05 comme un « batch nocturne ». La fréquence réellement configurée dans les JSON est **mensuelle à 04h00** (`field: months`). C'est la valeur du JSON qui est retenue ici.
> - WF 08 et WF 14 portent un `Schedule Trigger` : ce sont des **workflows planifiés**, même s'ils servent respectivement le cycle achats (groupe événementiel) et le sous-système formation. Classés selon leur déclencheur réel.

## Scans planifiés (WF 01 à 05)

### WF 01 — Scan parc équipements
- **Déclencheur :** planifié, mensuel à 04h00.
- **Objectif :** déclencher les tâches de maintenance, étalonnage et contrôle de déviation selon les échéances métrologiques de *Master Equipements*.
- **Flux :** `Schedule Trigger` → lecture (`getAll`) de *Master Equipements* → `If` / `Switch` sur les marqueurs de demande (`Étalonnage Request`, `Maintenance Request`, `Déviation request`) → `Loop` → appel des sous-workflows WF 01.01 (maintenance / déviation) et WF 01.02 (calibration) → *Logger*.
- **Bases impliquées :** Master Equipements (source), Master Tâches (cible via sous-workflows), Types de tâche, Départements.
- **Valeur opérationnelle :** supprime les oublis métrologiques, point critique ISO 17025.
- **Sous-workflows :** WF 01.01 (60 nœuds — création de tâche RACI complexe avec contenu de page riche via API blocs), WF 01.02 (27 nœuds — calibration).

### WF 02 — Scan certificats fournisseurs
- **Déclencheur :** planifié, mensuel à 04h00.
- **Objectif :** surveiller les dates d'expiration des certificats fournisseurs et déclencher leur renouvellement.
- **Flux :** `Schedule Trigger` → lecture de *Certificats Fournisseurs* et *Master Fournisseurs* → `If` sur l'échéance → `Loop` → sous-workflow WF 02.01 → *Logger*.
- **Bases impliquées :** Certificats Fournisseurs, Master Fournisseurs (sources) ; Master Tâches (cible).
- **Valeur opérationnelle :** preuve continue de la chaîne qualité matériaux.
- **Sous-workflows :** WF 02.01 (22 nœuds — création de la tâche de vérification).

### WF 03 — Scan tâches récurrentes
- **Déclencheur :** planifié, mensuel à 04h00.
- **Objectif :** générer périodiquement les tâches récurrentes (5S, revues, audits internes) définies dans *Tâches Récurrentes*.
- **Flux :** `Schedule Trigger` → lecture de *Tâches Récurrentes* → calcul de la prochaine occurrence (`Répéter tous les # jours`) → sous-workflow WF 03.01 → *Logger*.
- **Bases impliquées :** Tâches Récurrentes (source), Types de tâche, Départements, Master Tâches (cible).
- **Valeur opérationnelle :** industrialise les rituels qualité.
- **Sous-workflows :** WF 03.01 (17 nœuds).

### WF 04 — Scan calendrier qualité
- **Déclencheur :** planifié, mensuel à 04h00.
- **Objectif :** matérialiser les jalons du *Calendrier Qualité* (audits, revue de direction, inter-labs) en tâches actionnables.
- **Flux :** `Schedule Trigger` → lecture de *Calendrier Qualité* (filtre `Request n8n` / `Fréquence (Jours)`) → sous-workflow WF 04.01 → *Logger*.
- **Bases impliquées :** Calendrier Qualité (source), Types de tâche, Master Tâches (cible).
- **Valeur opérationnelle :** alignement direct entre stratégie qualité et exécution.
- **Sous-workflows :** WF 04.01 (16 nœuds).

### WF 05 — Archivage Master Tâches
- **Déclencheur :** planifié, mensuel à 04h00.
- **Objectif :** décharger *Master Tâches* en déplaçant les tâches clôturées vers des archives thématiques (conservation 5 ans).
- **Flux :** `Schedule Trigger` → lecture des tâches archivables → `Switch` par catégorie → routage vers l'un des 4 sous-workflows → *Logger*. Les sous-workflows lisent le contenu de page (`block:getAll`), recréent l'entrée d'archive puis archivent la page source (opération `archive` via API).
- **Bases impliquées :** Master Tâches (source) ; Archives Qualité / Contrôle Certificats / Contrôles Équipements / des Tâches (cibles) ; Archives - n8n Logs.
- **Valeur opérationnelle :** maintient la performance de la table centrale tout en conservant l'historique — c'est l'allègement structurel central de l'architecture.
- **Sous-workflows :** WF 05.01 Qualité, 05.02 Certificats, 05.03 Équipements, 05.04 Diverses (26 nœuds chacun).

## Webhooks événementiels (WF 06 à 11)

### WF 06 — Mise à jour des échéanciers
- **Déclencheur :** webhook POST, chemin nommé `wf06/validate` (anonymisé `{{WEBHOOK_PATH_WF06_NAMED}}`), déclenché à la clôture d'une tâche dans *Master Tâches*.
- **Objectif :** recalculer la prochaine échéance sur l'objet source (équipement, certificat, jalon qualité) une fois la tâche close, pour relancer le cycle de planification.
- **Flux :** `Webhook` → lecture et tri des données de *Master Tâches* → `Switch` par catégorie de tâche (`nom_tache` : Qualité, Maintenance, Déviation, Calibration, Certificat) → recalcul et mise à jour de l'échéance sur la page de l'objet source via les nœuds Notion → mise à jour du statut de la tâche → *Logger*.
- **Bases impliquées :** Master Tâches (source, lue puis mise à jour) ; objets sources par catégorie — Master Equipements (étalonnage / maintenance / déviation), Certificats Fournisseurs, Calendrier Qualité ; Archives - n8n Logs.
- **Volumétrie :** 38 nœuds dont 12 nœuds Notion.
- **Valeur opérationnelle :** ferme la boucle planification ↔ exécution sans intervention manuelle — l'objet qui a généré la tâche (via WF 01/02/04) voit son échéancier réarmé dès la clôture (cf. cycle de vie d'une tâche, [docs/03](03-processus-cles.md)).

### WF 07 — Génération PO sur demande
- **Déclencheur :** webhook POST, déclenché par le bouton *Check out* depuis *Demandes d'achat* / *Mon Panier*.
- **Objectif :** transformer une ou plusieurs demandes d'achat validées en bon de commande (PO), regroupées par fournisseur.
- **Flux :** `Webhook` → lecture des DA et du fournisseur → branches `If` (item déjà traité, quantité, etc.) → création / mise à jour du PO et des statuts via nœud Notion et API REST. Présence de `Sticky Note` documentant le flux dans le canvas.
- **Bases impliquées :** Demandes d'achat, Bons de Commande (PO), Master Fournisseurs, Départements.
- **Valeur opérationnelle :** conversion DA vers PO en un clic, traçable.

### WF 08 — Génération PO planifiés
- **Déclencheur :** planifié (intervalle par défaut, non spécifié dans le JSON).
- **Objectif :** créer automatiquement les PO récurrents (consommables, services planifiés).
- **Flux :** `Schedule Trigger` → lecture des DA récurrentes → regroupement par fournisseur → création des PO → *Logger*.
- **Bases impliquées :** Demandes d'achat, Bons de Commande, Master Fournisseurs, Départements.
- **Valeur opérationnelle :** évite les ruptures de stock prévisibles. Même cible que WF 07, mais en mode batch.

### WF 09 — Suivi PO
- **Déclencheur :** webhook POST.
- **Objectif :** mettre à jour le statut du PO (envoyé, confirmé, livré) et propager l'information vers les DA et le Magasin.
- **Flux :** `Webhook` → lecture du PO → branches `If` selon le statut → mises à jour multiples (`databasePage:update` × 6) sur *Demandes d'achat* et *Magasin*.
- **Bases impliquées :** Demandes d'achat, Magasin.
- **Valeur opérationnelle :** visibilité fournisseur en temps quasi réel.

### WF 10 — Update statut Magasin
- **Déclencheur :** webhook POST.
- **Objectif :** ajuster les statuts du Magasin à la réception ou à la sortie d'un consommable.
- **Flux :** workflow court (8 nœuds) : `Webhook` → `Code` → 2 mises à jour Notion sur *Magasin*.
- **Bases impliquées :** Magasin.
- **Valeur opérationnelle :** Magasin toujours cohérent avec les flux réels.

### WF 11 — Mise à jour documentation
- **Déclencheur :** webhook POST, déclenché par le bouton *Nouvelle Version* sur *Master Documentations Entreprise*.
- **Objectif :** versionner un document qualité et archiver automatiquement la version précédente.
- **Flux :** `Webhook` → lecture du document → création de l'entrée d'archive → archivage de la version précédente (opération `archive`) → mise à jour de la version courante.
- **Bases impliquées :** Master Documentations Entreprise (et *Archive Documentations Entreprise* en cible d'archivage).
- **Valeur opérationnelle :** conformité documentaire ISO 17025 (versionnage tracé).

## Formation et Onboarding (WF 12 à 16)

Ces cinq workflows pilotent le sous-système Formation du hub RH (détaillé dans [docs/05-formation-rh.md](05-formation-rh.md) et illustré par [diagrams/hr-onboarding-cycle.mmd](../diagrams/hr-onboarding-cycle.mmd)). Ils s'articulent autour des quatre bases du sous-système — *Nos Formations*, *Modules-Formations*, *Instances de formations*, *Inscriptions aux formations* — et sont majoritairement déclenchés par des boutons Notion (`⚡`) câblés sur des webhooks. Exception notable : **WF 14 est planifié** (programmation périodique des modules), pas événementiel.

### WF 12 — Onboarding par type de poste
- **Déclencheur :** webhook POST (deux nœuds webhook : bouton + création d'instance).
- **Objectif :** à l'embauche (bouton *⚡ Inscription d'entrée* sur *Master Employés*), générer les inscriptions aux modules obligatoires du *Type de poste*, avec calcul d'échéance via *Jours après embauche*.
- **Bases impliquées :** Master Employés, Nos Formations, Modules-Formations, Instances, Inscriptions, Master Documentations. C'est le workflow le plus connecté du groupe (35 nœuds, 11 opérations Notion).
- **Valeur opérationnelle :** onboarding reproductible par type de poste.

### WF 13 — MAJ des formations sur commande
- **Déclencheur :** webhook POST.
- **Objectif :** mettre à jour instances et inscriptions sur demande (recalcul d'état, synchronisation).
- **Bases impliquées :** Instances de formations, Inscriptions aux formations.
- **Valeur opérationnelle :** maintient la cohérence du suivi sans intervention manuelle.

### WF 14 — Programmation des modules
- **Déclencheur :** planifié, quotidien à 01h00.
- **Objectif :** programmer périodiquement les instances des modules de formation continue (champ `Tout les ? (jours)` de *Modules-Formations*).
- **Bases impliquées :** Modules-Formations.
- **Valeur opérationnelle :** automatise la récurrence des formations sans planification manuelle. **Équivalent fonctionnel d'un scan planifié appliqué à la formation continue.**

### WF 15 — Inscription individuelle
- **Déclencheur :** webhook POST.
- **Objectif :** inscrire un individu à une formation hors session de masse (catalogue → inscription unique).
- **Bases impliquées :** Nos Formations, Modules-Formations, Inscriptions, Type de poste, Master Documentations.
- **Valeur opérationnelle :** couvre les formations individuelles et hors catalogue.

### WF 16 — Tâche de formation (RACI)
- **Déclencheur :** webhook POST (bouton *⚡ Créer une tâche* sur *Inscriptions*).
- **Objectif :** pousser une inscription de formation en tâche RACI dans *Master Tâches* pour suivi opérationnel par l'employé.
- **Bases impliquées :** Inscriptions, Master Employés, Départements, Master Tâches.
- **Valeur opérationnelle :** raccroche la formation au cycle de vie de tâche commun — la formation devient une action traçable comme les autres.

## Captures

Captures de workflows n8n disponibles (catégorie `workflow-n8n` du [MANIFEST](../screenshots/MANIFEST.md)) : une par workflow et par sous-workflow, par exemple `workflow-n8n_wf01-scan-equipement.png`, `workflow-n8n_wf05-archive-taches.png`, `workflow-n8n_wf07-regroupement-achat-en-po-sur.png`, `workflow-n8n_wf12-inscriptions-des-employes-automatiques-par.png`, plus `workflow-n8n_logger-create-debugging-report.png` pour le sous-workflow de journalisation.

> Avant publication : les captures de canvas n8n peuvent exposer des identifiants de base de données ou des chemins de webhook. Voir `ANONYMIZE-TODO.md`.
