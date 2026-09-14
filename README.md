# photo-identite

Prise de photo d'identite depuis le navigateur du telephone, avec grille de cadrage
en temps reel et controle automatique de conformite (format francais 35 x 45 mm,
regles ICAO 9303 / ANTS).

## Fonctionnement

Page statique, sans build ni serveur applicatif. Tout le traitement s'execute
dans le navigateur : aucune image n'est transmise.

- detection du visage : MediaPipe FaceLandmarker (478 points, blendshapes, pose 3D),
  charge depuis le CDN avec barre de progression reelle
- mesures geometriques projetees dans le repere de la tete, donc insensibles au roulis
- sommet du crane estime par le rapport anthropometrique trichion-vertex (0,24)
- 24 criteres controles : cadrage, pose, expression, regard, nettete, exposition, fond
- stabilisation des verdicts par mediane glissante sur 5 images et hysteresis de 18 %
- declenchement automatique apres 3 secondes de cadrage conforme
- export JPEG 413 x 531 px a 300 ppp, et planche PDF 10 x 15 de six vignettes

## Deploiement

Fichier unique `index.html`. HTTPS obligatoire pour l'acces camera.

## A calibrer

Les seuils photometriques (nettete, residu du plan de fond, saturation) sont des
valeurs plausibles, non calibrees sur un corpus de photos reellement acceptees ou
refusees en mairie.
