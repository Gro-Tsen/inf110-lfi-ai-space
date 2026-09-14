Ce dépôt Git a pour objet de travailler avec une IA pour convertir des
slides (“transparents”, “diapositives”) LaTeX en notes de cours pour
le cours “Logique et Fondements de l'Informatique” (“CSC-3TC34-TP” ou
“INF110”) de première année à Télécom Paris.

== Structure du dépôt ==

Les documents placés dans slides/ constituent la source principale du
contenu et de la structure : ce sont eux qu'il faut convertir en notes
de cours.  Les documents placés dans modeles/ constituent des exemples
de style, de typographie et de mise en forme à imiter.  Les documents
placés dans exercices/ seront à recopier verbatim, sauf modification
strictement nécessaire pour permettre la compilation ou l'intégration
au document d'ensemble.

Le fichier compilation/notes-inf110.tex est celui sur lequel pdfLaTeX
sera appelé.  C'est lui qui définit les packages inclus et les macros
disponibles.

Le fichier style-guide.md contient le guide de style à suivre généré
par IA à partir de l'analyse des fichiers de modèle (légèrement édité
par humain).

Les prompts des différentes passes déjà effectuées sont dans le
répertoire prompt/ et sont uniquement là à fin de conserver une trace
du workflow.

Le répertoire output/ contient les documents produits (finaux ou en
cours de relecture) principalement produits par l'IA.

== Instructions générales pour l'IA ==

Tu m'assistes dans la transformation des fichiers LaTeX de slides en
notes de cours (en français) pour des étudiants de première année de
Télécom Paris.

But d'ensemble : produire un document LaTeX de notes de cours dont le
contenu reprenne et développe les slides déjà écrites par
l'enseignant, en imitant le style des notes de cours proposés comme
modèle.

Objectifs précis :

* conserver essentiellement la structure et l'ordre des slides, ainsi
  que la terminologie et les notations de celles-ci ;

* conserver exactement (autant que possible) la notation mathématique
  des slides (ou, à défaut, des exercices et des modèles) ;

* développer les définitions, énoncés, explications et preuves déjà
  suggérées par les slides ;

* ajouter le contexte nécessaire à la compréhension ;

* ne pas introduire de résultats ou de développements substantiels
  absents des slides sans me le signaler explicitement ;

* imiter le style des documents décrit dans style-guide.md (qui
  présente le style des fichiers du répertoire modeles/) ;

* produire du LaTeX compilable ;

* écrire en français ;

* conserver les commandes et macros existantes lorsque c'est possible.

En cas d'ambiguïté mathématique, stylistique ou éditoriale, ne décide
pas silencieusement.  Signale le point à revoir dans une annotation
claire, en utilisant la commande \review{...}.

Chaque document final doit contenir une mention explicite indiquant
qu'il s'agit d'un premier brouillon produit avec l'aide d'un modèle
d'IA et qu'il doit être relu et vérifié par l'enseignant.
