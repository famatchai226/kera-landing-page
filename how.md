# Guide de Déploiement (GitHub & Cloudflare Pages)

Ce guide explique comment mettre à jour vos deux pages de destination hébergées sur **Cloudflare Pages**.

## 1. Kera Landing Page (`kera-landing-page`)
Pour mettre à jour la page **Kera** :

1. Ouvrez votre terminal dans le dossier : `c:\Users\hp\Antigravity& Stitch\kera-landing-page`
2. **Préparer les fichiers** : `git add .`
3. **Enregistrer les changements** : `git commit -m "Mise à jour : Migration vers Cloudflare"`
4. **Envoyer sur GitHub** : `git push origin main`

*Le déploiement sur Cloudflare Pages se lancera automatiquement après le push.*

---

## 2. Balta Landing Page (`balta-landing-page`)
Pour mettre à jour la page **Baltazar** :

1. Ouvrez votre terminal dans le dossier : `c:\Users\hp\Antigravity& Stitch\balta-landing-page`
2. **Préparer les fichiers** : `git add .`
3. **Enregistrer les changements** : `git commit -m "Mise à jour : Migration vers Cloudflare"`
4. **Envoyer sur GitHub** : `git push origin main`

*Le déploiement sur Cloudflare Pages se lancera automatiquement après le push.*

---

## 3. Visuels des cartes d'upsell (`#upsell`)

La section « Nos Offres Premium Exclusives » (`#upsell`, en bas de page) présente 2 offre(s) :
**Collection Premium Baltazar** · **Pack +14 838 BD & Mangas pour Adultes**.

Chaque carte affiche le visuel du produit en vignette carrée, à gauche du texte.

| Élément | Rôle |
| --- | --- |
| `.upsell-grid` | pile verticale des cartes (max 850 px, centrée) |
| `.upsell-card` | carte flex, fond `--surface-container-lowest`, bordure `--outline-variant`, rayon 1.75 rem, léger soulèvement au survol |
| `img.upsell-thumb` | visuel produit : 152 × 152 px, `object-fit: cover`, `object-position: center 20%` (les affiches sont en portrait), `loading="lazy"` + `decoding="async"` |
| `.upsell-body` | titre `h3`, description `p` et bouton de la carte |

- **Mobile (≤ 640 px)** : la carte passe en colonne et le visuel devient un bandeau
  `aspect-ratio: 16 / 9` sur toute la largeur de la carte.
- **Images distantes** : les visuels sont servis par les Workers frères, toujours en **URL
  absolue** (aucun visuel n'est embarqué dans ce dépôt) :
  - Collection Premium Baltazar : `https://balta.famatchai226.workers.dev/assets/hero%20caroussel/0.jpeg`
  - Pack +14 838 BD & Mangas pour Adultes : `https://bd.famatchai226.workers.dev/assets/hero%20caroussel/0.jpg`
- **Modifier / ajouter une carte** : dupliquer un bloc `.upsell-card`, changer
  `img.upsell-thumb` (attributs `src` et `alt`), les `data-i18n` et le lien du bouton, puis
  ajouter les clés `upsell.<produit>_title` / `_desc` / `_btn` dans **`locales/fr.json` et
  `locales/en.json`** (les deux fichiers, sinon la traduction retombe sur le texte du HTML).
- **Vérification** : ouvrir `index.html` et faire défiler jusqu'à « Nos Offres Premium
  Exclusives » ; les vignettes doivent s'afficher. Elles viennent d'un autre domaine : si le
  réseau ou le DNS bloque ce domaine, les cartes restent sans image alors que le texte est là.

---

## Notes Importantes
- **Analytics** : Cloudflare Web Analytics est prêt. Si vous avez un Token, insérez-le dans le fichier `index.html`. Sinon, activez "Web Analytics" dans votre tableau de bord Cloudflare pour un suivi automatique.
- **Domaines** : N'oubliez pas de configurer vos domaines personnalisés directement dans l'interface Cloudflare Pages si nécessaire.
- **Vercel** : Tous les fichiers liés à Vercel ont été supprimés pour alléger le projet.