> # ⬛ Inspection 

## ▶ git status :

La commande ``git status`` affiche l'état du répertoire de travail et de la zone de transit. Il vous permet de voir quelles modifications ont été effectuées, lesquelles ne l’ont pas été et quels fichiers ne sont pas suivis par Git. La sortie d'état ne vous montre aucune information concernant l'historique du projet validé. Pour cela, vous devez utiliser ``git log``.

- git log
    - La commande ``git log`` affiche les instantanés validés. Il vous permet de répertorier l'historique du projet, de le filtrer et de rechercher des modifications spécifiques.

## Usage
```bash
    git status
```
Répertoriez les fichiers préparés, non préparés et non suivis.

## Discussion

La commande ``git status`` est une commande relativement simple. Cela vous montre simplement ce qui se passe avec ``git add`` et ``git commit``. Les messages d'état incluent également des instructions pertinentes pour la mise en attente/désactivation des fichiers. Un exemple de sortie montrant les trois catégories principales d'un appel « git status » est inclus ci-dessous :

```bash
    # On branch main
    # Changes to be committed:
    # (use "git reset HEAD <file>..." to unstage)
    #
    #modified: hello.py
    #
    # Changes not staged for commit:
    # (use "git add <file>..." to update what will be committed)
    # (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #modified: main.py
    #
    # Untracked files:
    # (use "git add <file>..." to include in what will be committed)
    #
    #hello.pyc
```

