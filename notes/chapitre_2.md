# Chapitre 2 : Les bases de Git
## 1.  Démarrer un dépôt Git
      * pour initialiser/creer un repo dans directory il suffit d'utilser la commande init apres avoir se positionner sur ce repertoire
        ce qui va creer un directory .git
        ```
          git init  
        ```
      * pour cloner un repo (equivalent de checkout sur subversion)
        ```
          git clone url [dest_name] ## on peut changer la nom de repertoire de reception
        ```
## 2.  Vérifier l'état des fichiers

      * tracked files : are files that were in the last snapshot, or staged. ( unmodified, modified, or staged. )
      * untracked files : are files that not were in the last snapshot and not staged.
      * git add <file|directory> ,if the add command take a directory in parameter it will add recursively all his files/directories
      * a particular case : is to stage a file then modify it, it will appear staged and unstaged because there are some modification
        that are staged and other not
        ```
        $ git status
          On branch master
          Your branch is up-to-date with 'origin/master'.
          Changes to be committed:
            (use "git reset HEAD <file>..." to unstage)

              new file:   README
              modified:   CONTRIBUTING.md

          Changes not staged for commit:
            (use "git add <file>..." to update what will be committed)
            (use "git checkout -- <file>..." to discard changes in working directory)

              modified:   CONTRIBUTING.md
        ```
       * git status -s or --short : there are two columns
            * the left one : the status of the staging area.
            * the right one : the status of the working tree.
            * ?? file untracked
               M modified and staged
             M   modified but not staged
             MM  modified and staged ,then modified and not staged
             A   add to stage area
             (see docs)
       * gitignore :
          * # comment,! negation
          * pattern start with / to avoid recursivity.
          * pattern end with / to specify a directory.
        * git diff is used to answer two questions :
          1. What have you changed but not yet staged?  
          ```
             git diff
          ```
          2. what have you staged that you are about to commit?  
          ```
             git diff --staged or  git diff--cached
             staged and cached are synonyms
          ```
        * commiting :
           * without specifying the -m option --> open your default editor with ``` git status ``` content on it
              or we could tell him to init with  ``` git diff ``` if we specify -v option
          * -m option  --> in-line message
          * -a option  --> stage and then commit (only tracked filed)
        * remove files :
          ```
          git rm file-name
          ```
           * this command with delete the file and stage it equivalent to :
             ```
             rm file-name
             git add file-name
             ```
           * to remove file from the staging area,or delete it from repository without delete it from the desk.
           ```
             git rm --cached file-name

           ```
       * renaming /moving
         ```
           git mv file_from  file_to
         ```
          is equivalent to
          ```
            mv file_from  file_to
            git rm file_from
            git add file_from
          ```
       * logging:
          ```
            # -p option means , see the diff ,-<n> means the last n commits
            git log -p -2

            # --stat option meas to make a summery for the
            git log --stat

            # --pretty ={online ,short,full,fuller} and format
            git log --pretty=oneline
            # --pretty with format
            git log --pretty=format:"%h - %an, %ar : %s"

            # --graph display branches in graph
            git log --pretty=format:"%h %s" --graph

            # --sence, --after, --until, --before = <date>
            git log --since=2.weeks

            # --autor ,--committer
            # --grep Only show commits with a commit message containing the string
            # -S Only show commits adding or removing code matching the string
          ```
       * Undoing Things :
         * undo a commit, for exemple to add a new file to the commit ,--amend keep the same first commit message
          ```
            git commit -m 'initial commit'
            git add forgotten_file
            git commit --amend
          ```
         * unstaging a Staged File
          ```
            git reset HEAD <file>
            git reset HEAD README
          ```
         * Unmodifying a Modified File
          ```
            git checkout -- <file>
            git checkout -- CONTRIBUTING.md
          ```  
       * remote : (to practice)
          * show your remotes
            ```
              git remote
              git remote -v
            ```
          * Adding Remote Repositories
             ```
               # git remote add <shortname> <url>
               git remote add pb https://github.com/paulboone/ticgit
             ```
          * fetch / pull
              ```
              # git fetch [remote-name]
              git fetch

              # git push [remote-name] [branch-name]
              git push origin master
              ```
          * Inspecting a Remote
             ```
              # git remote show [remote-name]
              git remote show origin

             ```
          * Removing and Renaming Remotes
            ```
               git remote rename pb paul
               git remote rm paul
            ```

       * Tagging : a pointer to a commit
         * list all tags : alphabetical order
           ```
              git tag
           ```
         * searching for tags
          ```
              git tag -l "v1.8.5*"
          ```
         * creating tags : there is two types of tags.
           1. lightweight :  it’s just a pointer to a specific commit
               ```
                  git tag <tag-name>
                  # to see the commit behind the tag
                  git show <tag-name>
               ```
           2. annotated : a tag with extra information like tagger name, email, and date; have a tagging message and could be
                          set to signed with GPG (GNU Privacy Guard ).
              ```
                   # git tag -a <tag-name> -m <message>
                   git tag -a v1.4 -m "my version 1.4"
              ```
          * tagging after :
             ```
                  # git tag <tag-name> <hash-part or all>
                  git tag -a v1.2 9fceb02
             ```
          * checkout to a specific tag : we shoudl use branch chekcout
             ```
                  # git checkout -b [branchname] [tagname]
                  git checkout -b version2 v2.0.0
             ```
          * Sharing Tags :
              1. push a specific tag
                 ```
                    # git push origin [tagname]
                    git push origin v1.5
                 ```
              2. push all tags
                 ```
                    git push origin --tags
                 ```
       * aliases:to add an alias we use the following syntax
         * git subcommand
          ```
             # git config --global alias.<al> <command>
             git config --global alias.ci commit

          ```
          * external tools (ei:gitk) ,we have to add !
          ```
            git config --global alias.vs '!gitk'
          ```
