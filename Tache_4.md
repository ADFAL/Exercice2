> # ⬛ Working with branches

Les branches Git sont en fait un pointeur vers un instantané de vos modifications. Lorsque vous souhaitez ajouter une nouvelle fonctionnalité ou corriger un bug, quelle que soit sa taille, vous créez une nouvelle branche pour encapsuler vos modifications. Cela rend plus difficile la fusion du code instable dans la base de code principale et vous donne la possibilité de nettoyer l'historique de votre futur avant de le fusionner dans la branche principale.

![1](Images/2.svg){width=500 heigth=500}

## Comment ça fonctionne

Une branche représente une ligne de développement indépendante. Les branches servent d'abstraction pour le processus d'édition/étape/validation. Vous pouvez les considérer comme un moyen de demander un tout nouveau répertoire de travail, une zone de préparation et un historique de projet. Les nouveaux commits sont enregistrés dans l'historique de la branche actuelle, ce qui entraîne une bifurcation dans l'historique du projet.

La commande ``git branch`` vous permet de créer, lister, renommer et supprimer des branches. Il ne vous permet pas de basculer entre les branches ou de reconstituer un historique bifurqué. Pour cette raison, ``git branch`` est étroitement intégré aux commandes ``git checkout`` et ``git merge``.


## Options communes

```bash
    git branch
```
Permet de répertorier toutes les branches de votre dépôt. Cette commande est synonyme de git ``branch --list``.
```bash
    git branch <branch>
```
Permet de créer une branche nommée ``＜branch＞``. Cette opération ne permet pas de faire un check-out de la nouvelle branche.
```bash
    git branch -d <branch>
```
Supprimez la branche spécifiée. Ceci est une opération « sûre » dans la mesure où Git vous empêche de supprimer la branche lorsqu'elle contient des changements non mergés.

```bash
    git branch -D <branch>
```
Forcez la suppression de la branche spécifiée, même lorsqu'elle contient des changements non mergés. C'est la commande à utiliser si vous souhaitez supprimer définitivement tous les commits associés à une ligne de développement spécifique.

```bash
    git branch -m <branch>
```
Permet de renommer la branche actuelle en ``＜branch＞``.
```bash
    git branch -a
```
Permet de répertorier toutes les branches distantes.


## Créer des branches

Il est important de comprendre que les branches sont juste des pointeurs vers des commits. Lorsque vous créez une branche, Git doit simplement créer un nouveau pointeur, il ne modifie le dépôt d'aucune manière. Donc, si vous commencez avec un dépôt qui ressemble à ceci :

![](Images/3.svg){width=500 height=300}

Ensuite, créez une branche avec la commande suivante :

```bash
    git branch crazy-experiment
```
L'historique du dépôt ne change pas. Vous obtenez simplement un nouveau pointeur vers le commit actuel :

![](Images/4.svg){width=500 height=300}

Remarque : cette commande permet uniquement de créer la branche. Pour y ajouter des commits, vous devez la sélectionner avec ``git checkout``, puis exécuter les commandes ``git add`` et ``git commit`` standard.


## Création de branches distantes

Jusqu'à présent, nos exemples illustraient tous des opérations sur une branche locale. La commande ``git branch`` fonctionne également sur les branches distantes. Afin d'utiliser des branches distantes, vous devez d'abord configurer un dépôt distant et l'ajouter à la configuration du dépôt local.

```bash
    $ git remote add new-remote-repo https://bitbucket.com/user/repo.git
    # Add remote repo to local repo config
    $ git push <new-remote-repo> crazy-experiment~
    # pushes the crazy-experiment branch to new-remote-repo
```

Cette commande fait un push d'une copie de la branche locale ``crazy-experiment`` vers le dépôt distant ``＜remote＞``.




## 🗑 Suppression de branches 

Lorsque vous avez terminé de travailler sur une branche et que vous l'avez mergée dans la base de code principale, vous pouvez la supprimer sans perdre l'historique :

```bash
    git branch -d crazy-experiment
```

Toutefois, si la branche n'a pas été mergée, la commande ci-dessus émettra un message d'erreur :

```bash
    error: The branch 'crazy-experiment' is not fully merged. If you are sure you want to delete it, run 'git branch -D crazy-experiment'.
```

Vous évitez ainsi de perdre votre accès à toute cette ligne de développement. Si vous souhaitez réellement supprimer la branche (p. ex., en cas d'expérience ratée), utilisez le flag ``-D`` en majuscules :

```bash
    git branch -D crazy-experiment
```

Cette opération supprime la branche, quel que soit son état, et sans avertissement. Par conséquent, utilisez-la avec précaution.

La commande précédente supprime une copie locale d'une branche. La branche peut continuer d'exister dans des dépôts distants. Pour supprimer une branche distante, exécutez la commande suivante

```bash
    git push origin --delete crazy-experiment
```
ou
```bash
    git push origin :crazy-experiment
```

Cette commande fait un push d'un signal de suppression vers le dépôt origin distant, ce qui déclenche la suppression de la branche ``crazy-experiment``.

