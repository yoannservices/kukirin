# Kukirin (Kuki City)

Jeu 3D de trottinette électrique en ville : livraisons, quêtes et garage.

**▶ Démo en ligne : [https://yoannservices.github.io/kukirin/](https://yoannservices.github.io/kukirin/)**

## Fonctionnalités

- Ville ouverte : livraisons de colis, pièces à ramasser, quêtes
- Téléphone en jeu : livraisons, carte, trottinettes
- Police : un feu grillé ou un excès de vitesse vu par une patrouille déclenche une poursuite ; 5 niveaux de recherche (plus de voitures, plus rapides, barrages) ; un policier peut descendre de sa voiture et t’arrêter si tu restes immobile 3 s
- Chutes : le pilote est éjecté dans la direction du choc, il faut revenir à pied relever la trottinette
- Garage : boutique, atelier, repos ; batterie à gérer
- Progression enregistrée automatiquement (`localStorage`)

## Commandes

| Touche | Action |
|---|---|
| Z S Q D (ou flèches) | Accélérer, freiner / reculer, tourner |
| Maj | Wheelie (accélérer pour monter jusqu’à 75°, freiner pour redescendre) ; courir quand on est à pied |
| Espace | Frein arrière : drift en virage, à tenir à l’accélérateur |
| E | Garage |
| T | Téléphone |
| C / M / Tab | Caméra / carte / quêtes et aide |
| Clic + glisser | Tourner la caméra autour de la trottinette (vue 3e personne) |
| Échap | Pause |

## Lancer en local

Aucune installation : ouvrez `index.html` dans un navigateur, ou servez le dossier :

```bash
python -m http.server 8000
```

puis allez sur http://localhost:8000 (dans le dossier `web/` de Mes Projets : http://localhost:8000/loisirs/kukirin/).

## Structure

- `index.html`, `style.css`
- `js/main.js` : le jeu

## À savoir

Fan game non officiel : les caractéristiques des trottinettes KUKIRIN sont ajustées pour le jeu.

## Technologies

HTML, CSS et JavaScript ; rendu 3D avec [Three.js](https://threejs.org/) r186 (chargé depuis un CDN par `assets/three-compat.js`). Sans étape de build.

---

Fait partie de [Mes Projets](https://yoannservices.github.io/) · [Portfolio](https://yoannservices.github.io/portfolio/) · par [@yoannservices](https://github.com/yoannservices)

## Fiche technique

Résumé de ce que fait le code, tenu à jour à chaque modification : le lire suffit pour vérifier une information sans relire tout le jeu.

- **Code** : un seul fichier `js/main.js` (script classique) + `assets/building-kit.js`, chargés par `three-compat.js`.
- **Trottinette du joueur** (`rebuildPlayer`) : le modèle procédural est purgé (pilote et compteur gardés) et remplacé par un vrai modèle :
  - toutes sauf la G6 : `tier-scooter.glb` (Niilo Poutanen, CC-BY), `fitGLB(1.3, π)`, échelle k = (front − rear) / 0,97 pour poser ses roues (z = +0,49 / −0,48) sur les cotes de `SCOOTER_DESIGNS` ;
  - G6 : `kukirin-g25.glb` (Kukirin G25 Pro, photogrammétrie d'un bloc, 8,9 Mo, chargé seulement quand la G6 est choisie), `fitGLB(1.3, 0)`, essieux mesurés aux points de contact au sol (y < 0,015, |x| < 0,06).
- **Compteur** (`seatDisplay`) : posé sur le haut du guidon du vrai modèle (point le plus haut près de l'axe, z moyen des points à moins de 3 cm), échelle 0,55.
- **Hélicoptère de police** (`makeHeli` puis `realHeli`) : `mh6-little-bird.glb` (42manako, CC-BY) sans ses disques de rotor plats (nœuds `helicopter.001` et `.002`), `fitGLB(9.9, 0)`, patins à y = −1. Rotors procéduraux animés gardés : mât au sommet du modèle, rotor de queue à (z min + 0,35).
- **PNJ** : voitures `assets/models/npc/*.glb`.
- **Caméras (C)** : `GAME.cam` 0 = troisième personne, 1 = vue pilote.
- **Sauvegarde** : `kukicity.v1`.

## Crédits des modèles 3D

Véhicules réels sous licence CC-BY (Sketchfab) : auteurs et licences dans `assets/models/CREDITS.md`.
