Ce dépôt contient le code de développement du futur Vespéral dominicain basé sur l'Antiphonaire du R.P. Gillet op (1933), écrit en GABC et en LaTeX.

## Structure du projet

### Structure du code

Le fichier "chapeau" regroupant l'ensemble du projet est `VesperaleOP.tex`. Il assemble (via le module `subfiles`) un ensemble de fichiers de la forme `vop<numéro>_<partie>.tex`. Chacun de ces fichiers contient ensuite les titres des jours, les rubriques, les pièces de chant et les textes pertinents pour sa partie.

Le dossier `gabc` contient tous les fichiers GABC (antiennes avec, à la suite, l'incipit du psaume et l'euouae; hymnes; répons; etc.) Ces fichiers sont nommés par un code désignant leur emplacement liturgique (le "code Hudelmaier"), défini plus loin.

Le dossier `psalmi` contient les fichiers contenant le texte de chaque psaume et cantique, avec le pointage associé. Ces fichiers sont nommés `<numéro du psaume>_<mode>.gabc`, par exemple `109_1.gabc`, sachant que le mode peut être suivi d'une lettre si différents pointages existent dans le même mode.

### Nommage des fichiers GABC (code Hudelmaier)

La première partie du code désigne le jour liturgique.
* Pour le temporal et les fêtes mobiles, on indique d'abord la semaine de l'année:
  * A1 à A4 pour les semaines de l'Avent, 7G, 6G, 5G pour le temps de la Septuagésime, Q1 à Q6 pour le Carême et la Passion, P0 pour l'octave de Pâques, puis P1 à P7 jusqu'à la pentecôte, et H1 à H24 pour les semaines après la Pentecôte;
  * 08H1 pour la première semaine d'août, jusqu'à 11H5 pour la cinquième semaine de novembre;
  * puis on ajoute F1 pour le dimanche, F2 pour le lundi, jusqu'à F7 pour le samedi; ainsi A3F4 pour le mercredi des quatre-temps de l'Avent, 09H3F7 pour le samedi des quatre-temps de Septembre, P6F7 pour la vigile de Pentecôte.
* Pour les fêtes fixes, on indique le mois et le jour sur quatre chiffres : 1201 pour le 1er décembre, etc.
* Pour les communs, on abrège le nom du commun: APEX pour les apôtres hors du temps pascal, APTP pour les apôtres au temps pascal, UMEX pour un martyr hors du temps pascal, PMEX pour plusieurs, MRTP pour les martyrs au temps pascal, COPO pour les confesseurs pontifes, CONP pour les confesseurs non-pontifes, etc.
* Pour l'ordinaire, on indique OR

La deuxième partie du code désigne le genre de la pièce et son rang dans l'office: A1 à A5 pour les antiennes, AM pour l'antienne à Magnificat, H pour l'hymne, R pour le répons.

### Structure de l'ouvrage

Il n'est pas nécessaire que la numérotation des fichiers `vop<numéro>_<partie>.tex` soit continue, il est utile qu'elle soit ordonné, de sorte que les fichiers s'affichent (dans un explorateur de fichiers) dans l'ordre de l'ouvrage.

## Conventions GABC

### Caractères spéciaux

Dans le code GABC, il n'est pas rare de devoir insérer divers caractères spéciaux.

*`<sp>V/</sp>` : Symbole verset suivi d'un point (en conséquence, ne pas ajouter soi-même le point)
*`<sp>R/</sp>` : Symbole répons suivi d'un point
*`<sp>A/</sp>` : Symbole antienne suivi d'un point
*`<sp>*</sp>` : Astérisque d'incipit
*`<sp>+</sp>` : Obèle (croix fine à branche inférieure longue, pour les renvois)
*`<sp>crux</sp>` : Croix pattée indiquant les signes de croix de l'épaule à l'épaule
*`<sp>lcrux</sp>` : Croix latine indiquant les signes de croix sur une partie du corps

### En-têtes

Les en-têtes sont séparés du code GABC par un double pourcent `%%` et prennent la forme de couples `nom: valeur;`

L'en-tête `name` contient le nom de la pièce tel qu'il apparaît dans l'index, p.ex. `name: Alleluia (Feria V T.P.);`

L'en-tête `office-part` contient le genre de la pièce parmi les suivants: `office-part: Antiphona;`, `office-part: Responsorium Breve;`, `office-part: Responsorium;`, `office-part: Hymnus;`, `office-part: Toni Communes;`

L'en-tête `mode` contient le mode la pièce, en chiffres arabes de 1 à 8, avec sa differentia si c'est une antienne. Ainsi `mode: 1a;`, `mode: 1` (pour une pièce autre qu'une antienne), etc.

### Bonnes pratiques

La numérotation des strophes d'hymnes se fait après la double barre: `... por(e)ta.(d) (::) 2. Su(d)mens(hi) ...` 

L'incipit du psaume est précédé de `<i>Ps.</i>`, l'incipit du cantique, de `<i>Cant.</i>` (attention, encadrer la première voyelle d'accolades, pour centrer la note dessus: `<i>Cant.</i> M{a}g(f)ni(gh)...`)

L'euouae est encadrée par les balises `<eu>` : `<eu>E(h) u(h) o(g) u(f) a(gh) e.(gf) </eu>(::)` ce qui autorise gregorio à le comprimer plus que d'habitude, mais lui interdit de le séparer sur deux lignes, et supprime le guidon s'il est renvoyé de ce fait à la ligne suivante.


## Commandes LaTeX

### Commandes pour le pointage des psaumes

Chaque verset commence par `\item`

`\pscross{}` indique la flexe, il contient l'espace qui le sépare du texte: ainsi écrire `ómnia mandáta ejus,\pscross{} confirmata...`

`\psstar{}` indique la médiante, il contient l'espace qui le sépare du texte: ainsi écrire `...dómino meo:\psstar{} sede...`

`\sylchange{}` indique la première syllabe où la note change lors d'une cadence (a priori, il correspondra à du gras)

`\sylpass{}` indique une syllabe de passage (a priori, il correspondra à de l'italique)

### Commandes employées dans le corps de l'ouvrage

`\festum{jour}{titre}{sous-titre}{en_tete}{niveau_titre}`

Commande utilisée pour tous les titres qui modifient les en-têtes de pages (titres de sous-parties, titres de fêtes):

* jour : donné explicitement comme imprimé, p.ex. "Die 24 Junii"
* titre : pas en capitales : si on décide d'imprimer en capitales, le système fera la conversion. Cela préserve la possibilité de changer d'avis. p.ex. "in Nativitate S. Joannis Baptistæ"
* sous-titre : certains titres du Gillet ont une deuxième ligne imprimée moins gras. Cet argument est prépositionné au cas où on en a besoin pour reproduire ce genre de cas.
* en_tete : ce qu'on veut en tête de page à partir de la page sur laquelle commence cette fête. p.ex. "Die 24 Junii --- in Nativitate S. Joannis Bapt."
* niveau_titre : 0 pour les titres les plus grands (Proprium de Tempore), 1 pour les fêtes majeures avec un titre en pleine largeur, 2 ou 3 pour les titres plus petits.

`\cantus[annotation_mode]{nom_fichier}{annotation_emploi}`

Commande utilisée pour imprimer la plupart des pièces de chant.

* annotation_mode : optionnel. Désigne le texte imprimé immédiatement au-dessus de l'initiale de la pièce. S'il n'est pas indiqué, c'est le mode indiqué dans l'en-tête `mode` du GABC sera imprimé (en chiffres romains).
* `nom_fichier` : correspond au code Hudelmaier (voir plus haut) sans le `.gabc` de fin et sans la mention du sous-dossier `/gabc/`
* annotation_emploi : texte imprimé au-dessus de l'initiale, au-dessus de l'annotation de mode. Gillet l'emploie parfois pour numéroter les antiennes (1. Ant, 2. Ant...), parfois pour indiquer le genre (Hymnus), parfois rubricalement (T.Pasch., Super Ps.)

`\cantusparvus{nom_fichier}`

Commande utilisée pour imprimer une pièce de chant sans initiale, sans annotations initiales ("1 Ant.", "T. Pasch.", "1c", "Super Ps.", etc.), et sans indexation.

* `nom_fichier` : correspond au code Hudelmaier (voir plus haut) sans le `.gabc` de fin et sans la mention du sous-dossier `/gabc/`

`\psalmus[ton]{numero_psaume}`

Commande utilisée pour les psaumes.

* ton : argument optionnel indiquant le ton de pointage. Celui-ci est détecté automatiquement à partir de l'antienne précédente. On peut forcer le ton de pointage dans les sections où on imprime plusieurs psaumes pointés sans rapport avec une antienne.
* numero_psaume : le numéro, avec son suffixe pour les psaumes divisés (`144ii`) le cas échéant.

`\canticum[ton]{nom_fichier}{titre}{reference}`

Commande utilisée pour les cantiques (seul le Magnificat, aux Vêpres, mais pensée pour pouvoir gérer ceux des Laudes).

* ton : argument optionnel indiquant le ton de pointage. Celui-ci est détecté automatiquement à partir de l'antienne précédente. On peut forcer le ton de pointage dans les sections où on imprime plusieurs cantiques pointés sans rapport avec une antienne.
* nom_fichier : partie du nom de fichier qui identifie le cantique. Par exemple, si le fichier pour le cantique Benedicite en ton 1 se nomme `Dn3_1.tex`, cet argument doit être `{Dn3}`
* titre : titre imprimé du cantique, sans le mot "Canticum". Dans l'exemple précédent, `{Trium Puerorum}`.
* reference : référence biblique du cantique, imprimée à la manière d'une rubrique, sous le titre.

`\titulumrubrica{texte}`

Rubrique-titre employée avant divers tons d'une pièce pour indiquer quel ton est employé quand, p.ex. "In Adventu", "Per Annum", devant les divers tons du Te Lucis, etc.

`\rubrica{texte}`

Une rubrique qui n'est pas un titre.

`\titulum{texte}`

Petit titre intermédiaire, employé pour "Capitulum", "Psalmus N", etc. (inutile de l'employer en conjonction avec la commande `\psalmus` qui imprime déjà son titre.

`\versiculus{verset}{reponse}`

imprime le caractère V barré, le verset, le caractère R barré, la réponse.

`\oratio{texte}`

imprime le petit titre "Oratio" et le texte de l'oraison.

`\capitulum{ref}{texte}`

imprime le petit titre "Capitulum", la référence biblique "ref" (dessous, ou alignée à droite sur la même ligne comme Gillet le fait parfois), et le texte du capitule (on peut pointer le capitule et les oraisons avec le même système que les psaumes, sylprep sylac psstar pscross, si on fait un livre "pour les nuls"!)

### Raccourcis d'écriture

`\vvrub`, `\rrrub` et `\aarub` sont à employer à l'intérieur de rubriques et impriment les caractères V barré, R barré, A barré, en adoptant la couleur de la rubrique.

`\dominexaudiversiculus` imprime le V/&R/ Dómine exáudi...

`\dominusvobiscumversiculus` imprime le V/&R/ Dóminus vobíscum...

Caractères spéciaux à copier-coller si votre clavier ne les a pas : æ œ Æ Œ á é í ó ú ý ǽ œ́ Á É Í Ó Ú Ý Ǽ (pas de œ́ majuscule)

### Renvois

`\label{nom_label}` n'imprime rien, mais mémorise le numéro de la page en cours pour future référence, et l'asspcie au nom `nom_label`

Toutes les pièces sont labélisées par leur code Hudelmaier (nom de fichier sans le `.gabc`)

`\pageref{nom_label}` imprime le numéro de page de l'endroit où on a inséré `\label{nom_label}` (si `nom_label` est le code Hudelmaier d'une pièce, renvoie au début de la pièce)

\scorename{nom_fichier} imprime le nom de la pièce référencée par `nom_fichier` (tel qu'il figure dans les en-têtes GABC)

## Procédure d'emploi de Git

Une seule fois par ordinateur, quand un nouvel ordinateur rejoint le projet:

`git clone https://github.com/frfrancois/VesperaleOP`

Après un temps d'inactivité, rafraîchir le dossier:

`git fetch` pour télécharger l'état du dépôt GitHub sans toucher à ses fichiers locaux

`git rebase origin/main` pour mettre à jour ses fichiers à la dernière version du dépôt GitHub

Ou bien en une seule commande qui revient au même : `git pull --ff-only` (peut échouer si on avait oublié de pousser la dernière fois...)

Après avoir modifié des fichiers :

`git add .` pour inscrire toutes les modifications dans le prochain commit

ou bien `git add <dossier>/<fichier>` pour n'inscrire que certains fichiers, autant de fois que nécessaire

puis `git commit -m <description du commit>` pour créer un commit: un commit est un ensemble cohérent de modifications.

S'il reste des modifications non commitées, on recommence à `git add` jusqu'à avoir commité tout notre travail

`git fetch` pour télécharger l'état du dépôt GitHub au cas où quelqu'un a travaillé en même temps que nous et a poussé des changements

`git rebase origin/main` pour intégrer notre travail aux changements poussés précédemment par quelqu'un d'autre

`git push` pour pousser nos changements vers GitHub

Seules les commandes `git fetch` (ou `pull`) dans un sens, et `git push` dans l'autre, utilisent le réseau. Les autres sont purement locales.

On peut enfin utiliser `git add --interactive` et sélectionner `patch` pour que le système nous fasse passer en revue individuellement toutes les modifications faites à un fichier, si on veut les séparer en plusieurs commits.
