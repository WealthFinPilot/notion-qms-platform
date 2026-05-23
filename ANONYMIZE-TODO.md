# ANONYMIZE-TODO

> Liste de contrôle des éléments à anonymiser **avant toute publication publique** du dépôt. Le document source porte une mention de confidentialité explicite : le dépôt public doit être dérivé, anonymisé et reformulé. Aucune image n'a été modifiée par l'agent générateur ; aucun nom de personne réelle, fournisseur, prix, URL interne ou credential n'a été reproduit dans les fichiers `.md` ou `.mmd` générés.

## 1. Captures d'écran à anonymiser (19)

Marquées `[ANONYMIZE]` dans `screenshots/MANIFEST.md` — susceptibles d'exposer noms d'employés, fournisseurs, prix ou données personnelles. À flouter / caviarder avant publication.

| Nouveau nom | Catégorie | Raison probable (depuis la description du log) |
|---|---|---|
| `achats_espace-personnel-des-demandes-et.png` | achats | La page d'acceuil de la gestion opérationnelles nomé "Achâts". On peut y voir une section personnel du suivis de ses demandes. |
| `achats_gestion-des-demandes-d-achats.png` | achats | Dans la section superviseur - Une vue base de donnée des demandes listés groupés par fournisseurs avec demandeur etc.. |
| `achats_gestion-des-purschase-order.png` | achats | Dans la section superviseur - Une vue kanban des demandes regroupés sous un PO et de l'avancés de la demande. |
| `achats_gestion-fournisseurs.png` | achats | Une vue base de donnée des fournisseurs. |
| `achats_magasin-industriel.png` | achats | Un magasin virtuel style e-commerce des consommables de l'entreprise pour effectué une demande. Les items sont listés en étiquettes avec leurs photos. Un bouton est disponible pour faire la demande et le statut (commandé, ou en cours) est disponible. |
| `equipements_controle-des-certifications-des-fournisseurs.png` | equipements | Une vue étiquettes des certificats des fournisseurs de calibration avec leurs statuts et barres de progressions jusqu’à péremption pour facilité le contrôle. |
| `master-taches_espace-personnel-employe.png` | master-taches | Une vue Kanban des tâches de l'employés. C'est son espace personnel. |
| `master-taches_section-approbation.png` | master-taches | Une vue base de données dans la section superviseur pour que le superviseur du département approuve les fins de tâches des employés du départements |
| `master-taches_section-gestion-des-operations.png` | master-taches | Une vue base de données dans la section superviseur pour que le superviseur du département suivent les tâches des employés du départements |
| `master-taches_zoom-sur-planning-de-la.png` | master-taches | Zoom sur un planning personnalisé. L'employé ne vois que ces tâches plannifiés. |
| `rh-formation_espace-personnel-de-suivis-des.png` | rh-formation | Section personnel du suivis de ses inscriptions grace a une vue base de donnée. |
| `rh-formation_exemple-d-espace-de-formation.png` | rh-formation | Exemple d'une page de formation avec vidéo youtube embeded à suivre et bouton pour valider la formation. |
| `rh-formation_formulaire-de-demande-de-formation.png` | rh-formation | Formulaire pour effectuer une demande de formation. |
| `rh-formation_gestion-des-employes.png` | rh-formation | Section superviseur - Une vue base de données des employés. |
| `rh-formation_gestion-des-modules-de-formations.png` | rh-formation | Section superviseur - Gestion des modules de formations grace à une vue base de donnée. |
| `rh-formation_programmation-des-instances-de-formation.png` | rh-formation | Section superviseur - Bases de données de programmations des instances de formations avec bouton pour automatiser les inscriptions par types de poste. |
| `rh-formation_rh.png` | rh-formation | La page d'acceuil de la gestion des ressources humaines nomé "RH" |
| `rh-formation_suivis-des-employes.png` | rh-formation | Section superviseur - Bases de données du suivis de toutes les inscriptions des employés au cas par cas. |
| `rh-formation_suivis-global-des-formations.png` | rh-formation | Section superviseur - Suivis global des formations complètes avec barres de progressions pour facilités le suivis des objectifs. |

## 2. Workflows n8n (champs JSON et captures de canvas)

Non reproduits dans les fichiers générés, mais présents dans les sources et potentiellement visibles sur les captures de canvas n8n (catégorie `workflow-n8n`) :

- **Chemins de webhook (UUID).** WF 09, WF 10, WF 11, WF 12, WF 13, WF 15, WF 16 utilisent des chemins de webhook sous forme d'identifiants UUID ; WF 06 et WF 07 utilisent des chemins nommés (`wf06/validate`, anonymisé `{{WEBHOOK_PATH_WF06_NAMED}}`). Ces chemins sont des points d'entrée callables : ne pas les publier (ni dans les JSON, ni sur les captures de canvas).
- **Identifiants de base de données Notion.** Les nœuds Notion référencent des `databaseId` / `pageId` ; visibles dans les configs de nœuds sur les captures. À masquer.
- **Credentials.** Toutes les connexions utilisent une credential nommée `Notion API` (et `Notion Header` pour les sous-workflows d'archivage WF 05.0x). Aucun jeton en clair n'a été trouvé dans l'extraction, mais vérifier les nœuds `httpRequest` / en-têtes avant publication des JSON.
- **URL d'asset.** WF 01 contient une URL d'image hébergée (`...notion-static.com/...`) dans une note de canvas ; asset public à faible risque, à retirer par cohérence.
- **WF 06.** Le fichier source était initialement décrit comme vide (1 octet) ; il est désormais complet (38 nœuds, dont 12 nœuds Notion) et a été anonymisé comme les autres — chemin de webhook nommé `wf06/validate` remplacé par `{{WEBHOOK_PATH_WF06_NAMED}}`, `webhookId` remplacé par `{{WEBHOOK_ID_WF06}}`, `pinData` vide. Documenté dans `docs/02-workflows-n8n.md` (cf. `ANONYMIZE-ADDENDUM.md` §E).

## 3. Agents IA

- Les **prompts verbatim ne sont pas reproduits** dans `docs/06-agents-ia.md` (règle de confidentialité respectée).
- Les prompts sources (`Source/Notion synthèse/Prompt des agents IA/`) référencent des **URLs internes Notion** (identifiants de pages, ex. la page *Master Tâches*). À retirer si les prompts sources sont publiés.
- Le prompt de l'agent 1 contient un prénom à titre d'**exemple fictif** (non réel) — sans risque.

## 4. Passages texte des fichiers générés

Aucun nom de personne réelle, fournisseur, prix, salaire, URL interne ou credential n'apparaît dans les fichiers `.md` / `.mmd` produits. Les bases sont nommées par leur intitulé fonctionnel générique (Master Tâches, Master Fournisseurs, etc.), sans données d'instance. **Vérification effectuée.**

## Récapitulatif

| Type d'élément | À anonymiser |
|---|---|
| Captures d'écran | 19 sur 61 |
| Chemins de webhook / IDs de base (JSON + captures) | À masquer avant publication |
| Prompts d'agents IA (URLs internes) | Non publiés ici ; à nettoyer si publiés |
| Fichiers .md / .mmd générés | Aucun (vérifié) |
