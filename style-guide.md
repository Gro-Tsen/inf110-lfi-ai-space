# Guide de style pour les notes de cours

## 1. Sources analysées et priorité entre les modèles

Le répertoire `modeles/` contient principalement deux documents :

- `notes-inf105.tex`, modèle plus ancien ;
- `notes-mitro206.tex`, modèle plus récent ;
- `vc`, petit script utilisé pour inscrire la version Git du document.

En cas de divergence, les conventions de `notes-mitro206.tex` doivent être privilégiées. Les deux fichiers sont cependant très proches dans leur conception générale : il s’agit de notes de cours longues, rédigées comme un texte mathématique continu, et non d’un simple développement linéaire des diapositives.

Les exemples ci-dessous sont principalement tirés de `notes-mitro206.tex`, avec mention des différences observables dans `notes-inf105.tex`.

---

## 2. Philosophie générale de rédaction

Le style est celui d’un cours oral transformé en texte écrit :

- partir d’une intuition ou d’un exemple concret ;
- expliquer progressivement les notions ;
- donner ensuite une définition formelle ;
- développer les conséquences et les exemples ;
- signaler les subtilités, abus de notation et cas particuliers ;
- renvoyer fréquemment à des notions introduites précédemment ou qui seront étudiées plus tard.

Le texte ne cherche pas à être excessivement abstrait. Même lorsqu’une définition formelle est donnée, elle est généralement précédée d’une motivation informelle.

Par exemple, dans `notes-mitro206.tex`, la notion de jeu est d’abord approchée de manière volontairement vague, par accumulation d’éléments caractéristiques : état, positions, joueurs, coups, hasard, gains, stratégies. Le texte précise ensuite que cette « définition » reste incomplète, notamment pour les jeux différentiels.

Il faut donc éviter :

- les définitions brutalement formelles sans motivation ;
- les enchaînements de résultats sans explication ;
- les introductions trop encyclopédiques ;
- les reformulations artificiellement condensées.

Le ton est pédagogique, direct et parfois légèrement personnel. Il est acceptable d’écrire par exemple :

- « On verra plus loin que… »
- « On peut se convaincre que… »
- « Il est facile de comprendre intuitivement que… »
- « Il faut cependant faire attention à… »
- « Cette question mérite l’attention. »
- « On ne développera pas… »
- « Dans ce cours, on s’intéressera surtout à… »

---

## 3. Structure générale d’un document

### 3.1. Préambule

Le préambule suit globalement cette organisation :

1. classe `article`, en 12 points, sur papier A4 ;
2. réglage des marges ;
3. langue française et encodage UTF-8 ;
4. polices et paquets mathématiques ;
5. outils graphiques ;
6. index et hyperliens ;
7. environnements de résultats mathématiques ;
8. macros spécialisées ;
9. `\makeindex` ;
10. titre, auteur, intitulé du cours ;
11. numéro de version Git ;
12. table des matières.

Dans le modèle récent, les choix sont notamment :

- `\usepackage[a4paper,margin=2.5cm]{geometry}` ;
- `\usepackage[french]{babel}` ;
- `\usepackage{lmodern}` ;
- `\usepackage{newtxtext}` ;
- `amsmath`, `amsfonts`, `amssymb`, `amsthm` ;
- `tikz` ;
- `hyperref` avec `hyperindex=false`.

Le modèle ancien utilise `francais`, `times` et des marges intérieures/extérieures différentes. Ces choix doivent être considérés comme historiques et non comme la convention à reproduire par défaut.

### 3.2. Titre

Le titre est court et descriptif. Il peut comporter un sous-titre entre parenthèses ou sur une seconde ligne.

Exemples :

- `Théories des jeux\\(notes de cours)`
- `THL (Théorie des langages)\\Notes de cours`

L’auteur indiqué est `David A. Madore`. Le code du cours apparaît ensuite séparément, centré et en gras :

- `CSC-4MI06-TP / MITRO206`
- `INF105`

Pour les nouvelles notes, conserver cette séparation entre le titre principal et le code du cours.

### 3.3. Version Git

Le document récent affiche une ligne du type `Git: ...`, générée par le script `vc`. Cette information est placée après le titre et le code du cours, en petits caractères.

Il faut conserver ce mécanisme lorsque le document final est destiné à être maintenu dans le dépôt. La commande utilisée dans le modèle est visible dans `notes-mitro206.tex` aux lignes 89–94.

### 3.4. Table des matières

La table des matières est placée au début du document, après les informations de version, et composée en petits caractères :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L106-L110
{\footnotesize
\tableofcontents
\par}
```

Elle est suivie d’un espacement vertical important avant le début du cours.

---

## 4. Hiérarchie des chapitres et sections

### 4.1. Sections

La structure principale utilise :

- `\section{...}` pour les grandes parties ;
- `\subsection{...}` pour les thèmes principaux à l’intérieur d’une partie ;
- exceptionnellement des sous-sections plus fines si elles sont nécessaires.

Les titres sont informatifs et relativement longs. Ils décrivent le contenu plutôt qu’un mot-clé isolé.

Exemples :

- `Introduction et typologie`
- `La notion de jeu mathématique : généralités`
- `Quelques types de jeux`
- `Quelques exemples en vrac`
- `Remarques`
- `Plan`

Le modèle ancien emploie parfois des titres regroupant plusieurs notions, par exemple :

- `Alphabets, mots et langages ; langages rationnels`
- `Concaténation de mots, préfixes, suffixes, facteurs, sous-mots`

Cette pratique reste appropriée lorsqu’elle permet de conserver la structure d’un chapitre sans multiplier les sous-sections.

### 4.2. Ponctuation des titres

Les titres ne se terminent généralement pas par un point.

Les deux-points peuvent être utilisés pour introduire une précision :

- `La notion de jeu mathématique : généralités`
- `Concaténation de mots, préfixes, suffixes, facteurs, sous-mots`

Il faut employer les espaces insécables dans les titres lorsque la typographie française l’exige.

### 4.3. Paragraphes numérotés

La plupart des paragraphes importants commencent par la macro `\thingy`. Celle-ci incrémente un compteur commun à chaque sous-section et produit un numéro en gras.

Dans le modèle récent :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L29-L33
\theoremstyle{definition}
\newtheorem{comcnt}{Tout}[subsection]
\newcommand\thingy{%
  \refstepcounter{comcnt}\smallskip\noindent\textbf{\thecomcnt.} }
```

Cette macro est utilisée pour les remarques, explications, exemples et énoncés informels. Elle ne correspond donc pas exclusivement à une catégorie mathématique particulière.

Le style de rédaction à privilégier est :

- un paragraphe autonome ;
- une numérotation implicite par `\thingy` ;
- un texte suivi, éventuellement suivi d’une liste, d’une formule ou d’un tableau ;
- une nouvelle unité numérotée lorsque l’on change de point important.

Exemple typique : le début d’une section de `notes-mitro206.tex` commence par plusieurs paragraphes `\thingy`, chacun développant un aspect distinct de la notion de jeu.

### 4.4. Transitions

Les sections comprennent fréquemment des transitions explicites :

- « Passons maintenant à une définition plus précise. »
- « Donnons quelques exemples. »
- « Cette question mérite l’attention. »
- « On peut résumer ceci de la façon suivante. »
- « Nous allons maintenant voir… »

Ces phrases sont utiles pour transformer une suite de diapositives en exposé continu. Elles doivent être conservées ou ajoutées lorsque le passage d’une idée à une autre serait autrement abrupt.

---

## 5. Définitions, résultats et exemples

## 5.1. Définitions informelles

Avant une définition formelle, commencer si possible par :

1. une motivation ;
2. un exemple ;
3. une reformulation en langage courant ;
4. la définition précise.

Le modèle introduit fréquemment les termes nouveaux avec `\defin{...}`. Cette commande met le terme en gras et l’inscrit dans l’index.

Exemples de formulations :

- « Une \defin{stratégie} d’un joueur est… »
- « On appelle \defin{état}… »
- « Un jeu est dit \defin{impartial} lorsque… »
- « On définit le langage \defin{miroir}… »

La première occurrence d’un terme technique doit normalement utiliser `\defin`. Les occurrences suivantes peuvent être composées normalement.

### 5.2. Définitions formelles

Les définitions importantes utilisent l’environnement `defn`, numéroté avec le compteur commun de la sous-section :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L34-L41
\newtheorem{defn}[comcnt]{Définition}
\newtheorem{prop}[comcnt]{Proposition}
\newtheorem{lem}[comcnt]{Lemme}
\newtheorem{thm}[comcnt]{Théorème}
\newtheorem{cor}[comcnt]{Corollaire}
\newtheorem{scho}[comcnt]{Scholie}
\newtheorem{algo}[comcnt]{Algorithme}
```

Cependant, il ne faut pas systématiquement transformer chaque définition en environnement `defn`. Le modèle emploie très souvent une définition intégrée dans un paragraphe `\thingy`, surtout pour les notions élémentaires.

Règle pratique :

- utiliser un paragraphe `\thingy` pour introduire une notion et l’expliquer ;
- utiliser `defn` lorsqu’il est important de disposer d’un énoncé formel autonome, réutilisable ou référencé ;
- ne pas créer artificiellement des environnements numérotés pour chaque phrase définitoire.

### 5.3. Propositions, lemmes, théorèmes et corollaires

Les énoncés mathématiques importants doivent être isolés et numérotés à l’aide des environnements disponibles :

- `prop` pour une proposition ;
- `lem` pour un lemme ;
- `thm` pour un théorème ;
- `cor` pour un corollaire ;
- `scho` pour une scholie ;
- `algo` pour un algorithme.

Le modèle n’utilise pas ces environnements comme de simples titres décoratifs. Ils doivent correspondre à une assertion mathématique clairement délimitée.

Les résultats doivent être annoncés ou motivés avant leur énoncé lorsque cela est possible. Après un résultat, il est fréquent d’ajouter :

- une explication en langage courant ;
- un exemple ;
- une remarque sur la portée du résultat ;
- un renvoi vers une preuve ou un résultat connexe.

### 5.4. Exemples

Les exemples sont généralement intégrés dans le texte par des formulations comme :

- « À titre d’exemple… »
- « Par exemple… »
- « Prenons… »
- « Considérons le jeu suivant… »
- « Donnons quelques exemples en vrac. »

Ils ne sont pas nécessairement placés dans un environnement `example`. Aucun environnement `example` n’apparaît dans le préambule des modèles.

Les exemples sont souvent développés assez longuement. Ils peuvent comprendre :

- une description informelle ;
- une formalisation ;
- une matrice de gains ;
- une formule ;
- une discussion intuitive ;
- un renvoi vers un résultat ultérieur.

Il ne faut donc pas réduire un exemple à une phrase si les diapositives suggèrent une analyse plus développée.

---

## 6. Style des preuves et démonstrations

### 6.1. Ton général

Les preuves sont rédigées en prose mathématique, avec des étapes explicitées. Le modèle évite les preuves purement télégraphiques.

Les formulations récurrentes comprennent :

- « Montrons que… »
- « Supposons que… »
- « Réciproquement… »
- « Il suffit de vérifier que… »
- « On obtient alors… »
- « Cela signifie précisément que… »
- « Par définition… »
- « En effet… »
- « D’où le résultat. »
- « Ceci achève la démonstration. »

La preuve peut commencer directement par un paragraphe explicatif plutôt que par un environnement formel.

### 6.2. Fin des preuves

Le symbole de fin de démonstration est un smiley, défini par :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L39-L41
\renewcommand{\qedsymbol}{\smiley}
```

Il faut donc employer les environnements de preuve de `amsthm` lorsque cela est approprié, afin que le symbole apparaisse automatiquement.

Le symbole ne doit pas être remplacé spontanément par un carré noir ou par une formule différente.

### 6.3. Preuves par contradiction

Le modèle emploie explicitement les formulations :

- « Supposons par l’absurde que… »
- « Si tel était le cas… »
- « Cela contredirait… »
- « On obtient une contradiction. »

L’argument doit rester lisible et ne pas être compressé en une seule ligne.

### 6.4. Preuves informelles

Certaines affirmations sont justifiées par une explication plutôt que par une preuve complète :

- « On peut se convaincre que… »
- « Il est facile de voir que… »
- « Il est assez facile de comprendre intuitivement… »
- « On pourra vérifier que… »

Ces formulations sont une composante réelle du style, mais elles ne doivent pas servir à masquer une difficulté essentielle. Lorsqu’un résultat est central ou subtil, il faut distinguer clairement :

- ce qui est démontré ;
- ce qui est seulement annoncé ;
- ce qui sera démontré plus tard ;
- ce qui est laissé comme exercice.

---

## 7. Organisation des explications

Le style alterne plusieurs niveaux de formalité.

### 7.1. Intuition puis formalisation

Séquence privilégiée :

1. description en français ;
2. exemple ;
3. définition ou formule ;
4. interprétation de la formule ;
5. conséquences.

Exemple représentatif dans `notes-inf105.tex` : la concaténation des mots est d’abord décrite comme le fait de « mettre bout à bout » les lettres de deux mots, puis définie formellement par une écriture avec des suites de lettres.

### 7.2. Reformulation

Après une définition formelle, reformuler souvent :

- « Autrement dit… »
- « En plus clair… »
- « Ce qui signifie… »
- « On peut traduire de façon savante cette propriété en disant que… »
- « Si on préfère… »

Cette pratique est particulièrement importante en première année.

### 7.3. Distinction entre notions proches

Le modèle insiste régulièrement sur les confusions possibles :

- une notion mathématique contre son analogue informatique ;
- deux objets qui ont des notations proches ;
- un langage vide contre le langage contenant le mot vide ;
- une propriété d’une classe contre une propriété d’un élément de cette classe.

Utiliser alors des formulations comme :

- « Il ne faut pas confondre… »
- « Il faut cependant distinguer… »
- « Attention : … »
- « Cette notation ne signifie pas… »
- « La différence est la suivante… »

Les passages d’avertissement peuvent être mis en évidence par `\emph{Attention}` ou `\emph{Attention !}`.

---

## 8. Formulations récurrentes

Les formulations suivantes sont caractéristiques et peuvent être reprises.

### Introduction d’une notion

- « On va commencer par définir… »
- « Le point de départ est donc… »
- « Une tentative pour approcher la notion de… »
- « Commençons par donner quelques exemples… »
- « Passons maintenant à une définition plus précise. »

### Définition

- « On appelle … »
- « On dira que … »
- « Un … est … »
- « On définit … par … »
- « Formellement, … »
- « Autrement dit, … »
- « Ce qui signifie exactement que … »

### Exemple

- « À titre d’exemple… »
- « Par exemple… »
- « Prenons le cas où… »
- « Considérons le jeu suivant… »
- « Donnons quelques exemples en vrac. »

### Conséquence

- « On en déduit que… »
- « Il s’ensuit que… »
- « Cela permet de voir que… »
- « On pourra donc… »
- « Cette observation sera utile plus loin. »

### Renvoi

- « cf. … »
- « voir … ci-dessous »
- « voir plus loin… »
- « comme on le verra en… »
- « en rappelant la définition donnée en… »
- « ce qui sera démontré en… »

### Restriction de portée

- « Dans ce cours, on ne considérera que… »
- « On s’intéressera surtout à… »
- « On ne développera pas… »
- « Nous négligerons parfois ce cas particulier. »
- « Cette distinction ne sera pas importante dans la suite. »

---

## 9. Références croisées et étiquettes

### 9.1. Principe général

Les notions et résultats importants reçoivent des `\label{...}` afin de pouvoir être rappelés ailleurs.

Les références sont faites avec `\ref{...}`, souvent précédé de `§` ou introduit par une formulation naturelle :

- `cf. §\ref{...}`
- `voir \ref{...}`
- `en \ref{...}`
- `cf. la définition donnée en \ref{...}`

Exemples observables :

- `cf. §\ref{subsection-introduction-and-words}`
- `cf. \ref{definition-best-response-and-nash-equilibrium}`
- `voir plus loin sur l’axiome de détermination`
- `en \ref{subsection-nim-sum}`

### 9.2. Convention de nommage des labels

Les labels sont en anglais, en minuscules, avec des mots séparés par des tirets :

- `intro-simultaneous-or-sequential`
- `rock-paper-scissors`
- `definition-best-response-and-nash-equilibrium`
- `introduction-graph-game`
- `number-of-words-of-length-n`

Il faut conserver cette convention, même dans un document rédigé en français, afin de rester cohérent avec les fichiers existants.

Les labels doivent être descriptifs et stables. Éviter les labels vagues comme `sec1`, `def2` ou `resultat`.

### 9.3. Références à une section

Pour une section ou une sous-section, employer volontiers :

- « la section \ref{...} »
- « la sous-section \ref{...} »
- « la partie \ref{...} »
- « cf. §\ref{...} »

La notation `§` est utilisée dans le modèle ancien et reste compatible avec le style général.

### 9.4. Éviter les numéros écrits en dur

Ne jamais écrire manuellement le numéro d’une définition, d’une section ou d’un théorème. Utiliser `\ref`.

---

## 10. Index

### 10.1. Commande `\defin`

La macro centrale est :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L77-L77
\newcommand{\defin}[2][]{\def\latexsucks{#1}\ifx\latexsucks\empty\index{#2}\else\index{\latexsucks}\fi\textbf{#2}}
```

Elle sert à la fois à :

- mettre le terme en gras ;
- l’inscrire dans l’index ;
- permettre un terme d’index différent grâce à l’argument optionnel.

Exemples :

- `\defin{stratégie}`
- `\defin[option]{options}`
- `\defin[impartial (jeu)]{partial/partisan ou impartial}`

### 10.2. Renvois dans l’index

Pour les synonymes ou variantes terminologiques, utiliser :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L216-L216
\index{partial (jeu)|see{partisan}}
```

Cette technique est utilisée pour regrouper les variantes sous une entrée principale.

### 10.3. Que mettre dans l’index

Indexer :

- les notions importantes ;
- les noms propres mathématiques ;
- les synonymes utiles ;
- les termes susceptibles d’être recherchés directement.

Ne pas indexer automatiquement chaque occurrence. Une entrée d’index correspond à une notion structurante, non à un simple mot courant.

### 10.4. Compilation de l’index

Le modèle récent indique la commande :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L18-L20
%% Self-note: compile index with:
%% texindy -C utf8 -L french notes-mitro206.idx
```

Cette convention doit être conservée pour les documents utilisant le même système.

---

## 11. Typographie française

### 11.1. Espaces insécables

Les espaces insécables sont utilisées avant :

- `:`
- `;`
- `!`
- `?`
- certains guillemets fermants ;
- les références précédées de `§` lorsque nécessaire.

Les modèles contiennent à la fois des espaces insécables Unicode et des espaces insécables LaTeX `~`. Le préambule déclare explicitement :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L55-L55
\DeclareUnicodeCharacter{00A0}{~}
```

Pour les nouvelles rédactions, employer de préférence `~` dans le code source lorsque cela rend la convention plus visible et plus robuste.

Exemples de formes à privilégier :

- `Attention !`
- `par exemple :`
- `cf. \ref{...}`
- `la section \ref{...}`
- `$x \in \Sigma$`

### 11.2. Guillemets

Les expressions françaises sont généralement entourées de guillemets français « … ».

Dans les fichiers modèles, les guillemets sont parfois directement présents sous forme Unicode. Il faut éviter les guillemets droits anglais pour du texte français, sauf lorsqu’ils font partie d’une chaîne de caractères ou d’une notation informatique.

### 11.3. Italique et gras

Utiliser :

- `\emph{...}` pour une mise en relief sémantique ;
- `\textbf{...}` pour les termes mis en évidence ou les mots importants ;
- `\textit{...}` pour certaines expressions étrangères ou conventions particulières.

Le gras est surtout pris en charge automatiquement par `\defin`. Il ne faut donc pas multiplier les `\textbf` sans raison.

L’italique sert notamment pour :

- les mots étrangers : `\textit{caveat programmator}` ;
- les avertissements ou oppositions ;
- les expressions que l’auteur veut faire ressortir.

### 11.4. Parenthèses et incises

Les parenthèses sont très fréquentes. Elles servent à ajouter :

- une précision ;
- une traduction informatique ;
- un cas particulier ;
- une remarque de portée limitée.

Les incises peuvent être assez longues, mais il faut éviter qu’elles rendent la phrase principale illisible. Lorsque la remarque devient substantielle, la déplacer dans un paragraphe séparé ou dans un passage en petits caractères.

---

## 12. Formules mathématiques

### 12.1. Formules dans le texte

Les expressions courtes sont placées entre `$...$`.

Les variables et objets mathématiques doivent rester en mode mathématique, y compris lorsqu’ils apparaissent dans une phrase française :

- `$x \in \Sigma$`
- `$L \subseteq \Sigma^*$`
- `$\varepsilon$`
- `$\frac{1}{2}$`

### 12.2. Formules affichées

Les formules importantes sont placées entre `\[...\]`, souvent avec `aligned` :

```tex name=notes-inf105.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-inf105.tex#L653-L657
\[
\begin{aligned}
L_1 L_2 &:= \{w_1 w_2 : w_1 \in L_1,\, w_2 \in L_2\}\\
 &= \{w \in \Sigma^* : \exists w_1 \in L_1\, \exists w_2 \in L_2\,(w = w_1 w_2)\}\\
\end{aligned}
\]
```

Les formules affichées ne sont généralement pas suivies d’un point ou d’une virgule placés après `\]`. La ponctuation est plutôt intégrée à la phrase qui introduit la formule, ou omise lorsque la formule forme un bloc autonome.

Cette règle est visible dans les exemples de définitions de `notes-inf105.tex`, notamment pour la concaténation et l’étoile de Kleene.

### 12.3. Alignement

Utiliser `aligned` lorsque plusieurs lignes appartiennent à une même définition ou transformation :

- alignement sur `=` ;
- alignement visuel simple ;
- pas de numérotation si aucune référence ultérieure n’est nécessaire.

Utiliser `equation` ou un environnement numéroté uniquement si la formule doit être référencée comme une équation autonome.

### 12.4. Ponctuation mathématique

Les virgules et ponctuations internes doivent rester en mode mathématique lorsque la formule l’exige :

- `\,` pour les petits espaces ;
- `\colon` dans les applications ;
- `\cdots` ou `\ldots` selon le contexte ;
- `\text{...}` seulement lorsque du texte apparaît véritablement dans une formule.

### 12.5. Notation

La notation doit suivre en priorité les diapositives source. Les modèles montrent toutefois plusieurs habitudes générales :

- `:=` pour une définition ;
- `\liff` et `\limp` pour les équivalences et implications ;
- `\mathbb{N}`, `\mathscr{P}`, etc. pour les ensembles usuels ;
- `\operatorname{...}` pour les opérateurs nommés ;
- `\mathtt{...}` pour les bits ou symboles informatiques ;
- `\texttt{...}` pour les chaînes de caractères ou exemples de code ;
- exposants en caractères romains lorsque l’exposant représente une opération, par exemple `w^{\textsf{R}}`.

---

## 13. Listes, tableaux et figures

### 13.1. Listes

Les listes utilisent principalement `itemize`, parfois sans phrase introductive particulière.

Elles servent notamment à :

- énumérer des cas ;
- donner les étapes d’une construction ;
- présenter plusieurs propriétés ;
- distinguer des variantes.

Chaque élément est généralement une phrase complète ou un groupe nominal suffisamment développé.

Les listes doivent être introduites par une phrase qui explique leur rôle :

- « Les constructions essentielles sont les suivantes : »
- « On distingue plusieurs cas : »
- « Quelques exemples sont : »

### 13.2. Tableaux

Les matrices de gains et comparaisons sont composées avec `tabular`, souvent dans un environnement `center`.

Le style est simple :

- pas de légende automatique ;
- première colonne et première ligne utilisées pour identifier les joueurs ou les options ;
- séparation des cases par `\hline` ;
- valeurs mathématiques entre `$...$`.

Exemples : les tableaux de pierre-papier-ciseaux, du dilemme du prisonnier et de la guerre des sexes dans `notes-mitro206.tex`.

### 13.3. Figures TikZ

Les figures sont intégrées directement dans le document avec `tikzpicture`.

Elles sont généralement :

- centrées ;
- placées dans un environnement `center` ;
- accompagnées d’une courte indication en petits caractères si nécessaire ;
- expliquées dans le texte avant ou après leur apparition.

Exemple de légende intégrée :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L758-L761
\end{tikzpicture}
\\{\footnotesize (Un état possible de Hackenbush.)}
\end{center}
```

---

## 14. Paragraphes et retour à la ligne

### 14.1. Une idée principale par paragraphe

Les paragraphes peuvent être assez longs, mais chacun doit développer une idée identifiable.

Le style n’est pas celui de petits paragraphes systématiquement séparés après chaque phrase. Il faut conserver des paragraphes continus lorsque les phrases forment une même explication.

### 14.2. Longueur des lignes source

Le modèle reformate généralement les lignes source à une longueur d’environ 70 à 80 caractères, avec des variations.

Il faut :

- insérer les retours à la ligne après des groupes syntaxiques naturels ;
- éviter les lignes extrêmement longues ;
- ne pas couper arbitrairement une formule ou une commande ;
- indenter les lignes continuées d’une formule ou d’une liste.

Les retours à la ligne du fichier source servent à la maintenance et à la lisibilité ; ils ne doivent pas être interprétés comme des changements de paragraphe.

### 14.3. Espacement vertical

Les modèles utilisent explicitement :

- `\smallskip`
- `\medskip`
- `\bigbreak`
- `\bigskip`

Ces commandes servent à rythmer le texte, notamment :

- avant ou après une remarque importante ;
- autour d’une transition ;
- avant une nouvelle grande partie ;
- entre des exemples indépendants.

Le modèle récent utilise `\smallskip` dans `\thingy`, alors que le modèle ancien utilise `\medskip`. La version récente doit être prioritaire.

---

## 15. Petits caractères, compléments et notes

Les passages secondaires sont fréquemment composés en `\footnotesize`.

Ils servent à donner :

- un cas limite ;
- une justification secondaire ;
- un commentaire historique ou terminologique ;
- une généralisation non nécessaire à la suite ;
- une preuve ou explication que le lecteur peut ignorer lors d’une première lecture.

Exemple de principe dans `notes-inf105.tex` : les remarques sur les alphabets vides, les propriétés universelles ou le dénombrement sont placées en petits caractères.

Ces passages doivent rester autonomes et être introduits comme des compléments. Il ne faut pas mettre en petits caractères une étape indispensable à la compréhension de la preuve principale.

Les formulations typiques sont :

- « Complément : … »
- « On peut par ailleurs montrer que… »
- « Cette remarque peut être ignorée en première lecture. »
- « Pour être tout à fait rigoureux… »
- « Le cas particulier suivant ne sera pas utilisé dans la suite… »

---

## 16. Exercices et corrigés

La macro `\exercice` fournit une numérotation commune avec les autres éléments :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L31-L33
\newcommand\exercice{%
  \refstepcounter{comcnt}\bigskip\noindent\textbf{Exercice~\thecomcnt.}\par\nobreak}
```

Les exercices doivent :

- être introduits par `\exercice` ;
- conserver leur formulation et leur notation lorsqu’ils proviennent du répertoire `exercices/` ;
- être séparés visuellement du texte courant ;
- recevoir un corrigé dans l’environnement `corrige` lorsque le corrigé est fourni.

Le modèle définit également :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L69-L75
\newif\ifcorrige
\corrigetrue
\newenvironment{corrige}%
{\ifcorrige\relax\else\setbox0=\vbox\bgroup\fi%
\smallbreak\noindent{\underbar{\textit{Corrigé.}}\quad}}
{{\hbox{}\nobreak\hfill\checkmark}%
\ifcorrige\relax\else\egroup\fi\par}
```

Ne pas réécrire ou moderniser inutilement ces commandes si le document d’ensemble les utilise déjà.

---

## 17. Points à vérifier et annotations

Les modèles ne fournissent pas de macro explicite `\review{...}` ou équivalente. Ils utilisent toutefois des formulations visibles telles que :

- « Attention ! »
- « Il faut cependant… »
- « Pour être tout à fait rigoureux… »
- « On ne développera pas… »
- « [et toute occurrence … sera probablement un lapsus …] »

Pour les futures notes produites avec l’aide d’une IA, il est recommandé d’utiliser une annotation clairement identifiable, par exemple `\review{...}`, si cette commande est ajoutée au préambule du document.

Ces annotations doivent être réservées aux cas où :

- la notation des slides est ambiguë ;
- une preuve est incomplète ;
- deux formulations sont contradictoires ;
- un résultat semble nécessiter une hypothèse supplémentaire ;
- la source ne permet pas de décider entre deux interprétations.

Il ne faut pas transformer silencieusement une ambiguïté en choix éditorial définitif.

---

## 18. Macros et commandes à préserver

Les macros existantes doivent être réutilisées plutôt que remplacées par des constructions ad hoc.

Macros particulièrement importantes :

- `\thingy`
- `\exercice`
- `\defin`
- `\limp`
- `\liff`
- `\spaceout`
- `\danger`
- `\corrige`
- les environnements `defn`, `prop`, `lem`, `thm`, `cor`, `scho`, `algo`.

Dans `notes-mitro206.tex`, des opérateurs spécifiques sont définis avec `\operatorname` :

```tex name=notes-mitro206.tex url=https://github.com/Gro-Tsen/inf110-lfi-ai-space/blob/main/modeles/notes-mitro206.tex#L43-L51
\newcommand{\outnb}{\operatorname{outnb}}
\newcommand{\downstr}{\operatorname{downstr}}
\newcommand{\precs}{\operatorname{precs}}
\newcommand{\mex}{\operatorname{mex}}
\newcommand{\id}{\operatorname{id}}
\newcommand{\limp}{\Longrightarrow}
\newcommand{\gr}{\operatorname{gr}}
\newcommand{\rk}{\operatorname{rk}}
\newcommand{\fuzzy}{\mathrel{\|}}
```

Pour un nouveau cours, il faut conserver les macros déjà présentes dans les slides ou les modèles, et n’en ajouter de nouvelles que si elles évitent une répétition réelle ou assurent une cohérence globale.

---

## 19. Niveau de détail attendu

Les notes doivent être plus développées que les slides, mais rester centrées sur leur contenu.

Il est souhaitable de développer :

- les définitions seulement esquissées ;
- les intuitions sous-jacentes ;
- les exemples ;
- les étapes intermédiaires des preuves ;
- les liens entre plusieurs diapositives ;
- les cas particuliers nécessaires à la compréhension ;
- les rappels de notation.

Il ne faut pas introduire sans signalement :

- un théorème substantiel absent des slides ;
- une nouvelle théorie ;
- une généralisation importante ;
- une preuve utilisant des outils non présentés ;
- une convention de notation qui change celle des slides.

Lorsqu’un développement est nécessaire mais non explicitement présent dans la source, le signaler comme un complément ou une annotation à vérifier.

---

## 20. Mention obligatoire concernant l’IA

Le document final doit contenir une mention explicite indiquant qu’il s’agit d’un premier brouillon produit avec l’aide d’un modèle d’IA et qu’une relecture par l’enseignant est indispensable.

Cette mention peut être placée dans les premières pages, à proximité du titre ou de la table des matières. Elle doit être clairement visible et ne pas être reléguée uniquement dans un commentaire LaTeX.

La formulation exacte n’est pas imposée par les modèles existants ; le contenu suivant est en revanche obligatoire :

- premier brouillon ;
- production avec l’aide d’un modèle d’IA ;
- nécessité d’une relecture et d’une vérification par l’enseignant.

---

## 21. Règles prioritaires en cas de choix éditorial

En cas d’hésitation, appliquer les priorités suivantes :

1. respecter la notation des slides source ;
2. respecter la terminologie déjà employée dans les slides ;
3. suivre `notes-mitro206.tex` plutôt que `notes-inf105.tex` ;
4. conserver les macros et environnements existants ;
5. privilégier une explication progressive à une définition trop abrupte ;
6. préférer un paragraphe `\thingy` à une multiplication d’environnements formels ;
7. donner les références croisées avec `\label` et `\ref` ;
8. utiliser une typographie française complète, notamment les espaces insécables ;
9. conserver des lignes source d’environ 70–80 caractères ;
10. signaler explicitement toute ambiguïté non résolue.

---

## 22. Règles qui ne peuvent pas être déterminées avec certitude

Les fichiers modèles permettent d’établir les conventions précédentes, mais certains points restent indéterminés.

### 22.1. Longueur exacte des lignes

Les lignes sont généralement proches de 70–80 caractères, mais aucune limite stricte n’est appliquée. Il s’agit d’une convention de lisibilité, non d’une contrainte mécanique.

### 22.2. Choix entre `\thingy` et les environnements formels

Les modèles utilisent les deux styles, sans règle entièrement explicite. Le choix dépend vraisemblablement de l’importance et de la réutilisabilité de l’énoncé.

### 22.3. Ponctuation des formules affichées

La tendance générale est de ne pas ajouter de ponctuation après `\]`, mais les modèles ne permettent pas d’en faire une règle absolue dans tous les contextes grammaticaux.

### 22.4. Forme exacte des annotations de vérification

Aucune commande dédiée n’existe dans les deux modèles. La commande `\review{...}` devra donc être introduite séparément si elle est retenue pour les notes produites par l’IA.

### 22.5. Usage systématique des petits caractères

Les modèles montrent une intention claire, mais ne donnent pas de critère formel pour décider quels compléments doivent être en `\footnotesize`. Il faut se baser sur le caractère facultatif du passage.

### 22.6. Compatibilité LaTeX moderne

Les modèles utilisent `inputenc` avec UTF-8, ce qui correspond à leur environnement de compilation historique. Il n’est pas possible de déduire des fichiers seuls s’il faut conserver exactement cette configuration dans un environnement LaTeX moderne. Pour éviter les problèmes, il vaut mieux préserver le préambule existant tant qu’aucune migration explicite n’est demandée.

---

## 23. Checklist pour les passes ultérieures

Avant de considérer une section comme rédigée, vérifier :

- la structure suit-elle celle des slides ?
- les termes et notations des slides ont-ils été conservés ?
- les notions nouvelles sont-elles motivées avant d’être formalisées ?
- les définitions importantes sont-elles repérables et indexées ?
- les résultats ont-ils le bon environnement (`prop`, `thm`, etc.) ?
- les preuves distinguent-elles clairement démonstration, intuition et annonce ?
- les références utilisent-elles `\label` et `\ref` ?
- les termes techniques utilisent-ils `\defin` à leur première occurrence ?
- les espaces insécables françaises sont-elles présentes ?
- les formules affichées sont-elles lisibles et correctement alignées ?
- les lignes du fichier restent-elles raisonnablement courtes ?
- les compléments facultatifs sont-ils distingués du texte principal ?
- les ambiguïtés sont-elles signalées plutôt que résolues silencieusement ?
- la mention obligatoire concernant le brouillon produit avec l’aide de l’IA est-elle présente ?
- le document compile-t-il avec les macros et environnements définis dans le préambule ?
