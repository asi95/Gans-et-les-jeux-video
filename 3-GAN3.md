---
layout: page
title:  Génération des niveaux de jeu 
---
La création de contenu dans les jeux vidéo est l’une des tâches les plus longues et les plus difficiles pour développer un produit de bonne qualité et produire un contenu intéressant fait souvent appel à des experts en conception. Le contenu d'un jeu vidéo appartient à deux catégories: le contenu fonctionnel est lié aux mécanismes du jeu, contrairement au contenu non fonctionnel, qui sert généralement à des fins esthétiques ou a un effet marginal sur le jeu du point de vue des actions du joueur. Mais un groupe de chercheurs italiens ont montré que les algorithmes **GANs**  permettant d'atteindre les niveaux de jeu vidéo souhaités par les utilisateurs peuvent automatiser des aspects de la conception de jeux. Nous allons parler de leur travail qui porté sur le fameux jeu **DOOM**.

![gan1](/Images/doom.png/)

**DOOM** est un jeu de tir à la première personne sorti en 1993 qui est considéré comme une étape importante dans l’histoire du jeu vidéo et qui a toujours une communauté active de joueurs. Il existe plusieurs collections de niveaux de **DOOM** disponibles gratuitement en ligne, comme le corpus de niveaux de jeu vidéo (**VGLC**), qui comprend les niveaux officiels de **DOOM** et de **DOOM2** représentés dans plusieurs formats, ainsi que les archives de jeux de rôle, un grand référentiel avec plus de 9 000 niveaux de **DOOM** créés  par la communauté.
Des chercheurs ont récemment formé avec succès des réseaux de neurones pour générer des cartes de niveaux pour Doom qui, selon [un article publié sur le serveur de pré-impression arXiv en avril](https://arxiv.org/pdf/1804.09154.pdf), "se sont révélés intéressants". Les travaux ont été effectués par des chercheurs de l'Université polytechnique de Milan et ont utilisé **Generative Adversarial Networks**, une innovation récente dans le domaine de l'apprentissage en profondeur. Le but ultime de cette technique est de réduire le temps nécessaire au développement de jeux en automatisant des parties de la conception de niveaux et en permettant, sans doute, à l’être humain de faire un travail plus créatif.
Les réseaux de neurones sont des algorithmes qui «*apprennent*» des modèles dans de grands ensembles de données, puis génèrent de nouvelles prédictions basées sur ce qu'ils ont appris. Les réseaux génératifs adversaires (**GAN**) fournissent un puissant modèle génératif et ont été utilisés pour générer des visages effrayants et même transformer des scènes d'hiver en scènes d'été. Le générateur est «*formé*» aux données d’entrée (dans ce cas, plus de 1 000 cartes **Doom**) et crée de nouveaux niveaux basés sur le modèle appris. L’objectif du générateur est de tromper le côté discriminateur de l’algorithme, qui est satisfait s’il croit qu’une carte **Doom** a été créée par une personne et non par un ordinateur.
Les chercheurs ont formé deux **GANs**: l'un ne contenait que des images de cartes Doom et l'autre, des images et des attributs tels que la taille, le nombre de pièces, etc. Un ensemble de données contenant plus de 1 000 niveaux Doom a été traité pour extraire les informations les plus vitales. Dans ce cas, des images décrivant les principales caractéristiques du niveau, telles que la zone praticable, la hauteur du sol et les objets, ainsi que les descriptions correspondantes. Le schéma suivant présente l’architecture de GAN utilisée

![gan1](/Images/wad.png/)

Selon l’auteur de l’article, comprendre les caractéristiques pertinentes et les plus appropriées des niveaux était le plus grand défi pour nous. Les niveaux de jeu vidéo ont des structures complexes et vous finissez par avoir un grand nombre de valeurs qui décrivent chaque niveau, le vrai défi étant de choisir celles qui fonctionnent le mieux avec le réseau de neurones. Voici quelques niveaux de **DOOM** générés par l’architecture ci-dessus après 36000 itérations :

![gan1](/Images/carte.png/)

Le modèle utilisé par les chercheurs de Milan est flexible. Supposons que vous souhaitiez modifier l'environnement généré par l'IA pour améliorer sa reproductibilité. Les auteurs ont expliqué qu’il était facile d’implémenter de tels changements, car la topologie du niveau reposait sur un modèle unique qui pouvait être adapté et intégré au réseau de manière simple et pratique. Selon le journal, cette approche pourrait éventuellement être appliquée à d'autres tâches, telles que la génération de sprites de personnages non jouables, de sorte que vous n'ayez pas à vous soucier des cinq mêmes citadins chaque fois que vous jouez à **Skyrim**.

# Autre exemple : Abuser les GANs pour créer un pixel art 8 bits:
Utilisons des modèles génératifs pour faire quelque chose d'un peu plus idiot: créez des illustrations pour des jeux vidéo 8 bits!

![gan1](/Images/gangan.png/)

L'idée est que si nous pouvions générer des captures d'écran de jeux vidéo imaginaires convaincants, nous pourrions copier et coller des morceaux d'art à partir de ces captures d'écran et les utiliser dans notre propre jeu vidéo de style rétro. Les jeux vidéo générés n’ayant jamais existé, ce ne serait même pas voler.
L'art du jeu vidéo à cette époque était très simple. Étant donné que la **NES** ne disposait que d'une petite quantité de mémoire, Les programmeurs ont dû utiliser de nombreuses astuces pour adapter le jeu à sa mémoire. Pour maximiser l'espace limité, les jeux utilisaient des graphiques basés sur des mosaïques, chaque écran du jeu ne comprenant que quelques mosaïques graphiques répétées (généralement 16 x 16 pixels).
Par exemple, l’écran de départ de ‘*The Legend of Zelda*’ se compose de seulement 8 mosaïques uniques:

![gan1](/Images/nes1.png/)
Voici les tuiles de la carte du jeu ‘*The Legend of Zelda*’:
![gan1](/Images/nes2.png/)

L’objectif est de créer une feuille de tuiles similaire pour le jeu. De ce fait, on ne se soucie pas vraiment de voir les captures d'écran du jeu qu’on génère avoir l'air complètement réalistes. Au lieu de cela, on cherche simplement les formes et les motifs que nous pouvons utiliser comme carreaux 16 x 16 dans notre jeu - des choses comme des pierres, de l’eau, des ponts, etc. On utilise ensuite ces carreaux pour construire des niveaux de jeu vidéo de style 8 bits. 

Voici à quoi ressemble un échantillon des données d’entraînement originales:

![gan1](/Images/nes3.png/)

Après plusieurs itérations d'entraînement, les images commencent à ressembler à des versions cauchemardesques des jeux Nintendo classiques:

![gan1](/Images/nesgif1.gif/)

Le niveau suivant du jeu **Castlevania** est généré en utilisant le **DCGAN** :

![gan1](/Images/nes4.png/)

Ensuite, ajoutons le personnage principal et quelques ennemis de **Castlevania** afin de voir à quoi ressemblerait ce niveau en action avec les éléments de menu ajoutés:

![gan1](/Images/nes5.png/)

Dans l’ensemble, ce travail nous rapproche d’un avenir où de grandes parties de la conception de jeux sont automatisées et où l’être humain gère les tâches les plus créatives.
