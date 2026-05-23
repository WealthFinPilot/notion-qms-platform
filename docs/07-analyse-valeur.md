# Analyse de valeur — enjeux, risques et ROI

> Ce document reprend le **dossier de valeur (business case)** établi pour justifier le déploiement de la plateforme QMS auprès de la direction. Les chiffres de coûts et de retour sur investissement sont **prévisionnels** (projection au moment de la décision), et non des résultats mesurés a posteriori. Posture conservée : le système *contribue à* la maîtrise du SMQ ; il ne *garantit pas* la conformité ISO/IEC 17025.

## Synthèse exécutive

La plateforme QMS répond à trois besoins opérationnels immédiats d'une PME de laboratoire accréditée (≈ 15-20 personnes) : **centralisation** de l'information, **traçabilité ISO/IEC 17025** et **coordination des responsabilités** (RACI). Elle offre un socle robuste et évolutif à 2-3 ans, peut servir de **prototype vivant** pour spécifier un futur progiciel sur mesure, et reste cohérente en coût face aux bénéfices attendus (rapidité, qualité, adoption). Ses limites principales portent sur l'analytique avancée, la dépendance à Notion et la tenue à une croissance forte. Avec une gouvernance claire, une documentation soignée et quelques garde-fous techniques, le rapport valeur/risque est jugé favorable.

## Forces clés

- **Adéquation immédiate au SMQ** : centralisation des données, des tâches et des exigences ISO 17025 ; meilleure lisibilité et conformité au quotidien.
- **Adoption facilitée** : interface moderne et mobile, vues simples par rôle ; déploiement progressif possible (pilote responsables → extension).
- **Architecture métier solide** : vues globales et par domaine (audits, équipements, formation…), attribution par type de poste (maintenabilité, remplacements facilités).
- **Automatisation n8n extensible** : rappels, création/MAJ de tâches, archivages, journaux — potentiel d'extension maîtrisé.
- **Capitalisation des connaissances** : référentiel unique (procédures, rôles, exigences) et architecture documentée (relations, rollups) utile à la formation et à la maintenance.
- **Réduction du risque « homme-clé »** : back end accessible pour relecture et évolution, moins de dépendance individuelle qu'un outillage VBA dispersé.
- **Réplicabilité multi-sites** : duplication de l'espace en conservant le squelette (reconnexion des webhooks à prévoir).

## Limites / faiblesses

- **Analytique avancée limitée** : pas de SQL natif ni de data-marts ; les tableaux de bord directionnels complexes exigent un pont externe.
- **Complexité du back end** : architecture dense (relations, rollups, boutons), intimidante pour un non-architecte ; la rétro-ingénierie globale est longue (abordable domaine par domaine).
- **Dépendance à Notion** : portabilité imparfaite ; écosystème plus naturel côté Google que Microsoft (Outlook / Teams / SharePoint).
- **Croissance forte** : au-delà d'un certain seuil d'effectifs ou de processus, une refonte ou une migration deviendrait probable.
- **Coûts d'abonnement** : forfait Business par siège ; l'IA n'est pas modulable (tout ou rien sur l'espace).
- **Sauvegardes et volumétrie** : à cadrer pour le long terme.
- **Résidence des données** : l'hébergement Notion se situe hors de la zone cible ; un déploiement contraint par la souveraineté des données impliquerait de relocaliser la couche n8n et de recâbler les connexions.

## Risques et mesures de mitigation

| # | Risque | Mesure de mitigation |
|---|---|---|
| R1 | Analytique directionnelle limitée → décisions stratégiques bridées | Pont analytique : exports contrôlés + n8n vers Power BI / tableur / base externe ; dictionnaire de données et vues « executive » |
| R2 | Dépendance à Notion / écosystème Microsoft | Intégrations n8n (Outlook/Graph, SharePoint), normalisation des exports, plan de sortie (modèle de données + mapping) |
| R3 | Sécurité et gestion des accès | Rôles et permissions, revue à chaque changement d'employé, journalisation n8n |
| R4 | Maintenabilité / turnover | Documentation vivante (schémas, runbooks), catalogue de relations à jour, formation croisée de 2 relais internes |
| R5 | Coûts récurrents | Politique de licences par rôle (responsables et chefs d'équipe prioritaires) |
| R6 | Charge et performance de la base centrale | Archivage régulier (WF 05), vues optimisées, nettoyage des relations lourdes |
| R7 | Résidence / souveraineté des données | Relocalisation possible de la couche n8n et recâblage des connexions Notion selon les contraintes de zone |

## Opportunités créatrices de valeur

- **Time-to-value rapide** : gains de temps, moins d'erreurs, meilleure préparation aux audits ISO 17025, traçabilité accrue.
- **Clarté des responsabilités** : visibilité des rôles et des échéances, responsabilisation des équipes.
- **Prototype pour un futur système sur mesure** : accélère les spécifications, réduit les coûts et les risques d'une migration ultérieure.
- **Réplicabilité multi-sites** : déploiement accéléré grâce au squelette existant.
- **Réduction du risque « homme-clé »** : transfert de savoir plus robuste qu'un outillage individuel.

## Coûts et retour sur investissement (projeté)

Hypothèses : forfait **Notion Business** (20 $ US / siège / mois, IA incluse, 250 sièges invités gratuits ; le forfait s'applique à tout l'espace partagé — pas de panachage). Trois scénarios de déploiement ont été chiffrés.

| Scénario | Périmètre | Coût annuel (CAD) |
|---|---|---|
| 1 | Tout le personnel a un siège (objectif final) | ≈ 5 515 $ |
| 2 | **Superviseurs et responsables seulement (recommandé au lancement)** | ≈ 2 950 $ |
| 3 | Noyau minimal de 6 personnes | ≈ 1 935 $ |

**Retour sur investissement projeté** — valorisation du temps gagné par siège (modèle : *1 heure économisée par semaine × 45 semaines ouvrées × taux horaire*ⁱ) :

| Scénario | Coût annuel | Gain projeté à 1 h/sem | Gain projeté à 2 h/sem | Retour |
|---|---|---|---|---|
| 1 | ≈ 5 515 $ | ≈ 21 600 $ | ≈ 43 200 $ | ≈ 4× à 8× |
| 2 *(recommandé)* | ≈ 2 950 $ | ≈ 12 150 $ | ≈ 24 300 $ | ≈ 4× à 8× |
| 3 | ≈ 1 935 $ | ≈ 6 975 $ | ≈ 13 950 $ | ≈ 4× à 7× |

ⁱ *Taux horaires illustratifs par rôle (Opérateur 25 $/h, Superviseur 35 $/h), sans donnée de paie réelle. Exemple : 25 $ × 1 h × 45 semaines = 1 125 $/an de productivité par siège. Coût d'un siège : ≈ 240 $/an. Le seuil de rentabilité est donc atteint pour quelques minutes de temps gagné par semaine et par siège.*

Lecture : même dans l'hypothèse prudente d'**une seule heure gagnée par semaine et par personne**, le retour projeté représente plusieurs fois le coût d'abonnement. Le scénario 2 (responsables d'abord) est recommandé au lancement car il maximise ce ratio tout en limitant l'engagement initial.

## Conditions de succès

- **Gouvernance** : sponsor à la direction, comité de pilotage (décisions, priorités).
- **Conception et documentation** : dictionnaire de données, schémas de relations, conventions de nommage, modèles de pages.
- **Adoption** : formation courte par rôle, guides vidéo, « champion » référent dans chaque domaine.
- **Qualité des données** : règles de saisie, contrôles n8n, plan d'archivage.
- **Sécurité et conformité** : permissions, revues d'accès, sauvegardes programmées, registre des traitements.

## Feuille de route proposée (3 mois)

- **M0–M1 — Cadre et sécurité** : rôles et permissions, cartographie des relations, sauvegarde/archivage, documentation « quick start ».
- **M1–M2 — Pilote responsables** : déploiement contrôlé, corrections rapides, mesures d'usage.
- **M2–M3 — Automatisations prioritaires** : rappels critiques SMQ, journaux, anti-doublons, archivage — quick wins.

---
*Analyse dérivée du dossier de valeur interne, anonymisée. Les montants sont des projections de décision, pas des résultats mesurés.*
