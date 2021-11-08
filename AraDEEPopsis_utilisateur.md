# AraDEEPopsis

![Plantae | Getting to the Root of Plant Morphometrics, one DEEP Picture at a  Time | Plantae](https://plantae.org/wp-content/uploads/2020/11/tpc.20.00318-feature.png)



> araDEEPopsis: From images to phenotypic traits using deep transfer learning. Patrick Hüther, Niklas Schandry, Katharina Jandrasits, Ilja Bezrukov, Claude Becke - Gregor-Mendel-Institute - Vienne https://www.biorxiv.org/content/10.1101/2020.04.01.018192v2

## Préparation des images

La qualité de la prise d'image est déterminante pour obtenir une bonne analyse par Aradeepopsis.

Les photos des plantes doivent être prises systématiquement avec les même paramètres : hauteur de l'appareil, lumière, réglage de l'appareil...

Les résultats sont donnés en pixel. Pour obtenir les résultats en cm ou cm2 il faut connaitre la densité en pixel par cm de vos images. Les plus simple est de photographier un carré de taille connue (10 x 10 cm) dans les mêmes conditions que vos plantes. Vous pourrez alors définir le nombre de pixels par cm dans vos images et faire la conversion.

L’outil peut traiter un grande quantité d’image à la fois à la seule condition qu’il n’y ait qu’une seule plante par image. Tant que les plantes sont petites vous pouvez photographier le plateau entier puis découper chaque pot grâce à l'outil [graphicsmagik](./GraphicsMagick_utilisateur.pdf). Dès que les plantes deviennent trop grandes (cad qu'elles touchent les bords du pot) il faut prendre les photos une à une.

Les noms de vos photos apparaîtront dans le fichier de résultat. Afin de garantir un bon fonctionnement vous devez respecter les conditions suivantes pour le nommage de vos photos.

- Pas d'espaces
- Pas d'accent
- Pas de caractère spéciaux de type # ou @

Au moment de nommer vos photos pensez à la façon dont vous voudrez les grouper pour l'analyse et prenez garde à bien spécifier ces champs dans le nom et à les séparer tous par le même caractère (par exemple `_`) ce qui facilitera l'automatisation de la mise en forme de vos données pour une analyse dans R.

##Lancer l’analyse

Pour faire l'analyse :

- Ouvrir un terminal. L'affichage est le suivant :

```
pclinux@jitsi:~$
```

Cela signifie que vous êtes dans le HOME

- Forcer la mise à jour de Nextflow

Pour s'assurer d'utiliser toujours la dernière version de Nextflow, il faut supprimer le fichier caché `.nextflow` afin de forcer la mise à jour.

Taper les commandes suivantes :

```bash
ll -a
```

L’option `-a` permet de voir les fichiers cachés `.file`

Renommer le répertoire `.nextflow` en `.nextflow.old`

```bash
mv .nextflow .nextflow.old
```

Lors de l’exécution de la commande d’analyse, le téléchargement des mises à jour s’effectue, un nouveau répertoire `.nextflow` est créé.

Supprimer le répertoire `.nextflow.old`

```bash
rm .nextflow.old
```



- Lancer la commande 

Assurez vous que le prompt affiche toujours `pclinux@jitsi:~$`

Copier la commande suivante

```bash
nextflow run Gregor-Mendel-Institute/aradeepopsis --images '/Path/to/images/*.png' -profile docker --outdir /Path/to/outdirectory
```

Remplacer :

`'/Path/to/images/*.png'` par le chemin vers vos photos. SI vos images sont en `.jpg` remplacer `.png` par `.jpg` . 

:warning: Attention la commande est case sensitive

`/Path/to/outdirectory` par le chemin vers votre répertoire de résultat

## Résultat

1 fichier   `.csv`

Contient tous les paramètres mesurés : 

- Color channel quantification
- Morphometric traits

1 répertoire  `diagnostic`

Contient 4 répertoires de photos

- convex_hull
- crop
- mask
- overlay

Plusieurs rapports d’exécution

