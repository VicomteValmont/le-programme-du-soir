# Audit de l'expérience utilisateur

État au 30 juillet 2026, catalogue de 1330 œuvres.

## Méthode

Mesures relevées en instrumentant l'application : rendu de chacun des 50 écrans avec un profil réaliste (25 titres au journal, une collection, des repères saisis), comptage des éléments interactifs, et reconstruction du graphe de navigation par parcours en largeur depuis l'accueil.

Ce n'est pas un avis de goût. Les chiffres ci-dessous sont reproductibles.

## Le constat chiffré

| Mesure | Valeur |
|---|---|
| Écrans | 50 |
| Actions distinctes | 119 |
| Éléments cliquables, tous écrans confondus | **1650** |
| Boutons sur l'écran d'accueil | **34** |
| Écrans situés à un seul clic de l'accueil | **31 sur 40** |
| Questions avant la première recommandation | **7 + 6** |
| Taille du mode d'emploi | 2500 signes, 12 sections |

## Problème 1 — L'architecture est plate

**31 des 40 écrans navigables sont au niveau 1.** Il n'y a pas de hiérarchie : il y a une liste. L'accueil n'est pas un point de départ, c'est un sommaire de 34 entrées où tout se vaut — « Composer la séance » a exactement le même poids visuel que « Éphémérides ».

Répartition des profondeurs :

| Profondeur | Écrans |
|---|---|
| Niveau 1 | 31 |
| Niveau 2 | 7 |
| Niveau 3 | 1 |

Un utilisateur ne peut pas se construire de modèle mental d'une application dont tout est au même endroit. Il ne retient pas 34 entrées ; il en utilise trois et ignore le reste, sans savoir ce qu'il rate.

## Problème 2 — Une seule question, dix-neuf portes

L'application répond à une question : *qu'est-ce que je regarde ce soir ?* Elle propose **dix-neuf chemins différents** pour y répondre, tous au même niveau.

| Porte | Ce qu'elle fait vraiment |
|---|---|
| Composer la séance | Questionnaire de 6 questions, puis 3 propositions |
| Surprends-moi, sans question | Tirage aléatoire filtré par le profil |
| Régler mon humeur au détail | Les mêmes axes, en curseurs pondérés |
| L'atelier | Les mêmes axes, en filtres cumulables |
| Lancer un cycle | Sélection thématique de 5 titres |
| Le palmarès | Filtre par récompense |
| Composer une soirée | Enchaînement de plusieurs titres |
| Soirée à deux | Fusion de deux profils |
| Le défi du soir | Contrainte imposée |
| J'ai tant de temps devant moi | Filtre par durée disponible |
| Décrire une ambiance | Filtre par mots-clés en texte libre |
| Double programme | Deux titres accordés |
| À l'aveugle | Un titre décrit sans son nom |
| Fils rouges | Motifs transversaux du catalogue |
| Kaléidoscope | Échantillon varié |
| Festival | Programmation sur plusieurs jours |
| Almanach | Un titre par semaine de l'année |
| Éphémérides | Titres liés à la date du jour |
| Suggestions d'après mes goûts | Recommandation dérivée du journal |

Ces dix-neuf portes s'appuient sur **le même catalogue et largement le même moteur**. Ce ne sont pas dix-neuf fonctionnalités : ce sont dix-neuf réglages d'une seule, exposés comme s'ils étaient de nature différente.

Le coût pour l'utilisateur est double : il doit choisir sa porte avant de savoir ce qu'il y a derrière, et il ne peut pas passer de l'une à l'autre sans revenir à l'accueil.

## Problème 3 — Des noms qui ne disent pas ce qu'ils font

Le vocabulaire est soigné, souvent joli, et fréquemment opaque. Un nom d'écran doit permettre de décider si on clique ; ici, il faut cliquer pour savoir.

| Nom actuel | Ce que c'est réellement | Piste |
|---|---|---|
| Tirer le fil | Naviguer de proche en proche entre titres voisins | *De fil en aiguille* |
| Six degrés | Trouver un chemin entre deux films | *Relier deux films* |
| Kaléidoscope | Douze titres très différents entre eux | *Au hasard, mais varié* |
| À l'aveugle | Un film décrit sans révéler son titre | *Sans le titre* |
| Fils rouges | Motifs qui traversent le catalogue | *Obsessions du catalogue* |
| Le sablier | Filtrer par temps disponible | *J'ai tant de temps* |
| Éphémérides | Films liés à la date du jour | *C'est arrivé un 30 juillet* |
| Almanach | Un film par semaine sur l'année | *Une année de cinéma* |
| L'atelier | Filtres avancés cumulables | *Recherche détaillée* |
| Le pointage | Noter en masse les films déjà vus | *J'ai vu ces films* |
| Le carnet de bord | Journal de visionnage commenté | *Mes notes* |
| Les visages | Index des acteurs | *Acteurs* |
| Double programme | Deux films qui vont ensemble | *Deux films d'affilée* |
| La bibliothèque | Films tirés de livres | *Adaptations de romans* |

Le cas le plus coûteux est **l'atelier** : c'est la fonctionnalité la plus puissante de l'application, et son nom ne le laisse pas deviner.

## Problème 4 — Le coût d'entrée

**Sept questions** pour créer un profil, puis **six questions** avant chaque séance. Treize écrans de questionnaire avant le premier titre proposé.

C'est défendable pour quelqu'un qui utilisera l'application pendant des années. C'est rédhibitoire pour quelqu'un qui l'ouvre pour la première fois et veut savoir en trente secondes si elle lui sert.

Rien ne permet aujourd'hui de voir une recommandation avant d'avoir tout renseigné, sauf « Surprends-moi » — qui est le vingtième bouton de la liste.

## Problème 5 — Des écrans qui écrasent

| Écran | Boutons |
|---|---|
| Le pointage | **437** |
| L'atelier | 263 |
| Explorer | 155 |
| La bibliothèque | 153 |
| Les visages | 129 |

437 éléments cliquables sur un seul écran n'est pas une interface, c'est un inventaire. Ces écrans ne sont pas mauvais dans leur intention — ils sont livrés sans pagination ni progressivité.

## Problème 6 — L'application a besoin d'un manuel

Un mode d'emploi de 2500 signes en 12 sections existe dans l'application. Sa présence est le symptôme, pas le problème : une interface qui doit être expliquée n'a pas été comprise avant d'être écrite.

## Ce qui doit être préservé

L'audit porte sur la forme. Le fond est solide et ne doit pas être emporté par la refonte.

**La base de données**, qui est le vrai actif : 1330 œuvres distinctes, 334 étiquettes cohérentes, 792 réalisateurs, 186 repères historiques, 107 œuvres primées classées en 19 familles, zéro doublon, zéro référence morte. Elle survit à n'importe quelle refonte de l'interface.

**Le moteur**, entièrement composé de fonctions pures et testées : `composer`, `empreinte_gouts`, `filtrer_avance`, `calculer_interdits`, `apprendre`. Il est indépendant de l'affichage — c'est ce qui rend la refonte possible sans tout réécrire.

**Le ton des textes**. Les pitchs et les repères historiques sont la personnalité du projet. Ce sont les *noms d'écrans* qui doivent devenir clairs, pas les contenus qui doivent devenir plats.

**L'absence de réseau et le fichier unique.** Deux contraintes qui ont façonné le projet et qu'il faut tenir.

## Proposition — cinq intentions au lieu de trente-quatre

Une architecture possible, à discuter et non à appliquer telle quelle :

**1. Ce soir** — la recommandation, en une seule porte avec des réglages progressifs. Absorbe : composer la séance, surprends-moi, humeur fine, défi, à l'aveugle, double programme, suggestion du moment, sablier, ambiance. On arrive sur une proposition immédiate ; on affine si on veut.

**2. Chercher** — le catalogue sous toutes ses entrées. Absorbe : explorer, atelier, palmarès, acteurs, bibliothèque, cycles, fils rouges, réalisateurs, auteurs.

**3. Ma liste** — ce que j'ai vu et ce que je veux voir. Absorbe : à voir, journal, collections, pointage, carnet.

**4. Mon profil** — qui je suis pour l'application. Absorbe : profil cinéma, statistiques, réglages, données, vérification du catalogue.

**5. Curiosités** — un tiroir assumé pour ce qui est joueur plutôt qu'utile : kaléidoscope, six degrés, almanach, éphémérides, festival, fil, comparateur. Ces fonctionnalités ne méritent pas d'être supprimées, seulement de ne plus concurrencer l'usage principal.

Le rapport passerait de 34 entrées à 5, sans rien perdre : les 34 deviennent des réglages ou des onglets à l'intérieur des 5.

## Ce que je ne recommande pas

**Ne pas supprimer les fonctionnalités joueuses.** Elles font la différence avec un moteur de recherche, et leur coût de maintenance est nul puisque le moteur est partagé. Le problème n'est pas qu'elles existent, c'est qu'elles sont au même niveau que l'usage principal.

**Ne pas toucher au moteur pendant la refonte.** Il est testé et pur ; le garder stable est ce qui permettra de vérifier qu'une refonte d'interface n'a rien cassé.

**Ne pas commencer par les noms.** Renommer 14 écrans sans changer l'architecture donnerait une liste de 34 entrées mieux libellées, ce qui reste une liste de 34 entrées.

## Ordre de travail suggéré

1. Trancher l'architecture cible — c'est une décision, pas une technique.
2. Réduire le coût d'entrée : une recommandation visible avant tout questionnaire.
3. Regrouper les dix-neuf portes de recommandation.
4. Renommer, une fois que les regroupements sont stables.
5. Traiter les écrans surchargés par la pagination.
