# rgastald.github.io

Site web personnel de recherche — HTML/CSS statique, sans générateur ni étape de build.
Publié par GitHub Pages à l'adresse <https://rgastald.github.io/>.

## Aperçu local

```bash
python3 -m http.server 8000 --directory ~/rgastald.github.io
```

Puis ouvrir <http://localhost:8000/>. (Il faut passer par un serveur, et non par
`file://`, parce que les chemins des feuilles de style sont absolus.)

## Structure

```
index.html              Accueil : barre latérale + « About » et « Research »
cv/index.html           CV : expérience de recherche, formation, compétences
teaching/index.html     Enseignement
publications/index.html Prépublications et articles
events/index.html       Exposés
assets/css/main.css     Toute la mise en forme (thèmes clair/sombre inclus)
assets/js/theme.js      Bouton de bascule clair/sombre
assets/img/portrait.jpg Photo de profil (carré, 480x480)
assets/files/cv.pdf     CV téléchargeable
.nojekyll               Désactive Jekyll sur GitHub Pages (site purement statique)
```

Le menu de navigation et le pied de page sont recopiés à l'identique dans les cinq
pages : si vous ajoutez une page, pensez à ajouter son entrée dans les cinq fichiers.

## Mises à jour courantes

**Remplacer la photo.** Écraser `assets/img/portrait.jpg` par une autre image
**carrée** (le CSS l'affiche dans un cadre 1:1 avec `object-fit: cover`, donc une
image non carrée serait rognée en son centre). 480x480 suffit : la photo est
affichée à 240 px, ce qui laisse la marge nécessaire aux écrans haute densité.

**Mettre à jour le CV PDF.**

```bash
cp ~/CV/cv_r_gastaldello.pdf ~/rgastald.github.io/assets/files/cv.pdf
```

**Ajouter une publication.** Dans `publications/index.html`, copier un bloc
`<li class="publications__item">` :

```html
<li class="publications__item">
  <p class="publications__title">Titre de l'article</p>
  <p class="publications__authors"><span class="publications__me">R. Gastaldello</span>, G. Stoltz</p>
  <p class="publications__venue">Journal, volume, année</p>
  <p class="publications__links">
    <a href="https://arxiv.org/abs/XXXX.XXXXX">arXiv:XXXX.XXXXX</a>
    <a href="https://doi.org/...">DOI</a>
  </p>
</li>
```

`publications__me` met votre nom en évidence dans la liste des auteurs.

**Ajouter un exposé, un cours ou une ligne de CV.** Toutes ces pages utilisent le
même bloc daté :

```html
<div class="entry">
  <div class="entry__date">Mon 2026</div>
  <div class="entry__body">
    <p class="entry__title">Titre</p>
    <p class="entry__sub">Sous-titre en italique (lieu, institution)</p>
    <p class="entry__quote">« Titre de mémoire ou de thèse »</p>
    <p class="entry__note">Ligne de détail (répétable)</p>
  </div>
</div>
```

Toutes les lignes sauf `entry__date` sont facultatives. La page `events/index.html`
contient un modèle en commentaire pour créer une section *Posters* ou
*Summer schools*.

**Modifier les textes de recherche.** Ils sont dans `index.html`, sous
`<h2 id="research">`, un `<h3>` par axe.

## Publication sur GitHub Pages

1. Créer sur GitHub un dépôt **public** nommé exactement `rgastald.github.io`
   (sans README ni .gitignore initial).
2. Pousser ce dépôt :

   ```bash
   git -C ~/rgastald.github.io push -u origin main
   ```

   Le remote `origin` est déjà configuré en HTTPS (le port SSH 22 est bloqué
   depuis le réseau de l'école).

3. Dans *Settings → Pages*, choisir **Deploy from a branch**, branche `main`,
   dossier `/ (root)`. Le site est en ligne au bout d'une minute environ.

Chaque `git push` ultérieur redéploie le site automatiquement.
