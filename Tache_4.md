> # ⬛ Working with branches

Les branches Git sont en fait un pointeur vers un instantané de vos modifications. Lorsque vous souhaitez ajouter une nouvelle fonctionnalité ou corriger un bug, quelle que soit sa taille, vous créez une nouvelle branche pour encapsuler vos modifications. Cela rend plus difficile la fusion du code instable dans la base de code principale et vous donne la possibilité de nettoyer l'historique de votre futur avant de le fusionner dans la branche principale.

![1](Images/2.svg){width=500 heigth=500}

## Comment ça fonctionne

Une branche représente une ligne de développement indépendante. Les branches servent d'abstraction pour le processus d'édition/étape/validation. Vous pouvez les considérer comme un moyen de demander un tout nouveau répertoire de travail, une zone de préparation et un historique de projet. Les nouveaux commits sont enregistrés dans l'historique de la branche actuelle, ce qui entraîne une bifurcation dans l'historique du projet.

La commande ``git branch`` vous permet de créer, lister, renommer et supprimer des branches. Il ne vous permet pas de basculer entre les branches ou de reconstituer un historique bifurqué. Pour cette raison, ``git branch`` est étroitement intégré aux commandes ``git checkout`` et ``git merge``.

