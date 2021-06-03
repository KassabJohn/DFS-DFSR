

**Rôle DFS/DFS-R**

![How to configure DFS Replication on Windows Server
2019](mediafolder/e895e676281a1b0a7204066e2d6ff1ec884fb765.png)

Nous allons mettre en application le DFS et le DFSR, le premier permet
aux utilisateurs l'accès aux données distribuées, le second assurera la
réplication entre les cibles.

Pour se faire, nous avons besoin de 2 serveurs :

On clone le 1^e^ serveur, on se rend dans le serveur cloné, on sysprep
la machine en mode OOBE et on la redémarre pour la rendre distincte du
1^e^ serveur

On modifie le nom de la machine et son adresse ip

![](mediafolder/29c6dad09bea6b7ba11603069be9be405925b112.png)

![](mediafolder/26b156148f3dd62ae604cbbc7be436c921bc8b12.png)

On installe le service ADDS sur le 1^e^ serveur rattaché au nom de
domaine CONTOSO

![](mediafolder/9666114af1b45b17c7cfe9fec409c64d65da5c3b.png)

On rafraichit dans l'adds

![](mediafolder/7f33dfdc5de654c0ff25934d3e63290c24cd2977.png)

Notre serveur s'est bien ajouté à l'Active Directory

On se rend dans le gestionnaire de rôles et fonctionnalités et on y
ajoute l'espace de noms DFS ainsi que la réplication DFS

![](mediafolder/3a98f4628f1c7ca362165b990d466deebfa94eb0.png)

Sur le serveur principal qui est pour moi SRV-WIN2019, je vais
lancer l'application « Gestion du système de fichiers distribués DFS »

Faites clic droit sur « Espace de noms » puis cliquez sur « Nouvel
espace de noms... ».

![](mediafolder/9e3345e48892d5de857a93c2c028b880c02cc011.png)

Entrez le nom du serveur qui hébergera l'espace de nom

![](mediafolder/1dd06e6cf64d55c76b443381486836595c14c097.png)

Puis cliquez sur « Modifier les paramètres ... »

Choisissez les paramètres qui vous conviennent. Pour ma part j'ai choisi
de laisser l'accès en lecture et écriture aux utilisateurs et un accès
total aux administrateurs.

![](mediafolder/d816f58aa89ba83f7ce5b2163c73ed063115b392.png)

Pour le type d'espace de nom à créer, on laisse les valeurs par défaut :

![](mediafolder/404df8b54c78e2f315beb2843adbaf435ecec12f.png)

Maintenant que l'espace de noms est opérationnel, nous devons ajouter
les dossiers de notre partage.

Clic droit sur notre espace de noms et Nouveau dossier...

![](mediafolder/92990eaa9090de79aef98d9a28d34589730c455f.png)

Clic droit sur réplication → Nouveau groupe de réplication

![](mediafolder/69170d10e2bd8ab835ec8854ed362d5947628b8e.png)

On choisit le groupe de réplication multi-usage

On lui définit un nom et son domaine :

![](mediafolder/f221e2f2bb8ef13ae9a8e7c51aa567bd992dbb9c.png)

On y ajoute les membres (serveurs) désirés en cliquant sur ajouter et en
spécifiant le nom exact de nos membres

![](mediafolder/e88cc50521046ce3a03010c7799f23ae44d96a91.png)

Comme sélection de topologie, on définit maille pleine :

![](mediafolder/9abbc37a5657c552c7a5d5ba6b44e4ac56e28898.png)

On définit la planification de la bande passante :

![](mediafolder/e8c8b14487a9d310042da34829d9c80ed9747a22.png)

En tant que membre principal, on choisit le serveur de son choix qui
fera office de membre principal

![](mediafolder/c6707e018a4fc42f8d62b2728ea1199f0e5e9bd4.png)

On ajoute un chemin d'accès local :

![](mediafolder/63d1a62b7c963c1b416a239090d33e3f449546bc.png)

On définit un chemin d'accès local de C:\\ pour les autres membres

![](mediafolder/1b6bafd95af6695ac39a572dd953a9ca46dd2783.png)

On confirme et on crée la réplication

Quelques secondes après tous les dossiers du partage commun dans
SRV-WIN2019 sont répliqués dans le dossier commun du serveur SRV-20192.

![](mediafolder/fae12aa24fcd62d957c1a91236355e6ceb36fba8.png)
