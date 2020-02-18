Exercice 1:  
1. On utilise la commande printenv PATH. On obtient ceci : /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin  
2. On utilise la commande cd $HOME.  
3. Lang :  Sert à afficher la langue utilisée par les logiciels pour communiquer avec l'utilisateur  
PWD:  Affiche le chemin absolu du répertoire courant  
OLDPWD:  Affiche le dernier répertoire visité avant un cd  
SHELL: Indique le shell utilisé par l'utilisateur connecté
_ : Renvoit la dernière commande saisie  
4. Création : MY_VAR="truc". Vérification: echo MY_VAR. La dernière commande retourne "truc", preuve que la variable a bien été créée.  
5. la commande bash crée unnouveau shell. Par conséquent on peut pas accéder aux variables locale de notre ancien shell. c'est purquoi MY_VAR n'existe pas. On peut voir le niveau d'imbrication des shells avec la commande echo $SHLVL.  
6. On utilise la commande export MY_VAR pour la transformer en variable d'environnment. La commande bash crée un nouveau shell mais MY_VAR est visble car les variable d'environnement sont héritées.  
7. Création  : NOMS = "GUEYE ROLLET" Vérification :  echo $NOMS  
8. On utilise  la ommande echo Bonjour à vous deux $NOMS   
9. unset permet de supprimer un variable alors que donner une valeur vide à une variable ne la supprime pas, elle existera toujours.  
10. On utlise la commande echo '$HOME' = $HOME

EXERCICE 2:  
