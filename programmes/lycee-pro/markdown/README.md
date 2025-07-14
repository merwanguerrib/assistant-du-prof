# Générer une mindmap HTML avec Markmap CLI

## Prérequis

- Node.js installé sur votre machine

## Installation de markmap-cli

```bash
npm install -g markmap-cli
```

## Générer un fichier HTML à partir d'un fichier Markdown

Placez-vous dans le dossier contenant votre fichier `.md` puis exécutez :

```bash
markmap <votre-fichier>.md
```

Cela va générer un fichier `<votre-fichier>.html` interactif.

## Astuce : auto-resize de la mindmap

Pour que la carte mentale s'adapte automatiquement à la taille de la fenêtre lors d'un clic sur un nœud, ajoutez le script suivant juste avant la balise `</body>` dans le fichier HTML généré :

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
