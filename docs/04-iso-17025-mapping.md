# Correspondance ISO/IEC 17025:2017

> Le système *contribue à* documenter, structurer et tracer des éléments utiles à la maîtrise d'un SMQ de laboratoire. Il ne constitue pas une preuve de conformité complète ni ne garantit l'accréditation, qui reste une décision de l'organisme accréditeur.

Ce tableau consolide les correspondances établies au fil de l'analyse. Il n'ajoute rien qui ne soit présent dans les sources. Les niveaux de lien se lisent ainsi :

- **Direct** — le composant contribue explicitement à l'exigence visée.
- **Indirect** — le composant soutient l'exigence sans la couvrir à lui seul.
- **À confirmer** — exigence non couverte explicitement par l'espace Notion à ce jour ; gap potentiel à formaliser.

## Tableau de correspondance

| Élément du projet (plateforme QMS) | Paragraphes ISO/IEC 17025:2017 | Contribution à la conformité | Niveau de lien |
|---|---|---|---|
| Master Tâches + matrice RACI | §5.5 b, §5.6, §7.5, §8.4 | Centralise les responsabilités, les enregistrements techniques et la traçabilité d'exécution de toutes les actions | Direct |
| Master Equipements + WF 01 + WF 06 | §6.4.3, §6.4.6, §6.4.7, §6.4.8, §6.4.13, §6.5, Annexe A | Programme d'étalonnage tenu à jour, identification du statut, historique, contribution à la traçabilité métrologique | Direct |
| Cycle Achats (DA vers PO vers Magasin) + WF 02 / 07 / 08 / 09 / 10 | §6.6.1, §6.6.2 a-d, §6.6.3 a-b, §6.4.11 | Maîtrise des prestataires externes, communication des exigences, suivi des certificats fournisseurs | Direct |
| Gestion Locaux (Salles de travail, Stockages) | §6.3.1, §6.3.2, §6.3.3, §6.3.4 | Documentation du cadre physique et des conditions d'environnement | Direct |
| Calendrier Qualité + WF 04 | §7.7, §8.8, §8.9 | Pilotage planifié de la surveillance, des audits internes et de la revue de direction | Direct |
| Scope ISO 17025 + Types de procédé | §5.3, §7.2 | Définition documentée du champ d'activités et des méthodes utilisées | Direct |
| Documentation entreprise + WF 11 + Archives doc | §8.2, §8.3.1, §8.3.2 a-f | Approbation, revue, identification des versions, retrait des versions obsolètes | Direct |
| Hub RH + sous-système Formation (Inscriptions, Modules-Formations, Instances) | §6.2.2, §6.2.3, §6.2.5 a-f, §6.2.6 | Exigences de compétence documentées, formation enregistrée, autorisations tracées avec péremption | Direct |
| Profils Front End (commun / gestionnaires / personnels) | §4.2, §7.11.3 a | Confidentialité, accès maîtrisé et différencié à l'information | Direct |
| WF 05 Archivage + logs n8n + bases Archives | §7.5.2, §8.4.2, §8.4.3 | Rétention, intégrité, identification des amendements et des auteurs | Direct |
| Architecture SMQ (Modules SMQ + Modules n8n) | §8.2.4, Annexe B | Auto-documentation du système de management — soutien à la maintenabilité | Indirect |
| RACI + séparation Approbateur | §4.1.4, §4.1.5 | Contribue à l'identification et à la minimisation des risques d'impartialité | Indirect |
| WF 03 Tâches récurrentes (rituels qualité) | §7.7.1, §8.5 | Surveillance planifiée de la validité des résultats et traitement des risques | Indirect |
| Rollups, dashboards Notion (analytique) | §7.7.3, §8.9.2 | Surveillance et entrants de revue de direction — limite reconnue : absence de SQL natif, à compenser par BI externe | À confirmer |
| Travail non conforme (module non identifié) | §7.10.1, §7.10.2 | Gap potentiel — exigence non couverte explicitement, à formaliser | À confirmer |
| Actions correctives (module non identifié) | §8.7.1, §8.7.2, §8.7.3 | Gap potentiel — exigence non couverte explicitement, à formaliser | À confirmer |
| Registre de risques formel (non identifié) | §8.5.1, §8.5.2, §8.5.3 | Gap potentiel — la dette technique gagnerait à être consignée formellement | À confirmer |

**Répartition :** 10 lignes *Direct*, 3 lignes *Indirect*, 4 lignes *À confirmer*. Les lignes *À confirmer* identifient les exigences non encore couvertes explicitement par l'espace Notion.

## Éléments hors périmètre

Le projet ne prétend pas couvrir seul l'ensemble d'ISO/IEC 17025:2017. Les sujets suivants sont présentés comme hors périmètre visible, à confirmer ou à formaliser :

| Sujet | Référence ISO/IEC 17025:2017 | Statut dans le portfolio |
|---|---|---|
| Réclamations | §7.9 | Non démontré explicitement |
| Travail non conforme | §7.10 | À formaliser ou documenter |
| Actions correctives | §8.7 | À formaliser ou documenter |
| Rapports d'essais | §7.8 | Hors périmètre visible |
| Règles de décision | §7.1.3, §7.8.6 | Hors périmètre visible |
| Validation complète du système d'information | §7.11 | À documenter si le système devient critique pour les données qualité |

## Lecture du tableau

Les niveaux *Direct*, *Indirect* et *À confirmer* traduisent une **gradation de contribution**, pas une note de conformité. Un lien *Direct* signifie que le composant participe explicitement à l'exigence (par exemple, l'archivage WF 05 contribue à la maîtrise des enregistrements §8.4) ; un lien *Indirect* qu'il la soutient sans la garantir (l'auto-documentation §8.2.4) ; *À confirmer* marque un gap assumé.

Cette transparence est volontaire : elle présente le projet avec une posture **crédible et audit-compatible**. Le système contribue à la maîtrise d'un SMQ de laboratoire ; il ne se substitue pas à un dossier officiel d'accréditation et ne garantit pas une décision favorable de l'organisme accréditeur.
