# Exports — Workflows n8n

25 workflows exportés depuis n8n, anonymisés avant publication.
Les identifiants de bases de données Notion, les chemins de webhook et les données d'instance
ont été remplacés par des placeholders documentés.

## Workflows principaux (WF 01–16)

| Fichier | Description |
|---|---|
| wf-01-scan-equipement.json | Scan QR équipement → création tâche |
| wf-02-scan-certificat.json | Scan QR certificat → création tâche vérification |
| wf-03-scan-tache-recurrente.json | Scan QR → déclenchement tâche récurrente |
| wf-04-scan-evenement-qualite.json | Scan QR → création tâche qualité |
| wf-05-archive-taches.json | Archivage des tâches complétées |
| wf-06-remise-a-jour-plannings.json | Mise à jour automatique des plannings |
| wf-07-regroupement-achat-po-sur-demande.json | Regroupement achats en PO (sur demande) |
| wf-08-regroupement-achat-po-planifie.json | Regroupement achats en PO (planifié mensuel) |
| wf-09-suivi-des-po.json | Suivi des purchase orders |
| wf-10-update-magasin.json | Mise à jour du magasin industriel |
| wf-11-mise-a-jour-documentation.json | Synchronisation documentation |
| wf-12-inscriptions-employes-automatiques.json | Inscriptions aux formations par type de poste |
| wf-13-mise-a-jour-formations-sur-commande.json | Mise à jour formations (sur commande) |
| wf-14-planification-inscription-module-formation.json | Planification des inscriptions formation |
| wf-15-inscription-individuelle-formations.json | Inscription individuelle aux formations |
| wf-16-creer-tache-formation-individuelle-raci.json | Création tâche formation individuelle avec RACI |

## Sous-workflows (WF 01.01–05.04)

| Fichier | Description |
|---|---|
| wf-01-01-creation-tache-maintenance-deviation-raci.json | Tâche complexe Maintenance/Déviation avec RACI |
| wf-01-02-creation-tache-calibration-raci.json | Tâche complexe Calibration avec RACI |
| wf-02-01-creation-tache-verification-certificats.json | Tâche vérification certificats fournisseurs |
| wf-03-01-creer-tache-recurrente.json | Création tâche récurrente |
| wf-04-01-creation-tache-evenement-qualite.json | Tâche liée à un événement qualité |
| wf-05-01-archive-tache-qualite.json | Archivage tâche qualité |
| wf-05-02-archive-tache-certificat.json | Archivage tâche certificat |
| wf-05-03-archive-tache-equipement.json | Archivage tâche équipement |
| wf-05-04-archive-tache-custom.json | Archivage tâche personnalisée |

## Note sur l'anonymisation

Les placeholders suivent la convention `{{TYPE_NOM_FONCTIONNEL}}`.
Voir `ANONYMIZE-TODO.md` et `ANONYMIZE-ADDENDUM.md` pour le détail complet.
