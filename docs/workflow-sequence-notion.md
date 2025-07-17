# 📚 Workflow complet : Génération et Publication d’une Séquence Pédagogique dans Notion

---

## 1. **Génération de la séquence pédagogique (prompt_sequence.md)**

### **Point de départ**

- Utiliser le prompt `assets/prompts/prompt_sequence.md` pour cadrer la génération.
- Exiger de l’utilisateur :
  - Le tableau du programme officiel (niveau, thème, compétences, attendus…)
  - Les fiches thématiques détaillées (notions, activités, ressources, évaluations)
  - Les contraintes spécifiques éventuelles

### **Étapes de génération**

1. **Analyser le programme** pour identifier : niveau, thème, attendus, compétences.
2. **Étudier les fiches** pour extraire : notions, activités, ressources, évaluations.
3. **Structurer la séquence** : séances logiques, objectifs, activités, supports, évaluations, AP si possible.
4. **Inclure** : différenciation, projet final, justification pédagogique, ressources complémentaires.
5. **Format attendu** : markdown conforme au template fourni (`sequence-template.md`).

---

## 2. **Conversion du markdown vers le format Notion JSON**

### **Mapping**

- Utiliser le template `assets/templates/sequence-template.notion.json` comme référence de structure.
- Respecter :
  - Les types de blocks Notion (`heading_1`, `paragraph`, `bulleted_list_item`, `divider`, `table`, etc.)
  - Les propriétés de la base Notion (titre, classe, thème, durée, problématique, matière, numéro…)
  - Le mapping du tableau markdown → bloc `table` Notion (voir ci-dessous).

### **Exigences pour le bloc `table`**

- La clé `children` doit être **imbriquée dans la propriété `table`**.
- Chaque ligne (`table_row`) doit avoir **exactement le même nombre de cellules** que `table_width`.
- Les cellules vides doivent être présentes (exemple : `[{ "type": "text", "text": { "content": "" }, ... }]`).
- **Aucune clé `has_children`** dans le payload.

### **Exemple de structure JSON Notion**

```json
{
  "object": "block",
  "type": "table",
  "table": {
    "table_width": 7,
    "has_column_header": true,
    "has_row_header": false,
    "children": [
      {
        "object": "block",
        "type": "table_row",
        "table_row": {
          "cells": [
            [{ "type": "text", "text": { "content": "Titre de la séance" }, ... }],
            [{ "type": "text", "text": { "content": "Problématique / Question" }, ... }],
            // ... 5 autres cellules
          ]
        }
      },
      // ... autres lignes, toutes avec 7 cellules
    ]
  }
}
```

---

## 3. **Validation et correction du JSON**

### **Étapes de validation**

- **Vérifier la présence de la clé `children`** dans chaque bloc `table`.
- **Vérifier le nombre de cellules** dans chaque ligne du tableau.
- **Corriger les erreurs** signalées par l’API Notion (ex : “Number of cells in table row must match the table width of the parent table”).
- **Supprimer tout commentaire JSON** (non supporté).

---

## 4. **Publication dans Notion**

### **Création de la page**

- Utiliser l’API Notion (via MCP ou SDK officiel).
- Pour créer une **entrée dans une base de données Notion** :
  - Utiliser l’ID de la base (`database_id`), pas d’une page parent.
  - Exemple de payload :
    ```json
    {
      "parent": { "database_id": "..." },
      "properties": { ... },
      "children": [ ... ]
    }
    ```
- **Partager la base avec l’intégration** (dans Notion, bouton “Partager” > ajouter l’intégration/bot).

### **Gestion des erreurs**

- **Erreur 400** : souvent causée par un mauvais mapping du bloc `table` (voir plus haut).
- **Erreur 404** : l’ID de la base n’est pas accessible ou n’existe pas, ou l’intégration n’a pas les droits.

---

## 5. **Bonnes pratiques et points de vigilance**

- **Toujours valider la structure du JSON** avant envoi.
- **Respecter strictement le template Notion** (voir `sequence-template.notion.json`).
- **Documenter toute correction ou adaptation** dans le process.
- **Utiliser Sequential Thinking et Serena** pour analyser, corriger, et tracer les étapes du workflow.
- **Mettre à jour la documentation** à chaque évolution du template ou du process.

---

## 6. **Exemples de fichiers**

- **Markdown source** : `geo/3-Terminale/sequence1-acces-ressources.md`
- **JSON Notion généré** : `geo/3-Terminale/sequence1-acces-ressources.notion.json`
- **Template Notion** : `assets/templates/sequence-template.notion.json`
- **Prompt de génération** : `assets/prompts/prompt_sequence.md`

---

## 7. **Résumé du process (schéma)**

```mermaid
graph TD
    A[Prompt utilisateur (programme + fiches)] --> B[Génération séquence markdown]
    B --> C[Mapping markdown → JSON Notion]
    C --> D[Validation structure JSON]
    D --> E[Publication dans Notion (API MCP)]
    E --> F[Contrôle visuel et correctifs]
```

---

## 8. **Ressources utiles**

- [Documentation Notion API](https://developers.notion.com/reference/post-page)
- [Template Notion JSON du projet](../assets/templates/sequence-template.notion.json)
- [Prompt de génération séquence](../assets/prompts/prompt_sequence.md)

---

**Ce workflow garantit la conformité, la traçabilité et la robustesse de la génération et publication de séquences pédagogiques dans Notion.**
_Mise à jour à chaque évolution du template ou du process recommandée._
