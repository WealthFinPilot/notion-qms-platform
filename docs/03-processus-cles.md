# Processus clés

Six processus structurent l'exploitation quotidienne du système. Tous convergent, directement ou indirectement, vers *Master Tâches* et vers les bases d'archives — c'est la conséquence concrète du choix de table de faits centrale décrit dans [docs/01](01-architecture-back-end.md).

## P1 — Cycle de vie d'une tâche

Diagramme : [diagrams/task-lifecycle.mmd](../diagrams/task-lifecycle.mmd).

Le processus pivot : il industrialise l'exécution RACI de toute action de l'entreprise, quelle que soit son origine.

1. **Planification** — une échéance arrive sur un objet source (équipement, certificat, jalon qualité, tâche récurrente).
2. **Création** — un scan n8n (WF 01-04) ou un formulaire crée une tâche dans *Master Tâches* avec son RACI complet. Le marqueur `Anti-Spam` empêche la double génération.
3. **Exécution** — le Responsable et l'Équipe traitent la tâche ; statut piloté par la propriété `État`.
4. **Approbation** — l'Approbateur valide (champ `Approbateur` + `Verification` native Notion).
5. **MAJ de l'objet source** — à la clôture, WF 06 recalcule la prochaine échéance sur l'objet source.
6. **Archivage** — WF 05 déplace la tâche close vers l'archive thématique et journalise le run (*Archives - n8n Logs*).

**Valeur :** traçabilité de bout en bout — chaque action laisse une preuve datée, attribuée et archivée 5 ans.

## P2 — Cycle Achats

Diagramme : [diagrams/purchase-cycle.mmd](../diagrams/purchase-cycle.mmd).

De l'expression du besoin à la mise à jour du stock, avec quatre workflows :

1. **Mon Panier / Demande d'achat** — l'opérateur sélectionne dans le *Magasin* (boutons `🛒 Mon panier` / `Commander`) ; une *Demande d'achat* (DA) est créée.
2. **Approbation** — bouton *Approuver la demande*.
3. **Génération PO** — WF 07 (bouton *Check out*, à la demande) ou WF 08 (planifié, récurrent) regroupe les DA par fournisseur en *Bons de Commande*.
4. **Suivi PO** — WF 09 met à jour les statuts (envoyé, confirmé, livré) et les propage vers les DA.
5. **Réception / Magasin** — WF 10 ajuste le statut du *Magasin* ; les certificats reçus alimentent *Master Fournisseurs*.

**Workflows :** WF 07, WF 08, WF 09, WF 10. **Valeur :** traçabilité financière et conformité fournisseurs, avec une UX e-commerce côté opérateur.

## P3 — Cycle Documentation

Diagramme : [diagrams/documentation-cycle.mmd](../diagrams/documentation-cycle.mmd).

Garantir une source unique contrôlée pour la documentation qualité :

1. **Déclencheur** — veille normative ou action corrective imposant une mise à jour.
2. **Nouvelle version** — bouton *Nouvelle Version* sur *Master Documentations Entreprise*.
3. **Validation** — revue hiérarchique avant publication.
4. **Archivage WF 11** — la version précédente est automatiquement déplacée vers *Archive Documentations Entreprise* ; la version courante devient unique.
5. **Notification** — diffusion aux destinataires (mécanisme exact non détaillé dans les sources).

**Workflow :** WF 11. **Valeur :** maîtrise documentaire ISO 17025 — une seule version courante, historique conservé, retrait tracé des versions obsolètes.

## P4 — Cycle Conformité ISO 17025

Transformer les jalons d'accréditation en preuves opérationnelles :

1. **Calendrier Qualité** — entrée planifiée (audit interne, revue de direction, inter-lab, etc.).
2. **Scan WF 04** — matérialise le jalon en tâche qualité dans *Master Tâches*.
3. **Exécution** — la tâche est traitée, preuves jointes.
4. **Archivage WF 05.01** — la tâche close part vers *Archives Qualité*, constituant le dossier d'audit consolidé.

**Workflows :** WF 04 → WF 05.01. **Valeur :** préparation continue aux visites de surveillance ISO 17025, sans course de dernière minute. Détail des correspondances normatives : [docs/04](04-iso-17025-mapping.md).

## P5 — Cycle Équipements

Maintenir la justesse métrologique du parc — pilier technique de l'accréditation :

1. **Scan WF 01** — lecture des échéances de *Master Equipements* (étalonnage, maintenance, contrôle de déviation, indépendamment).
2. **Création des tâches** — via les sous-workflows WF 01.01 (maintenance / déviation) et WF 01.02 (calibration).
3. **Exécution** — interventions réalisées, résultats enregistrés.
4. **MAJ échéancier WF 06** — recalcul des prochaines dates sur l'équipement.
5. **Archivage WF 05.03** — historisation dans *Archives Contrôles des Équipements*.

**Workflows :** WF 01 → WF 06 → WF 05.03. **Valeur :** chaîne ininterrompue d'étalonnages, traçable. Limite relevée par l'audit : *Archives Contrôles des Équipements* n'a pas de relation directe vers *Master Equipements*, ce qui complique la reconstitution de l'historique métrologique d'un équipement précis.

## P6 — Cycle Formation et Onboarding RH

Diagramme : [diagrams/hr-onboarding-cycle.mmd](../diagrams/hr-onboarding-cycle.mmd). Détail complet : [docs/05](05-formation-rh.md).

Industrialiser la montée en compétences par *Type de poste* :

1. **Trousse par type de poste** — *Modules-Formations* obligatoires, ordre de passage, échéance (`Jours après embauche`).
2. **Déclenchement** — onboarding (WF 12, bouton *⚡ Inscription d'entrée*), programmation périodique (WF 14, planifié), ou demande individuelle (WF 15).
3. **Instance → Inscriptions** — une session est programmée puis les inscriptions par personne sont générées ; WF 13 maintient leur cohérence.
4. **Tâche RACI** — WF 16 pousse l'inscription en tâche dans *Master Tâches* (bouton *⚡ Créer une tâche*).
5. **Exécution → Approbation** — l'employé suit la formation, téléverse le certificat (*⚡ Terminer ma formation*), l'Approbateur RH valide.
6. **Dashboard** — indicateurs *En cours / Progression / Objectif* mis à jour.

**Workflows :** WF 12 à 16. **Valeur :** onboarding reproductible, formation continue tracée, preuve de qualification avec date de péremption.

## Captures

Sélection par processus (voir [screenshots/MANIFEST.md](../screenshots/MANIFEST.md)) :

- **P1 / tâches :** `master-taches_gestion-des-taches.png`, `master-taches_automatisation-de-taches.png`, `master-taches_formulaire-de-creation-de-tache.png`.
- **P2 / achats :** `achats_magasin-industriel.png`, `achats_gestion-des-demandes-d-achats.png`, `achats_gestion-des-purschase-order.png` *(à anonymiser)*.
- **P3 / documentation :** `documentation_bibliotheque-de-la-compagnie.png`.
- **P5 / équipements :** `equipements_controle-equipements-laboratoire.png`, `equipements_liste-des-equipements-laboratoire.png`, `equipements_zoom-sur-plan-de-controle.png`.
- **P6 / formation :** voir [docs/05](05-formation-rh.md).
