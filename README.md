# 📚 Assistant du Prof – Voie Pro

Bienvenue sur le dépôt _Assistant du Prof_ ! Ce projet vise à faciliter l’accès aux programmes et à la génération de ressources pédagogiques pour la voie professionnelle (Histoire, Géographie, Lettres).

---

## 🗂️ Sommaire

- [1. Site statique – Hébergement des programmes officiels](#1-site-statique--hébergement-des-programmes-officiels)
- [2. Génération & publication de séquences pédagogiques](#2-génération--publication-de-séquences-pédagogiques)
- [Structure du projet](#structure-du-projet)
- [Publication & contribution](#publication--contribution)

---

## 1. 🌐 Site statique – Consultation des programmes officiels

Le site statique, publié via GitHub Pages, sert uniquement à rendre accessibles les programmes officiels de la voie professionnelle au format sous forme de mindmaps.

- **Accès direct** aux programmes officiels sous forme de mindmaps pour chaque matière et niveau.
- **Publication automatique** à chaque mise à jour sur la branche `main`.
- **URL publique** : https://merwanguerrib.github.io/assistant-du-prof/



---

## 2. 🧪 Génération & publication de séquences pédagogiques

Le projet intègre un workflow complet pour générer des séquences pédagogiques structurées à partir de prompts, puis les publier automatiquement dans une base Notion dédiée.

### **Étapes principales**

1. **Génération** :
   - Utiliser le prompt `assets/prompts/prompt_sequence.md` pour cadrer la génération.
   - Structurer la séquence selon le template markdown `assets/templates/sequence-template.md`.
2. **Conversion Notion** :
   - Mapper le markdown vers le format JSON Notion (`assets/templates/sequence-template.notion.json`).
   - Gérer les propriétés Notion (titre, classe, thème, durée, problématique, matière, etc.).
3. **Publication** :
   - Créer la page dans la base Notion « Séquences Pédagogiques » via l’API.
   - Ajouter l’icône 🧪 et une cover couleur unie après création.

👉 Pour le détail complet du workflow, voir [`docs/workflow-sequence-notion.md`](docs/workflow-sequence-notion.md).

---

## Structure du projet

### 📁 Arborescence simplifiée

```
assistant-du-prof/
  ├── assets/
  │   ├── sequences-exemples/
  │   ├── prompts/
  │   └── templates/
  ├── geo/
  │   ├── 1-Seconde/
  │   ├── 2-Premiere/
  │   └── 3-Terminale/
  ├── histoire/
  │   ├── 1-Seconde/
  │   ├── 2-Premiere/
  │   └── 3-Terminale/
  ├── lettres/
  ├── metacognition/
  ├── programmes/
  │   └── lycee-pro/
  │       ├── html/
  │       ├── markdown/
  │       └── pdf/
  ├── docs/
  └── index.html
```

---

## Publication & contribution

- Toute contribution est la bienvenue !
- Voir le guide dans `programmes/lycee-pro/markdown/README.md` pour générer ou modifier des cartes mentales.
- Pour toute suggestion ou amélioration, ouvrez une issue ou une PR.

---
