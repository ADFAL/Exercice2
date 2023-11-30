> # ⬛ Saving changes
Lorsque vous travaillez dans Git ou dans d'autres systèmes de contrôle de version, le concept de « sauvegarde » est un processus plus nuancé que la sauvegarde dans un traitement de texte ou d'autres applications d'édition de fichiers traditionnelles. L'expression logicielle traditionnelle de « sauvegarder » est synonyme du terme Git « s'engager ». Un commit est l’équivalent Git d’une « sauvegarde ». La sauvegarde traditionnelle doit être considérée comme une opération du système de fichiers utilisée pour écraser un fichier existant ou écrire un nouveau fichier. Alternativement, la validation Git est une opération qui agit sur une collection de fichiers et de répertoires.

## git add

La commande ``git add`` ajoute une modification dans le répertoire de travail à la zone de transit. Il indique à Git que vous souhaitez inclure les mises à jour d'un fichier particulier dans la prochaine validation. Cependant, ``git add`` n'affecte pas vraiment le référentiel de manière significative : les modifications ne sont réellement enregistrées que lorsque vous exécutez ``git commit``.

En conjonction avec ces commandes, vous aurez également besoin de ``git status`` pour afficher l'état du répertoire de travail et de la zone de transit.

## Options communes
```bash
    git add <file>
```
Stage all changes in `<file>` for the next commit.
```bash
    git add <directory>
```
Stage all changes in `<directory>` for the next commit.
```bash
    git add -p
```
Démarrez une session de préparation interactive qui vous permet de choisir des parties d'un fichier à ajouter à la prochaine validation. Cela vous présentera un certain nombre de modifications et vous demandera une commande. Utilisez ``y`` pour mettre en scène le morceau, ``n`` pour ignorer le morceau, ``s`` pour le diviser en morceaux plus petits, e pour éditer manuellement le morceau et ``q`` pour quitter.

## Examples
Lorsque vous démarrez un nouveau projet, ``git add`` remplit la même fonction que ``svn import``. Pour créer un commit initial du répertoire actuel, utilisez les deux commandes suivantes :
```bash
    git add .
    git commit
```
Une fois que votre projet est opérationnel, de nouveaux fichiers peuvent être ajoutés en passant le chemin vers ``git add`` :
```bash
    git add hello.py
    git commit
```
Les commandes ci-dessus peuvent également être utilisées pour enregistrer les modifications apportées aux fichiers existants. Encore une fois, Git ne fait pas de différence entre les modifications apportées aux nouveaux fichiers et les modifications apportées aux fichiers déjà ajoutés au référentiel.



## Git commit
La commande ``git commit`` capture un instantané des modifications actuellement en cours dans le projet. Les instantanés validés peuvent être considérés comme des versions ``sûres`` d'un projet : Git ne les modifiera jamais à moins que vous le lui demandiez explicitement.

Avant l'exécution de ``git commit``, la commande « git add » est utilisée pour promouvoir ou  ``mettre en scène`` les modifications du projet qui seront stockées dans un commit. Ces deux commandes ``git commit`` et ``git add`` sont deux des plus fréquemment utilisées.

## Options communes
```bash
    git commit
```
Validez l’instantané intermédiaire. Cela lancera un éditeur de texte vous invitant à saisir un message de validation. Après avoir saisi un message, enregistrez le fichier et fermez l'éditeur pour créer le commit réel.
```bash
    git commit -a
```
Validez un instantané de toutes les modifications apportées au répertoire de travail. Cela inclut uniquement les modifications apportées aux fichiers suivis (ceux qui ont été ajoutés avec ``git add`` à un moment donné de leur historique).
```bash
    git commit -m "commit message"
```
Une commande de raccourci qui crée immédiatement une validation avec un message de validation transmis. Par défaut, ``git commit`` ouvrira l'éditeur de texte configuré localement et demandera qu'un message de validation soit saisi. Passer l'option ``-m`` abandonnera l'invite de l'éditeur de texte au profit d'un message en ligne.
```bash
    git commit -am "commit message"
```
Une commande de raccourci utilisateur expérimenté qui combine les options`` -a`` et ``-m``. Cette combinaison crée immédiatement une validation de toutes les modifications effectuées et prend un message de validation en ligne.
```bash
    git commit --amend
```
Cette option ajoute un autre niveau de fonctionnalité à la commande commit. Passer cette option modifiera le dernier commit. Au lieu de créer une nouvelle validation, les modifications échelonnées seront ajoutées à la validation précédente. Cette commande ouvrira l'éditeur de texte configuré du système et vous invitera à modifier le message de validation précédemment spécifié.


## Git diff

La différence est une fonction qui prend deux ensembles de données d'entrée et génère les modifications entre eux. ``git diff`` est une commande Git multi-usage qui, une fois exécutée, exécute une fonction diff sur les sources de données Git. Ces sources de données peuvent être des commits, des branches, des fichiers et bien plus encore. Ce document discutera des invocations courantes de ``git diff`` et des différents modèles de flux de travail. La commande ``git diff`` est souvent utilisée avec ``git status`` et ``git log`` pour analyser l'état actuel d'un dépôt Git.

## Comparer tous les changements
Invoquer ``git diff`` sans chemin de fichier comparera les modifications dans l'ensemble du référentiel. Les exemples spécifiques aux fichiers ci-dessus peuvent être invoqués sans l'argument ``./path/to/file`` et ont les mêmes résultats de sortie dans tous les fichiers du dépôt local.

## Modifications depuis le dernier commit
Par défaut, ``git diff`` vous montrera toutes les modifications non validées depuis la dernière validation.
```bash
    git diff
```

## Comparaison des succursales
**Comparer deux branches**
Les branches sont comparées comme toutes les autres entrées de référence à ``git diff``

```bash
    git diff branch1..other-feature-branch
```
Cet exemple présente l'opérateur point. Les deux points dans cet exemple indiquent que l'entrée diff correspond aux extrémités des deux branches. Le même effet se produit si les points sont omis et qu’un espace est utilisé entre les branches. De plus, il existe un opérateur à trois points :
```bash
    git diff branch1...other-feature-branch
```
L'opérateur à trois points lance la comparaison en modifiant le premier paramètre d'entrée ``branch1``. Il transforme ``branch1`` en une référence de la validation d'ancêtre commun partagée entre les deux entrées de différence, l'ancêtre partagé de ``branch1`` et d'une autre branche de fonctionnalité. Le dernier paramètre d'entrée reste inchangé en tant que pointe de l'autre branche de fonctionnalité.

## Git ignore

Les fichiers ignorés sont généralement des artefacts de construction et des fichiers générés par la machine qui peuvent être dérivés de la source de votre référentiel ou qui ne devraient pas être validés.

## Git ignore les modèles

``.gitignore`` utilise des modèles de globalisation pour correspondre aux noms de fichiers. Vous pouvez construire vos motifs à l'aide de différents symboles :

|Modèle|Exemples de correspondances|Explication*|
|-|-|-|
|`**/logs`|`logs/debug.log`<br>`logs/monday/foo.bar`<br>`build/logs/debug.log`|Vous pouvez préfixer un modèle avec un double astérisque pour qu'il corresponde aux répertoires partout dans le dépôt.|
|
|`.log`|`debug.log`<br>`foo.log`<br>`.log`<br>`logs/debug.log`|Un astérisque est un caractère générique qui correspond à zéro caractère ou plus.|

