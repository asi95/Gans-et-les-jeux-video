---
layout: page
title: Amélioration du graphisme du jeu
---
 
Les réseaux génératifs adversaires (GAN) sont des algorithmes récents, les applications faites sont déjà très variées. Elles restent cependant du domaine de de la recherche et ne sont pas encore déployées dans l’industrie, en partie à cause de la difficulté à gérer des données complexes comme les images de haute résolution. Voici donc un éventail non exhaustif d’applications possibles des GANs. Dans cette partie, je vais vous parler de certaines applications dans les jeux vidéo.

## Transformer Fortnite en PUBG avec CycleGAN
Nous allons comprendre comment utiliser le CycleGAN, une variance de GAN, dans la traduction d’images et explorer son application aux graphiques des jeux.

![gan1](/Images/fortnite-gif1.gif/)

￼Si vous êtes un joueur, vous devez avoir entendu parler des deux jeux incroyablement populaires de Battle Royale, **Fortnite** et **PUBG**. Ce sont deux jeux très similaires dans lesquels 100 joueurs s'affrontent sur une petite île jusqu'à ce qu'il ne reste qu'un survivant. Si vous préférez le gameplay de Fortnite, mais vous préférez les images plus réalistes de **PUBG**. Cela a fait réfléchir des gens, ils se sont demandés s’ils peuvent avoir des modes graphiques pour les jeux qui leurs permettent de choisir les effets visuels de leur choix sans avoir à compter sur les développeurs de jeux pour leur fournir cette option. Et si un mode était disponible qui pourrait rendre les cadres de **Fortnite** dans les visuels de **PUBG**? Et oui, c’est possible, avec l’examen de différents réseaux de neurones et la découverte de **CycleGAN** qui sont très bons pour le transfert de style d’image, convertir visuellement **Fortnite** en **PUBG** est devenue une réalité. 

￼![gan1](/Images/fortnite2.jpeg/)

## Que sont les CycleGANs?
Les **[CycleGANs](https://arxiv.org/pdf/1703.10593.pdf)** sont un type de réseau d'adversaire génératif utilisé pour le transfert de style d'image entre domaines. Ils peuvent être formés pour convertir les images d'un domaine, comme **Fortnite**, en un autre, tel que **PUBG**. Cette tâche est effectuée de manière non supervisée, c'est-à-dire qu'il n'y a pas de mappage un-à-un des images de ces deux domaines.

￼![gan1](/Images/fortnite3.jpeg/)

Le réseau est capable de comprendre les objets dans les images du domaine d'origine et d'appliquer les transformations nécessaires pour correspondre à l'apparence du même objet dans les images du domaine cible. La mise en œuvre originale de cet algorithme a été conçue pour convertir les chevaux en zèbres, les pommes en oranges et les photos en peintures avec des résultats étonnants.

## Comment fonctionnent-ils?
 Essayons de comprendre le fonctionnement de **CycleGAN** en utilisant l'exemple de **Fortnite** en tant que domaine d'entrée et de **PUBG** en tant que domaine cible. À l'aide de nombreuses captures d'écran des deux jeux, nous formons une paire de réseaux d'adversaires génératifs, l'un apprenant le style visuel de Fortnite et l'autre de **PUBG**. Ces deux réseaux sont entraînés simultanément de manière cyclique pour apprendre à former des relations entre les mêmes objets dans les deux jeux et à effectuer ainsi les transformations visuelles appropriées. La figure suivante montre l'architecture générale de la configuration cyclique de ces deux réseaux.
 
![gan1](/Images/fortnite4.png/)
 
Nous commençons le processus de formation en prenant l’image originale de **Fortnite**. Nous allons former deux réseaux profonds, un générateur et un discriminateur. Le discriminateur apprendra au fil du temps à distinguer les images réelles des images factices de Fortnite. Le générateur sera entraîné à convertir l'image d'entrée du domaine d'origine en domaine cible à l'aide de captures d'écran aléatoires de **PUBG** à partir de l'ensemble d'apprentissage.
Afin de nous assurer que cette transformation est significative, nous imposons une condition de reconstruction. Cela signifie que nous formons simultanément un autre ensemble de générateur / discriminateur qui reconstruit l'image dans le domaine d'origine à partir du faux domaine. Nous imposons la condition selon laquelle cette reconstruction doit être similaire à l'image d'origine, ce qui nous donne une valeur de perte de cycle que nous cherchons à minimiser dans le processus de formation. Ceci est similaire aux auto-encodeurs, sauf que nous ne cherchons pas un encodage dans un espace latent pour l'étape intermédiaire, mais une image entière dans notre domaine cible.

![gan1](/Images/fortinte5.png/)

Le réseau de générateurs (F2P) utilisé ici est constitué de trois blocs de convolution majeurs. Le premier trouve un encodage d'une capture d'écran **Fortnite**  dans un espace latent de dimension inférieure. Ce codage est transformé en un codage qui représente **PUBG** dans le même espace latent. Le décodeur construit ensuite l'image de sortie à partir du codage transformé, nous donnant l'image de Fortnite qui ressemble à **PUBG**.
 
## Résultats 
 
Les images générées par **CycleGAN** après 12 heures d’entraînement semblent très prometteuses. Le réseau a pu convertir avec succès les couleurs du ciel, des arbres et de l’herbe de **Fortnite** à celles de **PUBG**. Les couleurs sursaturées de Fortnite ont été transformées en couleurs plus réalistes de **PUBG**. 
 
![gan1](/Images/fortnite-gif2.gif/)
 
 Le ciel a l'air moins bleuâtre et les verts caricaturaux de l'herbe et des arbres ressemblent beaucoup plus à ceux de **PUBG**. Il a même appris à remplacer le compteur de santé situé en bas de l'écran par le pistolet et l'indicateur de munitions de **PUBG**! Par contre l'apparence du joueur n'est pas bien apprise, c’est la raison pour laquelle les pixels qui l’entourent sont un peu flous. Dans l’ensemble, le réseau a réussi à identifier les objets dans les deux domaines et à transformer leur apparence.
 
#  Autre exemple : graphiques réalistes pour Grand Theft Auto 5
![gan1](/Images/gta1.png/)
 
Dans cet exemple, la même structure de **CycleGAN** est utilisée pour rendre le graphisme du fameux jeu **GTA5** plus réaliste. De même, des captures d’écran du jeu sont prises comme domaine source que nous souhaitons convertir en quelque chose de photo-réaliste. Le domaine cible provient du jeu de données cityscapes qui représente le monde réel (auquel nous souhaitons faire ressembler notre jeu). 

## Résultats :
![gan1](/Images/gtagif2.gif/)

Basé sur environ trois jours de formation sur environ 100 itérations, le modèle **CycleGAN** semble faire un très bon travail d’adaptation de **GTA** au domaine réel. J'aime beaucoup le fait que les petits détails ne soient pas perdus dans cette traduction et que l'image conserve sa netteté même avec une résolution aussi faible.
Le principal inconvénient est que ce réseau de neurones s'est révélé être assez matérialiste: il hallucine partout le logo **Mercedes**, ce qui gâche la conversion presque parfaite de **GTA** au monde réel. (C’est parce que le jeu de données **Cityscapes** a été collecté par un propriétaire de **Mercedes**.) 

![gan1](/Images/gta-figif1.gif/)

## Application aux modes graphiques dans les jeux :

Bien que les résultats semblent vraiment bons, il est clair que nous avons encore beaucoup de chemin à parcourir avant de pouvoir jouer à **Fortnite** avec des graphiques **PUBG** ou au **GTA** avec un graphisme réaliste. Mais une fois que nous serons en mesure de générer des images de résolution supérieure en temps réel à l’aide de ces réseaux, il deviendrait possible à l’avenir de créer des moteurs de modification graphique pour les jeux sans avoir à compter sur les développeurs. Nous pourrions utiliser le style visuel d'un jeu de notre choix et l'appliquer à n'importe quel autre jeu!





 
