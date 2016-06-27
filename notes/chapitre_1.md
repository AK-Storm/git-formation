# Chapitre 1 : Démarrage rapide
## 1. Rudements de git
-- a revoir 
## 2. Configuration - outil config

   * Git donne trois niveaux de configuration :

        *   fichier /etc/gitconfig pour configurer git pour tous les utilisateurs et tous les repos
        ```
          git config --system attribut value
        ```
        * fichier ~/.gitconfig spécifique a votre utilisateur
        ```
          git config --global attribut value
        ```
        * fichier .git/config propre au repo courant
        ```
          git config attribut value
        ```
    * Chaque niveau surcharge le niveau précédent, donc les valeurs dans .git/config surchargent celles de /etc/gitconfig.

    * exemples :
       ```
         git config --global user.name "John Doe"
         git config --global user.email johndoe@example.com
         git config --global core.editor emacs
       ```
    * on peut lister l'ensemble des parametres de configuration par :
       ```
         git config --list
         // ou un seul parametre
         git config user.name
       ```

## 3.  Obtenir de l’aide
    * pour Obtenir de l'aide il y a les commandes suivants :
       ```
       git help <verb> // exemple git help config
       git <verb> --help
       man git-<verb>
       ```
    * aussi il y a  les canaux #git ou #github sur le serveur IRC Freenode (irc.freenode.net).
