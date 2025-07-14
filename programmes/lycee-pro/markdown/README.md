# 🧠 Générer une mindmap HTML avec Markmap CLI

Bienvenue ! Ce guide vous explique comment transformer vos fichiers Markdown en cartes mentales interactives et accessibles sur le web, en toute simplicité 🚀

## ⚡ Utilisation rapide de markmap-cli

Pour transformer un fichier Markdown en mindmap interactive HTML, utilise l’outil officiel [markmap-cli](https://markmap.js.org/docs/packages--markmap-cli#usage).

### ⚙️ Commande rapide sans installation

```bash
npx markmap-cli <votre-fichier>.md
```

### 🛠️ Options utiles

- `--no-open` : ne pas ouvrir le fichier après génération
- `-o <nom-fichier.html>` : spécifier le nom du fichier de sortie
- `--offline` : générer un HTML utilisable hors-ligne

### 📦 Exemples

```bash
npx markmap-cli programmes/lycee-pro/markdown/geo.md
npx markmap-cli programmes/lycee-pro/markdown/geo.md -o programmes/lycee-pro/html/geo.html --offline
```

Pour plus d’options et d’exemples, consulte la documentation officielle :
https://markmap.js.org/docs/packages--markmap-cli#usage

---

## 💡 Astuce : auto-resize de la mindmap

Pour que la carte mentale s'adapte automatiquement à la taille de la fenêtre lors d'un clic sur un nœud, ajoutez le script suivant juste avant la balise `</body>` dans le fichier HTML généré :

```html
<script>
  (function () {
    function autoFitOnNodeClick() {
      function clickFitButton() {
        const btn = document.querySelector(
          '.mm-toolbar-item[title="Fit window size"]'
        );
        if (btn) btn.click();
      }
      // Sélectionne tous les nœuds interactifs
      document.addEventListener('click', function (e) {
        const node = e.target.closest('g.markmap-node');
        if (node) {
          setTimeout(clickFitButton, 300);
        }
      });
    }
    // Attendre que la mindmap soit prête
    setTimeout(autoFitOnNodeClick, 1000);
  })();
</script>
```

Copiez ce bloc dans chaque fichier HTML généré pour une meilleure expérience utilisateur.

---

## 🏠 Ajouter un lien retour vers l'accueil

Pour faciliter la navigation, vous pouvez ajouter un lien vers la page d'accueil (`index.html`) dans chaque fichier HTML généré.

Ajoutez le bloc suivant **juste après l'ouverture de la balise `<body>`** :

```html
<a
  href="/index.html"
  style="position: absolute; left: 1rem; top: 1rem; z-index: 10; text-decoration: none; font-size: 1.2rem; background: #fff; border-radius: 9999px; padding: 0.3em 0.8em; box-shadow: 0 1px 4px #0001; border: 1px solid #eee; color: #222;"
  >🏠 Accueil</a
>
```

Cela permet à l'utilisateur de revenir facilement à la page principale depuis n'importe quelle mindmap.
