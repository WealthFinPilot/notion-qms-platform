# ANONYMIZE-ADDENDUM

> Éléments découverts **hors du périmètre écrit** d'`ANONYMIZE-TODO.md` §2 lors de l'anonymisation des 25 workflows JSON par l'Agent B.
> Le périmètre initial visait les `databaseId`/`pageId` des nœuds Notion, les chemins de webhook, les tokens en clair et l'URL d'asset WF 01.
> La reconnaissance a révélé une surface sensible bien plus large. Sébastien a **validé l'extension du périmètre** (« scrub Notion complet » + « vider pinData ») avant action.
> **Toutes les valeurs réelles sont masquées ci-dessous** — ce fichier est destiné au dépôt public.

---

## A. Données « pinData » (cache d'exécution de développement) — VIDÉ

`pinData` est un cache de données d'exécution épinglé pendant le développement ; il ne fait pas partie de la logique des workflows (aucun nœud ni connexion modifié en le vidant).

| Fichier source | Nœud épinglé | Contenu réel trouvé (masqué) | Action effectuée |
|---|---|---|---|
| WorkFlow 01.json | `Get Master Equipement2` | 71 enregistrements d'équipements réels : codes `ME-xx`/`MET-xx`, n° de série, modèles d'instruments, dates d'étalonnage, IDs de pages Notion, références `property_responsable` (personnes) | `pinData` mis à `{}` |
| WorkFlow 01.json | `Set Responsable1` | 1 enreg. : ID page + `property_responsable` (personne) | `pinData` mis à `{}` |
| WorkFlow 01.json | `Fix responsable1` | 1 enreg. : ID page + `property_responsable` (personne) | `pinData` mis à `{}` |

> L'**URL d'asset `notion-static.com`** mentionnée dans `ANONYMIZE-TODO.md` §2 (WF 01) se trouvait dans ce `pinData` (champ `avatar_url`) — elle a donc été supprimée avec le vidage. Aucune URL `notion-static` ne subsiste.

---

## B. Identifiants Notion hors des champs `databaseId`/`pageId` — REMPLACÉS par placeholders

`ANONYMIZE-TODO.md` ne visait que les champs `databaseId`/`pageId` des nœuds Notion. En réalité, des identifiants Notion étaient aussi présents dans :

| Fichier(s) source | Emplacement | Type d'élément (masqué) | Action effectuée |
|---|---|---|---|
| WF 01, 02, 03, 04, 05.0x, 07, 08, 09, 11–16 + sous-WF | URLs `https://www.notion.so/...<id>` (nœuds Notion `cachedResultUrl`, code, set) | IDs de bases/pages Notion encodés dans l'URL (formes avec et sans tirets) | Remplacés par le placeholder de la base correspondante |
| WF 02.01, 04.01, 11, 16, sous-WF 01.01/01.02, 03.01 | `jsonBody` (corps de requêtes HTTP), `notes` (sticky notes), `textContent`, `value` (Set) | 9 IDs Notion additionnels (data-sources / pages) sans nom fonctionnel identifiable | Remplacés par `{{NOTION_ID_GENERIC_01}}` … `{{NOTION_ID_GENERIC_09}}` (cohérents inter-fichiers) |

Les 17 bases nommées conservent un placeholder fonctionnel lisible : `{{NOTION_DB_ID_MASTER_TACHES}}`, `{{NOTION_DB_ID_MASTER_EQUIPEMENTS}}`, `{{NOTION_DB_ID_MAGASIN}}`, `{{NOTION_DB_ID_CERTIFICATS_FOURNISSEURS}}`, `{{NOTION_DB_ID_CALENDRIER_QUALITE}}`, `{{NOTION_DB_ID_MASTER_DOCUMENTATIONS_ENTREPRISE}}`, `{{NOTION_DB_ID_MASTER_EMPLOYES}}`, `{{NOTION_DB_ID_TACHES_RECURRENTES}}`, `{{NOTION_DB_ID_ARCHIVES_QUALITE}}`, `{{NOTION_DB_ID_ARCHIVES_CONTROLE_DES_CERTIFICATS_FOURNISSEURS}}`, `{{NOTION_DB_ID_ARCHIVES_CONTROLES_DES_EQUIPEMENTS}}`, `{{NOTION_DB_ID_ARCHIVES_DES_TACHES}}`, `{{NOTION_DB_ID_DEMANDES_D_ACHAT}}`, `{{NOTION_DB_ID_INSTANCES_DE_FORMATIONS}}`, `{{NOTION_DB_ID_MODULES_FORMATIONS}}`, `{{NOTION_DB_ID_INSCRIPTIONS_AUX_FORMATIONS}}`, `{{NOTION_DB_ID_BONS_DE_COMMANDE_PO}}`.

> Note : `pageId` n'a fait l'objet d'aucun remplacement de valeur littérale — tous les `pageId` des nœuds étaient des **expressions n8n dynamiques** (`={{ $json.id }}`, `={{ $('...').item.json.id }}`), non sensibles. Seuls des IDs Notion *littéraux* (dans code/set/notes/jsonBody/URLs) ont été remplacés.

---

## C. Champs `webhookId` — REMPLACÉS par placeholders

`ANONYMIZE-TODO.md` ne visait que le champ `path` des nœuds webhook. Or, pour WF 09/10/11/13/15/16, le `path` (UUID) est **identique** au `webhookId` du même nœud : anonymiser le `path` sans toucher au `webhookId` aurait laissé le secret du point d'entrée en clair.

| Fichier(s) source | Champ | Valeur (masquée) | Action effectuée |
|---|---|---|---|
| WF 06, 07, 09, 10, 11, 12, 13, 15, 16 | `webhookId` (nœud webhook) | UUID n8n = secret du point d'entrée | Remplacé par `{{WEBHOOK_ID_WFxx}}` |
| WF 12 | `webhookId` (nœud `Wait` — webhook de reprise) | UUID n8n distinct | Remplacé par `{{WEBHOOK_ID_WF12}}` |

Chemins (`path`) remplacés : `{{WEBHOOK_PATH_WF09}}` … `WF16`, et les chemins **nommés** WF 06 (`wf06/validate`) et WF 07 → `{{WEBHOOK_PATH_WF06_NAMED}}`, `{{WEBHOOK_PATH_WF07_NAMED}}`.

> WF 06 n'apparaissait pas dans la liste des webhooks d'`ANONYMIZE-TODO.md` §2 (le fichier y était décrit comme vide). Il est désormais plein et possède un chemin webhook nommé, anonymisé comme les autres. Voir §E.

---

## D. Credentials — AUCUNE action (conforme)

Aucun jeton / clé / secret en clair trouvé dans les 25 JSON (recherche `secret_…`, `Bearer …`, `ntn_…`, en-têtes `httpRequest` : **0 résultat**). Les références de credentials nommées (`Notion API`, `Notion Header`) sont des références sûres et n'ont **pas** été modifiées (règle 7).

---

## E. Divergence avec ANONYMIZE-TODO.md / docs

- `ANONYMIZE-TODO.md` §2 et `docs/02-workflows-n8n.md` décrivaient initialement **WF 06 comme un fichier vide (1 octet, `[INFO MANQUANTE]`)**. Le fichier source actuel `WorkFlow 06.json` contient **38 nœuds** (webhook `wf06/validate`, 12 nœuds Notion, etc.) et a été anonymisé normalement. → **Corrigé** : WF 06 est désormais documenté dans `docs/02-workflows-n8n.md` et la mention « fichier vide » a été levée dans `ANONYMIZE-TODO.md` §2.
- Identifiants Notion **non sensibles non touchés** : les 617 `id` de nœuds n8n, 25 IDs meta de workflow, et les IDs de lignes internes (Set `assignments`, conditions IF/Switch) — ce sont des identifiants structurels n8n, conservés tels quels pour ne pas altérer la logique.

---

## Récapitulatif des actions

| Catégorie | Hors périmètre écrit ? | Décision Sébastien | Statut |
|---|---|---|---|
| Vidage `pinData` (73 enreg. réels WF 01) | Oui | Vider | Fait |
| IDs Notion dans URLs `notion.so` | Oui | Scrub complet | Fait |
| 9 IDs Notion génériques (jsonBody/notes/code) | Oui | Scrub complet | Fait |
| `webhookId` (10 + 1 Wait) | Oui | Scrub complet (implicite) | Fait |
| 17 `databaseId` nommés | Non (périmètre initial) | — | Fait |
| Chemins webhook (10) | Non (périmètre initial) | — | Fait |
| URL asset `notion-static` | Non (périmètre initial) | — | Fait (via vidage pinData) |
| Tokens en clair | Non | — | Aucun trouvé |

*Agent B — addendum produit le 2026-05-21. Valeurs réelles conservées uniquement dans les fichiers source non publiés (`Source/Notion synthèse/Workflows/*.json`).*
