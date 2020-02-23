EXERCICE 1:  
1.Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur?  On utilise la commande printenv PATH. On obtient ceci : /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin  
2. Quelle variable d’environnement permet à la commandecdtapée sans argument de vous ramener dansvotre répertoire personnel?  On utilise la commande cd $HOME.  
3.Explicitez le rôle des variablesLANG,PWD,OLDPWD,SHELLet_.  
Lang :  Sert à afficher la langue utilisée par les logiciels pour communiquer avec l'utilisateur  
PWD:  Affiche le chemin absolu du répertoire courant  
OLDPWD:  Affiche le dernier répertoire visité avant un cd  
SHELL: Indique le shell utilisé par l'utilisateur connecté
_ : Renvoit la dernière commande saisie  
4.Créez une variable localeMY_VAR(le contenu n’a pas d’importance). Vérifiez que la variable existe.   Création : MY_VAR="truc". Vérification: echo MY_VAR. La dernière commande retourne "truc", preuve que la variable a bien été créée.  
5.Tapez ensuite la commandebash. Que fait-elle? La variableMY_VARexiste-t-elle? Expliquez. A la finde cette question, tapez la commande exitpour revenir dans votre session initiale.  La commande bash crée unnouveau shell. Par conséquent on peut pas accéder aux variables locale de notre ancien shell. c'est purquoi MY_VAR n'existe pas. On peut voir le niveau d'imbrication des shells avec la commande echo $SHLVL.  
6.Transformez MY_VARen une variable d’environnement et recommencez la question précédente. Expli-quez.   On utilise la commande export MY_VAR pour la transformer en variable d'environnment. La commande bash crée un nouveau shell mais MY_VAR est visble car les variable d'environnement sont héritées.  
7. Créer la variable d’environnementNOMSayant pour contenu vos noms de binômes séparés par un espace.Aﬀicher la valeur deNOMSpour vérifier que l’affectation est correcte.  Création  : NOMS = "GUEYE ROLLET" Vérification :  echo $NOMS  
8. Ecrivez une commande qui aﬀiche ”Bonjour à vous deux, binôme1 binôme2!” (où binôme1 et binôme2sont vos deux noms) en utilisant la variableNOMS.  On utilise  la ommande echo Bonjour à vous deux $NOMS   
9.Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commandeunset?   unset permet de supprimer un variable alors que donner une valeur vide à une variable ne la supprime pas, elle existera toujours.  
10.Utilisez la commandeechopour écrireexactementla phrase :$HOME =chemin(où chemin est votredossier personneld’après bash)   On utlise la commande echo '$HOME' = $HOME

EXERCICE 2: Vous enregistrerez vos scripts dans un dossierscriptque vous créerez dans votre répertoire personnel.Tous les scripts sont bien entendu àtester. Ajoutez le chemin versscript à votrePATH de manière permanente.

#!/bin/bash

PASSWORD="tp2"
read -s -p "Saisissez votre mot de passe" pwd
if [ $pwd=$PASSWORD ]; then
        echo -e "Mot de passe correct"
else
        echo -e "Mauvais mot de passe"
fi

EXERCICE 3 :
Ecrivez un script qui prend un paramètre et utilise la fonction is_number pour vérifier que ce paramètreest un nombre réel :

#!/bin/bash

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then 
  return 1
else
  return 0
fi
}
 if is_number $1 ; then
        echo -e "ok"
else
        echo -e "not ok"
fi

EXERCICE 4:
#!/bin/bash

if [ -z "$1"]; then
        echo -e "Utilisation : $(basename $0) nom_utilisateur";
//id renvoit l'ensemble des informations sur les utilisateurs. Si on lui on passe un nom un parametre, il renvoit un booleen. 0=n'existe pas  1=existe. La ligne suivante fait donc le test mais supprime les informatons normalement renvoyée par la commande id
elif id "$1" >/dev/null 2>&1 ; then
        echo -e "Utilisateur trouvé"
else
        echo -e "Utilisateur non existant"
fi

EXERCICE 5 :
Écrivez un programme qui calcule la factorielle d’un entier naturel passé en paramètre (on supposera quel’utilisateur saisit toujours un entier naturel).
#!/bin/bash

facto()
{
        n=$1
        if [ $n -eq 0 ] ;then
                echo 1
        else
                echo $((n*$facto $((n-1))))
        fi
}

echo "Le resultat est $(facto $1)"

EXERCICE 6:    Écrivez un script qui génère un nombre aléatoire entre 1 et 1000 et demande à l’utilisateur de le deviner.
Le programme écrira ”C’est plus !”, ”C’est moins !” ou ”Gagné !” selon les cas (vous utiliserez $RANDOM).

#!/bin/bash

MAXIMUM=1000
MINIMUM=1
WINNER=$((MINIMUM+RANDOM*(1+MAXIMUM-MINIMUM)/32767))
res=0
while [ $res -ne $WINNER ] ; do
        read -p "Entrez une valeur" res
        if [ $res -eq $WINNER ] ; then
                echo "Gagné!"
        elif [ $res -lt $WINNER ] ; then
                echo "C'est plus!"
        else
                echo "C'est moins!"
        fi
done

EXERCICE 7:1. Écrivez un script qui prend en paramètres trois entiers (entre -100 et +100) et affiche le min, le max
et la moyenne. Vous pouvez réutiliser la fonction de l’exercice 3 pour vous assurer que les paramètres
sont bien des entiers.
2. Généralisez le programme à un nombre quelconque de paramètres (pensez à SHIFT)
3. Modifiez votre programme pour que les notes ne soient plus données en paramètres, mais saisies et
stockées au fur et à mesure dans un tableau.

1/2. 
#!/bin/bash

function is_number()
{
 re='^[+-]?[0-9]+([.][0-9]+)?$'
 if ! [[ $1 =~ $re ]] ; then
  return 1
 else
  return 0
 fi
}

MAX=-100;
MIN=100;
MOY=0;
NBVAL=0;

while (("$#"));
do
        if is_number $1 ; then
                if [ $1 -lt $MIN ]; then
                        MIN=$1
                fi
                if [ $1 -gt $MAX ]; then
                        MAX=$1
                fi
                NBVAL=$(($NBVAL+1));
                MOY=$((MOY+$1));
        else
                echo "$1 n'est pas en entier"
        fi
        shift
done
MOY=$(($MOY/$NBVAL))
echo "MIN: $MIN / MOY: $MOY / MAX: $MAX";

3. 
#!/bin/bash

function is_number()
{
 re='^[+-]?[0-9]+([.][0-9]+)?$'
 if ! [[ $1 =~ $re ]] ; then
  return 1
 else
  return 0
 fi
}

GET=0;
MAX=-100;
MIN=100;
MOY=0;

TAB=();

while [ $GET -lt 101 ] && [ $GET -gt -101 ]
do
        read -p 'rentrez la note : ' GET

        if [ $GET -lt 101 ] && [ $GET -gt -101 ]; then
                if is_number $GET ; then

                        TSIZE=${#TAB[*]}
                        TAB[$TSIZE+1]=$GET

                        if [ $GET -lt $MIN ]; then
                                MIN=$GET
                        fi
                        if [ $GET -gt $MAX ]; then
                                MAX=$GET
                        fi

                        MOY=$(($MOY+$GET))
                else
                        echo "$GET n'est pas en entier"
                fi
        fi
done
TSIZE=${#TAB[*]}
echo "Generate Table ... ($TSIZE value(s))";
echo ${TAB[*]};
MOY=$(($MOY/$TSIZE))
echo "MIN: $MIN / MOY: $MOY / MAX: $MAX";
