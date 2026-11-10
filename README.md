# tirvel.com

Site statique de la chaîne Tirvel. Aucun outil de build : les fichiers sont servis tels quels.

- `index.html` : accueil.
- `golem/index.html` : liens de la vidéo 1 (Meshy, code). Adresse : tirvel.com/golem.
- `mentions-legales/index.html` : mentions légales.
- `CNAME` : domaine pour GitHub Pages.
- `fonts/` : Unbounded, réduite aux caractères utiles, licence OFL.

## Voir le site en local

Dans ce dossier : `python -m http.server 8765`, puis ouvrir http://127.0.0.1:8765/golem/.

## Hébergement : GitHub Pages

GitHub Pages est gratuit et le compte `tirvel` existe déjà. Le code des vidéos y sera aussi. Il n'y a donc aucun compte de plus à créer. Le certificat HTTPS est fourni et renouvelé seul. Cloudflare Pages ferait aussi bien, mais demande un compte Cloudflare en plus.

Limite : en offre gratuite, le dépôt du site doit être public.

## Mettre en ligne

### 1. Avant tout

1. Remplir l'éditeur dans `mentions-legales/index.html` (nom, ou nom et SIRET une fois la micro-entreprise créée).
2. Créer le dépôt public `tirvel/golem` et y pousser le prompt, le script et le projet Unity. Sinon le bouton « Voir le dépôt » mène à une page 404.
3. Dans le tableau de bord affilié Meshy (PromoteKit), déclarer le site `tirvel.com` comme propriété de promotion. Les conditions du programme (art. 2.2) l'exigent avant toute promotion.

### 2. Dépôt GitHub

Connecté au compte `tirvel` sur github.com :

1. New repository. Nom : `tirvel-site`. Visibilité : Public. Ne rien cocher (ni README, ni licence).
2. Dans ce dossier :
   - `git remote add origin https://github.com/tirvel/tirvel-site.git`
   - `git push -u origin main`

### 3. Vérifier le domaine sur GitHub (protège contre le détournement)

1. github.com → photo de profil → Settings → Pages → Add a domain → `tirvel.com`.
2. GitHub affiche un enregistrement TXT. Le créer chez Porkbun (étape 5, même écran), puis cliquer Verify.

### 4. Activer Pages

1. Dépôt `tirvel-site` → Settings → Pages.
2. Source : Deploy from a branch. Branche : `main`, dossier `/ (root)`. Save.
3. Custom domain : `tirvel.com`. Save. (Le fichier `CNAME` le contient déjà.)

### 5. DNS chez Porkbun

porkbun.com → Domain Management → tirvel.com → DNS.

À supprimer :

- l'enregistrement `A` de `tirvel.com` qui pointe vers le parking Porkbun (207.207.210.x) ;
- le `CNAME` de `www` vers `uixie.porkbun.com`.

Si l'option URL Forwarding est active sur le domaine, la désactiver.

À ajouter :

| Type | Hôte | Valeur |
|------|------|--------|
| A | (vide) | 185.199.108.153 |
| A | (vide) | 185.199.109.153 |
| A | (vide) | 185.199.110.153 |
| A | (vide) | 185.199.111.153 |
| AAAA | (vide) | 2606:50c0:8000::153 |
| AAAA | (vide) | 2606:50c0:8001::153 |
| AAAA | (vide) | 2606:50c0:8002::153 |
| AAAA | (vide) | 2606:50c0:8003::153 |
| CNAME | www | tirvel.github.io |

À garder tels quels : les `MX` (`fwd1.porkbun.com`, `fwd2.porkbun.com`) et le `TXT` SPF. Ils font marcher contact@tirvel.com.

### 6. HTTPS

1. Attendre que Settings → Pages affiche « DNS check successful ». Cela prend de quelques minutes à quelques heures.
2. Cocher Enforce HTTPS. Le certificat peut mettre jusqu'à une heure à arriver ; la case reste grisée d'ici là.

### 7. Contrôle

- https://tirvel.com/golem/ s'affiche, avec le cadenas.
- http://tirvel.com/golem et https://www.tirvel.com/golem renvoient vers https://tirvel.com/golem/.
- Les boutons Meshy et GitHub mènent au bon endroit.
- Un mail envoyé à contact@tirvel.com arrive toujours.

Ensuite seulement, mettre `https://tirvel.com/golem` dans la description de la vidéo.

## Ajouter une vidéo

Copier `golem/` sous un nouveau nom, changer les textes et les liens, puis ajouter une ligne dans la liste de `index.html`.
