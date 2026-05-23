# Agents IA de la plateforme QMS

## Vue d'ensemble

La plateforme QMS intègre des **agents Notion AI** configurés sur des pages existantes du workspace. Ils ne remplacent pas les workflows n8n (qui automatisent des processus) : ils offrent une **interface conversationnelle** posée sur les bases du SMQ, pour interroger et faire évoluer la donnée dans le respect des rôles. Le workspace les recense dans la base *Nos agents* (hub Documentation), simple annuaire `Fonction` / `Nom`.

Deux agents sont documentés dans les sources (`Source/Notion synthèse/Prompt des agents IA/`). Ils partagent un même contexte métier — PME métallurgique d'environ 20 personnes, laboratoire d'essais destructifs accrédité ISO 17025, documentation interne en français et externe en anglais — et une même posture : suivre les instructions de l'utilisateur, rester structuré, confirmer avant toute action sensible.

> **Confidentialité.** Les prompts ne sont pas reproduits ici : seule la logique fonctionnelle est décrite. Les prompts sources référencent des URLs internes Notion (identifiants de pages) — voir `ANONYMIZE-TODO.md`.

## Diagramme

[diagrams/ai-agents-overview.mmd](../diagrams/ai-agents-overview.mmd).

## Agents

### Le planificateur — Suivi de l'action

- **Rôle :** assistant de suivi des tâches, orienté responsabilité et planification. Il aide à enregistrer, prioriser, planifier et suivre les actions, et restitue des suivis structurés (listes d'actions, marqueurs de priorité, tableaux de progression) mettant en avant responsabilités et échéances.
- **Déclencheur :** question de l'utilisateur dans le chat de l'agent (agent Notion AI, activé manuellement).
- **Bases consultées :** *Master Tâches* (RACI, priorités, états, échéances).
- **Bases modifiées :** *Master Tâches* — il met à jour priorités et planification, en cohérence avec le planning.
- **Garde-fous fonctionnels :** il n'agit sur une tâche que si l'utilisateur apparaît dans son RACI (Créateur, Équipe, Personnel ressource ou Approbateur) ; il ne planifie pas le week-end ; il ne touche **jamais** aux propriétés techniques `Anti-Spam` et `*Référence n8n*` (réservées à n8n). Il distingue les tâches critiques (état *Problème*, échéance dépassée, priorité *Urgente* / *Élevée*).
- **Valeur opérationnelle :** transforme une demande floue en engagements datés et attribués, sans quitter Notion ; respecte le périmètre d'autorisation de chaque utilisateur (chacun ne pilote que ce qui le concerne).

### Le bibliothécaire — Mentor de la connaissance

- **Rôle :** mentor pédagogique. Il explique des sujets complexes de façon simple mais non édulcorée, en décomposant en étapes et en mettant en gras les idées clés, comme des notes de manuel.
- **Déclencheur :** question de l'utilisateur dans le chat de l'agent.
- **Bases consultées :** *Master Documentations Entreprise* (procédures, normes, formulaires, manuels).
- **Bases modifiées :** aucune — agent en lecture / explication.
- **Garde-fous fonctionnels :** répond en français ; compose avec la documentation interne (FR) et externe (EN) ; confirme avant tout changement sensible ou financier ; suit les instructions de l'utilisateur à la lettre.
- **Valeur opérationnelle :** sert de « second cerveau » documentaire — retrouver, résumer et pointer la bonne information (et la bonne version) sans parcourir manuellement la bibliothèque.

## Posture

Les agents IA s'appuient sur des prompts documentés dans le dépôt source. Conformément à la règle de confidentialité, **les prompts verbatim ne sont pas reproduits** dans ce dépôt : seule la logique fonctionnelle (rôle, déclencheur, bases, garde-fous) est décrite. Les agents contribuent à l'usage du SMQ ; ils ne constituent ni une preuve de conformité ni un mécanisme de contrôle qualité automatisé.

## Captures

Aucune capture spécifique aux agents IA ne figure dans l'inventaire (catégorie `agents-ia` vide dans le [MANIFEST](../screenshots/MANIFEST.md)). Les agents apparaissent en contexte dans certaines captures Front End — par exemple l'assistant de suivi des tâches dans l'espace *Focus* (voir la vidéo 2 référencée dans le [README](../README.md)).
