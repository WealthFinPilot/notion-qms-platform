# MANIFEST — Captures d'écran

> Inventaire construit à partir de `Source\Notion synthèse\ScreenShots de l'intranet Notion\Log des screenshots Notion.xlsx` (34 captures de l'intranet Notion) et des fichiers du dossier `Screenshots des workflows n8n` (27 captures, nommées d'après leur fichier source — non couvertes par le log Excel). Les images n'ont pas été ouvertes : la classification et l'anonymisation s'appuient sur les descriptions du log et sur les noms de fichiers.

**Convention de nommage :** `[catégorie]_[description-courte].png` (description en kebab-case, sans accents).

**Colonne Anonymisation :** `[ANONYMIZE]` lorsque la description ou le module évoque des noms de personnes, des fournisseurs, des prix ou des données personnelles ; `OK` sinon. Aucune image n'a été modifiée — l'anonymisation effective reste à appliquer avant publication (voir `ANONYMIZE-TODO.md`).

| Nom original | Nouveau nom | Catégorie | Description (depuis log) | Anonymisation | Utilisé dans |
|---|---|---|---|---|---|
| 00.01 - Page d'acceuil - Sous page children  - exemple de gestion de projet.png | `front-end_exemple-de-gestion-de-projet.png` | front-end | Exemple de gestion d'un projet, ici le déploiement de l'intranet dans la compagnie | OK | README.md · docs/01-architecture-back-end.md |
| 00 - Main - Page d'acceuil - SYSTÈME MANAGEMENT QUALITÉ ISO_IEC 17025.png | `front-end_systeme-management-qualite-iso-iec.png` | front-end | La page d'acceuil de l'intranet | OK | README.md · docs/01-architecture-back-end.md |
| 01.04 - Page Focus - Sous page children - Automatisation de tâches.png | `master-taches_automatisation-de-taches.png` | master-taches | Une vue base de données dans la section superviseur pour suivrents gérer ses tâches récurentes programmés et traités automatiquements. Ainsi le superviseur peux automatiser sans être un expert. N8n prend le relais sans qu'il s'en appercoive. | OK | docs/03-processus-cles.md · docs/01-architecture-back-end.md |
| 01.01 - Page Focus - Sous page children - Espace personnel employé.png | `master-taches_espace-personnel-employe.png` | master-taches | Une vue Kanban des tâches de l'employés. C'est son espace personnel. | [ANONYMIZE] | docs/03-processus-cles.md · docs/01-architecture-back-end.md |
| 01.06 - Page Focus - Sous page children - Formulaire de création de tâche automatique.png | `master-taches_formulaire-de-creation-de-tache-2.png` | master-taches | Un formulaire de plannification de tâche automatisé. | OK | docs/03-processus-cles.md · docs/01-architecture-back-end.md |
| 01.05 - Page Focus - Sous page children - Formulaire de création de tâche.png | `master-taches_formulaire-de-creation-de-tache.png` | master-taches | Un formulaire de plannification de tâche. | OK | docs/03-processus-cles.md · docs/01-architecture-back-end.md |
| 01 - Main - Page Focus - Gestion des tâches.png | `master-taches_gestion-des-taches.png` | master-taches | La page d'acceuil des la gestion opérationnelles nomé "Focus" | OK | README.md · docs/03-processus-cles.md · docs/01-architecture-back-end.md |
| 01.02 - Page Focus - Sous page children - Espace superviseur - section approbation.png | `master-taches_section-approbation.png` | master-taches | Une vue base de données dans la section superviseur pour que le superviseur du département approuve les fins de tâches des employés du départements | [ANONYMIZE] | docs/03-processus-cles.md · docs/01-architecture-back-end.md |
| 01.03 - Page Focus - Sous page children - Espace superviseur - section gestion des opérations.png | `master-taches_section-gestion-des-operations.png` | master-taches | Une vue base de données dans la section superviseur pour que le superviseur du département suivent les tâches des employés du départements | [ANONYMIZE] | docs/03-processus-cles.md · docs/01-architecture-back-end.md |
| 01 a - Page Focus - Zoom sur planning de la semaine.png | `master-taches_zoom-sur-planning-de-la.png` | master-taches | Zoom sur un planning personnalisé. L'employé ne vois que ces tâches plannifiés. | [ANONYMIZE] | docs/03-processus-cles.md · docs/01-architecture-back-end.md |
| A - Exemple d'une base de donnée structuré du back end.png | `back-end_exemple-d-une-base-de.png` | back-end | Un exemple d'une base de données structurés du Back end. | OK | docs/01-architecture-back-end.md |
| back-end_n8n-API-key-to-Notion.png | `back-end_n8n-API-key-to-Notion.png` | back-end | Screenshot de l'interface n8n montrant la configuration de la clé API vers Notion. 100% anonymisé — aucune clé ou credential visible. | OK | docs/01-architecture-back-end.md |
| back-end_NOTION-API.png | `back-end_NOTION-API.png` | back-end | Screenshot de l'interface Notion montrant la configuration de l'API. 100% anonymisé — aucune clé ou credential visible. | OK | docs/01-architecture-back-end.md |
| B - Base de donnée des Logs n8n et suivis execution des workflows.png | `architecture_base-de-donnee-des-logs.png` | architecture | La base de données de suivis des logs n8n enregistrant, le workflow, les logs, les Run ID, le temps d'executions, le nombre d'action effectué, le nombre d'actions, le nombre échoués, Pass/Fail | OK | docs/01-architecture-back-end.md |
| D - Base de données des suivis des workflows n8n.png | `architecture_base-de-donnees-des-suivis.png` | architecture | La base de données de suivis des workflows pour maintient et orchestration. | OK | docs/01-architecture-back-end.md |
| C - Base de données du suivis des bases de données Notion.png | `architecture_base-de-donnees-du-suivis.png` | architecture | La base de données de suivis des bases de données Notion pour maintient et orchestration. | OK | docs/01-architecture-back-end.md |
| Governance-flowchart.png | `architecture_governance-flowchart.png` | architecture | Governance-flowchart | OK | README.md · docs/01-architecture-back-end.md |
| (ajout manuel) | `architecture_tableau-de-bord-projet.png` | architecture | Dashboard de suivi du projet : 302h cumulées sur 5 mois, répartition par catégorie (n8n 150h, Notion 135h, Rapport 15h, Hostinger 4h), taux de participation 64%, rythme moyen 3.8h/jour ouvré. | OK | README.md · docs/01-architecture-back-end.md |
| (ajout manuel) | `architecture_tableau-de-bord-projet-2.png` | architecture | Dashboard des métriques du dévellopement Back end / Front end : 6 Pages Notion, 38 Sous pages, 6 Formulaires, 26 automatisation n8n, 16 Workflow principaux, 10 Sous Workflows, 10 Webhook trigger, 7 Schedule trigger, Run time average : 3.87 secondes, Répartition de la charge Back end Vs Front end (77% Back end, 18% Front end, 5% Autre), Perception de la difficulté des tâches (129 tâches, 47% Facile, 25% Moyenne, 19% élevé, 9% Très élevé) | OK | README.md · docs/01-architecture-back-end.md |
| (ajout manuel) | `architecture_tableau-de-bord-projet-3.png` | architecture | QMS Dashboard 17025 Suivi de Projet : 41 Jalons Qualité, 92 Équipements, 104 Fournisseurs, 205 Consommables, 5 Départements, 15 Employés, 372 Documents, Répartition de la charge par exigences ISO/IEC 17025 (Gestion des équipements 63 heures, Achats et Fournisseurs 57 heures, Maintenance et Sécurité des données 57 heures, Gestion des Opérations 32 heures, Documentation du projet 31 heures, Gestion du Système Management Qualité 26 heures, Gestion de la documentation entreprise 24h, Gestion des Ressources Humaines 15 heures) | OK | README.md · docs/01-architecture-back-end.md |
| 02.03 - Page Controle - Sous page children - Contrôle des certifications des fournisseurs.png | `equipements_controle-des-certifications-des-fournisseurs.png` | equipements | Une vue étiquettes des certificats des fournisseurs de calibration avec leurs statuts et barres de progressions jusqu’à péremption pour facilité le contrôle. | [ANONYMIZE] | docs/03-processus-cles.md |
| 02.01 - Page Controle - Sous page children - Contrôle Equipements Laboratoire.png | `equipements_controle-equipements-laboratoire.png` | equipements | Une liste des équipements contrôlés avec status et barres de progression jusqu'au prochain évêvement (Calbration, maintenance, suivis). | OK | docs/03-processus-cles.md |
| 02 - Main - Page Contrôle - Gestion des équipements.png | `equipements_gestion-des-equipements.png` | equipements | La page d'acceuil des la gestion opérationnelles nomé "Contrôle" | OK | docs/03-processus-cles.md |
| 02.02 - Page Controle - Sous page children - Liste des Equipements Laboratoire.png | `equipements_liste-des-equipements-laboratoire.png` | equipements | Une vue étiquettes des équipements avec leurs photos et le statut en cours (Disponibles, en quarantaine etc). | OK | docs/03-processus-cles.md |
| 02 a - Page Contrôle - Zoom sur Plan de contrôle mensuel.png | `equipements_zoom-sur-plan-de-controle.png` | equipements | Exemple d'un plan de contrôle mensuel des équipements. | OK | docs/03-processus-cles.md |
| 03 - Main - Page Achât - Espace personnel des demandes et livraisons.png | `achats_espace-personnel-des-demandes-et.png` | achats | La page d'acceuil de la gestion opérationnelles nomé "Achâts". On peut y voir une section personnel du suivis de ses demandes. | [ANONYMIZE] | docs/03-processus-cles.md |
| 03.03 - Page Achât - Sous page children - section superviseur - Gestion des demandes d'achats.png | `achats_gestion-des-demandes-d-achats.png` | achats | Dans la section superviseur - Une vue base de donnée des demandes listés groupés par fournisseurs avec demandeur etc.. | [ANONYMIZE] | docs/03-processus-cles.md |
| 03.04 - Page Achât - Sous page children - section superviseur - Gestion des Purschase Order.png | `achats_gestion-des-purschase-order.png` | achats | Dans la section superviseur - Une vue kanban des demandes regroupés sous un PO et de l'avancés de la demande. | [ANONYMIZE] | docs/03-processus-cles.md |
| 03.02 - Page Achât - Sous page children - Gestion fournisseurs.png | `achats_gestion-fournisseurs.png` | achats | Une vue base de donnée des fournisseurs. | [ANONYMIZE] | docs/03-processus-cles.md |
| 03.01 - Page Achât - Sous page children - Magasin industriel.png | `achats_magasin-industriel.png` | achats | Un magasin virtuel style e-commerce des consommables de l'entreprise pour effectué une demande. Les items sont listés en étiquettes avec leurs photos. Un bouton est disponible pour faire la demande et le statut (commandé, ou en cours) est disponible. | [ANONYMIZE] | docs/03-processus-cles.md |
| 05 - Main - Page Bibliothèques - Bibliothèque de la compagnie.png | `documentation_bibliotheque-de-la-compagnie.png` | documentation | Point de vérité unique ou les documents sont catégorisés, listés, groupés, et constitue le point de vérité unique de l'entreprise. | OK | docs/03-processus-cles.md |
| 04.03 - Page Ressource humaine - Sous page children - Espace personnel de suivis des formations.png | `rh-formation_espace-personnel-de-suivis-des.png` | rh-formation | Section personnel du suivis de ses inscriptions grace a une vue base de donnée. | [ANONYMIZE] | docs/05-formation-rh.md |
| 04.02 - Page Ressource humaine - Sous page children - Exemple d'Espace de formation personnel.png | `rh-formation_exemple-d-espace-de-formation.png` | rh-formation | Exemple d'une page de formation avec vidéo youtube embeded à suivre et bouton pour valider la formation. | [ANONYMIZE] | docs/05-formation-rh.md |
| 04.04 - Page Ressource humaine - formulaire de demande de formation.png | `rh-formation_formulaire-de-demande-de-formation.png` | rh-formation | Formulaire pour effectuer une demande de formation. | [ANONYMIZE] | docs/05-formation-rh.md |
| 04.01 - Page Ressource humaine - Sous page children - section superviseur - Gestion des employés.png | `rh-formation_gestion-des-employes.png` | rh-formation | Section superviseur - Une vue base de données des employés. | [ANONYMIZE] | docs/05-formation-rh.md |
| 04.05 - Page Ressource humaine - Sous page children - Section superviseur - Gestion des modules de formations.png | `rh-formation_gestion-des-modules-de-formations.png` | rh-formation | Section superviseur - Gestion des modules de formations grace à une vue base de donnée. | [ANONYMIZE] | docs/05-formation-rh.md |
| 04.06 - Page Ressource humaine - Sous page children - Section superviseur - Programmation des instances de formation.png | `rh-formation_programmation-des-instances-de-formation.png` | rh-formation | Section superviseur - Bases de données de programmations des instances de formations avec bouton pour automatiser les inscriptions par types de poste. | [ANONYMIZE] | docs/05-formation-rh.md |
| 04 - Main - Page Ressource Humaine - RH.png | `rh-formation_rh.png` | rh-formation | La page d'acceuil de la gestion des ressources humaines nomé "RH" | [ANONYMIZE] | docs/05-formation-rh.md |
| 04.07 - Page Ressource humaine - Sous page children - Section superviseur - Suivis des employés.png | `rh-formation_suivis-des-employes.png` | rh-formation | Section superviseur - Bases de données du suivis de toutes les inscriptions des employés au cas par cas. | [ANONYMIZE] | docs/05-formation-rh.md |
| 04.05 - Page Ressource humaine - Sous page children - Section superviseur - Suivis global des formations.png | `rh-formation_suivis-global-des-formations.png` | rh-formation | Section superviseur - Suivis global des formations complètes avec barres de progressions pour facilités le suivis des objectifs. | [ANONYMIZE] | docs/05-formation-rh.md |
| Logger - Create debugging report.png | `workflow-n8n_logger-create-debugging-report.png` | workflow-n8n | Logger - Create debugging report | OK | docs/02-workflows-n8n.md |
| WF01.01 - Creation tache complexe MaintenaNnce OU deviation avec RACI.png | `workflow-n8n_wf01-01-creation-tache-complexe-maintenannce-ou.png` | workflow-n8n | Creation tache complexe MaintenaNnce OU deviation avec RACI | OK | docs/02-workflows-n8n.md |
| WF01.02 - Creation tache complexe Calibration avec RACI.png | `workflow-n8n_wf01-02-creation-tache-complexe-calibration-avec.png` | workflow-n8n | Creation tache complexe Calibration avec RACI | OK | docs/02-workflows-n8n.md |
| WF01 - Scan Equipement.png | `workflow-n8n_wf01-scan-equipement.png` | workflow-n8n | Scan Equipement | OK | README.md · docs/02-workflows-n8n.md |
| WF02.01 - Creation tache vérification des certificats fournisseurs.png | `workflow-n8n_wf02-01-creation-tache-verification-des-certificats.png` | workflow-n8n | Creation tache vérification des certificats fournisseurs | OK | docs/02-workflows-n8n.md |
| WF02 - Scan certificat.png | `workflow-n8n_wf02-scan-certificat.png` | workflow-n8n | Scan certificat | OK | docs/02-workflows-n8n.md |
| WF03.01 - Creer une tache recurrente.png | `workflow-n8n_wf03-01-creer-une-tache-recurrente.png` | workflow-n8n | Creer une tache recurrente | OK | docs/02-workflows-n8n.md |
| WF03 - Scan tache recurrente.png | `workflow-n8n_wf03-scan-tache-recurrente.png` | workflow-n8n | Scan tache recurrente | OK | docs/02-workflows-n8n.md |
| WF04.01 - Creation d'une tache lié a un evenement qualité.png | `workflow-n8n_wf04-01-creation-d-une-tache-lie.png` | workflow-n8n | Creation d'une tache lié a un evenement qualité | OK | docs/02-workflows-n8n.md |
| WF04 - scan evenement qualité.png | `workflow-n8n_wf04-scan-evenement-qualite.png` | workflow-n8n | scan evenement qualité | OK | docs/02-workflows-n8n.md |
| WF05.01 - Archive tache qualité.png | `workflow-n8n_wf05-01-archive-tache-qualite.png` | workflow-n8n | Archive tache qualité | OK | docs/02-workflows-n8n.md |
| WF05.02 - Archive tache Certificat.png | `workflow-n8n_wf05-02-archive-tache-certificat.png` | workflow-n8n | Archive tache Certificat | OK | docs/02-workflows-n8n.md |
| WF05.03 - Archive tache Equipement.png | `workflow-n8n_wf05-03-archive-tache-equipement.png` | workflow-n8n | Archive tache Equipement | OK | docs/02-workflows-n8n.md |
| WF05.04 - Archive tache custom.png | `workflow-n8n_wf05-04-archive-tache-custom.png` | workflow-n8n | Archive tache custom | OK | docs/02-workflows-n8n.md |
| WF05 - Archive taches.png | `workflow-n8n_wf05-archive-taches.png` | workflow-n8n | Archive taches | OK | docs/02-workflows-n8n.md |
| WF06 - Remise à jours des plannings des taches.png | `workflow-n8n_wf06-remise-a-jours-des-plannings.png` | workflow-n8n | Remise à jours des plannings des taches | OK | docs/02-workflows-n8n.md |
| WF07 - Regroupement achat en PO sur demande.png | `workflow-n8n_wf07-regroupement-achat-en-po-sur.png` | workflow-n8n | Regroupement achat en PO sur demande | OK | docs/02-workflows-n8n.md |
| WF08 - REgroupement achat en Purchase order plannifié.png | `workflow-n8n_wf08-regroupement-achat-en-purchase-order.png` | workflow-n8n | REgroupement achat en Purchase order plannifié | OK | docs/02-workflows-n8n.md |
| WF09 - Suivis des PO.png | `workflow-n8n_wf09-suivis-des-po.png` | workflow-n8n | Suivis des PO | OK | docs/02-workflows-n8n.md |
| WF10 - Update du Magasin.png | `workflow-n8n_wf10-update-du-magasin.png` | workflow-n8n | Update du Magasin | OK | docs/02-workflows-n8n.md |
| WF11 - Mise à jours documentation.png | `workflow-n8n_wf11-mise-a-jours-documentation.png` | workflow-n8n | Mise à jours documentation | OK | docs/02-workflows-n8n.md |
| WF12 - Inscriptions des employés automatiques par type de poste.png | `workflow-n8n_wf12-inscriptions-des-employes-automatiques-par.png` | workflow-n8n | Inscriptions des employés automatiques par type de poste | OK | docs/02-workflows-n8n.md |
| WF13 - Mise à jours des formations sur commande.png | `workflow-n8n_wf13-mise-a-jours-des-formations.png` | workflow-n8n | Mise à jours des formations sur commande | OK | docs/02-workflows-n8n.md |
| WF14 - Plannification d'inscription module formation.png | `workflow-n8n_wf14-plannification-d-inscription-module-formation.png` | workflow-n8n | Plannification d'inscription module formation | OK | docs/02-workflows-n8n.md |
| WF15 - Inscription individuelle aux formations.png | `workflow-n8n_wf15-inscription-individuelle-aux-formations.png` | workflow-n8n | Inscription individuelle aux formations | OK | docs/02-workflows-n8n.md |
| WF16 - Creer une tache de formation individuelle avec RACI.png | `workflow-n8n_wf16-creer-une-tache-de-formation.png` | workflow-n8n | Creer une tache de formation individuelle avec RACI | OK | docs/02-workflows-n8n.md |

## Récapitulatif

| Catégorie | Nombre |
|---|---|
| front-end | 2 |
| master-taches | 8 |
| back-end | 3|
| architecture | 7 |
| equipements | 5 |
| achats | 5 |
| documentation | 1 |
| rh-formation | 9 |
| workflow-n8n | 26 |
| **Total** | **66** |

## Fichiers manquants

Aucun fichier référencé dans le log n'est introuvable dans le dossier source : les 34 lignes du log correspondent toutes à un fichier présent. Les 27 captures de workflows n8n ne figurent pas dans le log Excel (leur nom de fichier sert de source descriptive).

## À anonymiser

Captures marquées `[ANONYMIZE]` (détail et justification dans `ANONYMIZE-TODO.md`) :

 - Les captures ont été anonymisé par Sébastien en ajoutant des traits noir empêchant la lecture des informations sensibles.