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
