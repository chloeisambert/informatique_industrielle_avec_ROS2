==============================
Astuces et outils
==============================

1. Astuces Git/GitHub
=======================================

Utiliser `git add -u`
---------------------

La commande `git add -u` est utilisée pour mettre à jour l'index avec les modifications apportées aux fichiers déjà suivis par Git (modifiés ou supprimés), sans inclure de nouveaux fichiers non suivis.

* **Ajouter les modifications des fichiers suivis** :

   Utilisez la commande suivante pour ajouter uniquement les modifications des fichiers déjà suivis par Git (et éviter d'ajouter des fichiers non nécessaires et seulement les fichiers que vous venez de modifier) :

   .. code-block:: bash

      git add -u

   - Cette commande met à jour l'index en incluant :

     - Les fichiers modifiés.
     - Les fichiers supprimés.

   - Les fichiers non suivis (nouveaux fichiers) ne sont pas pris en compte.
   - Une fois la commande exécutée, utilisez `git status` pour vérifier quels fichiers ont été ajoutés à l'index.

.. note:: **Ajouter les modifications dans un répertoire spécifique** :

   Si vous souhaitez limiter l'opération à un répertoire particulier, utilisez :

   .. code-block:: bash

      git add -u <chemin_du_répertoire>

   - Exemple : Ajouter uniquement les modifications dans le dossier `src` :

     .. code-block:: bash

        git add -u src/


Réinitialiser un fichier modifié
--------------------------------

Si vous avez modifié un fichier dans votre dépôt Git mais souhaitez revenir à son état initial (tel qu'il était dans le dernier commit), suivez ces étapes :

1. **Réinitialiser le fichier** :

   Pour annuler les modifications et ramener le fichier à son état initial, utilisez la commande suivante :

   .. code-block:: bash

      git restore <nom_du_fichier>

   - Cette commande remet le fichier dans l'état qu'il avait lors du dernier commit.
   - Si vous utilisez une version de Git antérieure à 2.23, utilisez cette alternative :

     .. code-block:: bash

        git checkout -- <nom_du_fichier>

2. **Vérifiez l'état** :

   Une fois la commande exécutée, vérifiez que le fichier n'apparaît plus comme modifié avec :

   .. code-block:: bash

      git status

   Cette commande confirme que le fichier a bien été réinitialisé.

Mise en place de Git sur Windows
--------------------------------

Pour installer et configurer Git sur un ordinateur Windows, suivez ces étapes :

1. **Télécharger Git :**

   - Rendez-vous sur le `site officiel de Git <https://git-scm.com/downloads/win>`_ pour télécharger la dernière version.
   - Téléchargez la version correspondant à votre système, généralement **64-bit Git for Windows Setup**.

2. **Installer Git :**

   - Lancez l’exécutable téléchargé.
   - Suivez les étapes de l'installation par défaut en cliquant sur **Suivant** jusqu'à la fin.

3. **Configurer Git pour Windows :**

   - Une fois l'installation terminée, ouvrez une invite de commande (CMD ou PowerShell).
   - Configurez votre nom et votre e-mail pour Git en exécutant les commandes suivantes :

     .. code-block:: bash
      
        git config --global user.name "VotreNom"
        git config --global user.email "VotreEmail@example.com"


4. **Gérer les erreurs courantes :**

   - Si, lors d'un `git pull`, vous rencontrez l'erreur suivante :  
     
     ```
     fatal: filename too long
     ```
     
     Cela signifie que Windows ne peut pas gérer des chemins de fichiers dépassant 260 caractères. Pour corriger cela, exécutez la commande suivante :

     .. code-block:: bash

        git config --system core.longpaths true


   - Cette commande permet à Git de prendre en charge les chemins de fichiers longs sous Windows.


Visualiser la documentation en ligne
------------------------------------

Après la création et le déploiement de la documentation via GitHub Pages, suivez ces étapes pour la visualiser en ligne :

1. **Depuis l'onglet Actions :**

   - Accédez à votre projet sur GitHub.
   - Cliquez sur l'onglet **Actions**.
   - Recherchez le workflow intitulé **Page build and deployment** et cliquer dessus, votre lien devrait apparaître.
   - Vérifiez que le statut indique **Deploy succeeded** pour confirmer que la documentation a été déployée avec succès.

2. **Depuis les paramètres du projet :**

   - Accédez à votre projet sur GitHub.
   - Cliquez sur l'onglet **Settings**.
   - Dans le menu latéral, sous la section **Code and automation**, cliquez sur **Pages**.
   - Vous trouverez un lien vers la documentation déployée sous la section **GitHub Pages**.

3. **Lien direct :**

   Une fois configurée, la documentation est accessible à l'adresse suivante :

   - `https://<username>.github.io/<repository-name>/`
   - Remplacez `<username>` par votre nom d'utilisateur GitHub et `<repository-name>` par le nom de votre projet.


Inviter des collaborateurs sur un projet
----------------------------------------

Pour inviter des collaborateurs à participer à votre projet sur GitHub, suivez ces étapes :

1. **Accéder aux paramètres du projet :**

   - Ouvrez votre projet sur GitHub.
   - Cliquez sur l'onglet **Settings**.

2. **Rechercher et ajouter :**

   - Dans le menu latéral, sous la section **Access**, cliquez sur **Collaborators**.
   - Cliquez sur le bouton **Add people** pour inviter des collaborateurs.
   - Entrez le nom d'utilisateur ou l'adresse e-mail GitHub du collaborateur que vous souhaitez inviter.
   - Cliquez sur **Add** pour envoyer l'invitation.

3. **Confirmer l'invitation :**

   - Une fois l'invitation envoyée, le collaborateur recevra un e-mail avec un lien pour accepter.
   - Une fois accepté, il apparaîtra dans la liste des collaborateurs de votre projet.

.. note:: Pour supprimer un collaborateur, cliquez sur l'icône **Trash** à côté de son nom.


Mettre à jour un fork réalisé sur GitHub
----------------------------------------

Pour synchroniser un fork avec le dépôt d'origine sur GitHub, suivez les étapes ci-dessous :

1. **Vérifier la configuration des remotes :**

   - Ouvrez un terminal et naviguez dans le dossier de votre projet.
   - Vérifiez si le remote `upstream` est déjà configuré :

     .. code-block:: bash

        git remote -v

   - Si `upstream` n'est pas listé, ajoutez-le avec la commande suivante :

     .. code-block:: bash

        git remote add upstream git@github.com:[nom_utilisateur]/[nom_dépôt_initial].git

2. **Récupérer les mises à jour depuis le dépôt original :**

   - Téléchargez les nouvelles données depuis le dépôt `upstream` :

     .. code-block:: bash

        git fetch upstream

3. **Rebaser votre branche locale sur la branche distante :**

   - Intégrez les modifications de la branche distante (`rolling`, dans ce cas) dans votre branche locale :

     .. code-block:: bash

        git rebase upstream/rolling

4. **Configurer Git pour les futures synchronisations :**

   - Configurez Git pour utiliser le mode `rebase` par défaut lors d’un pull, afin de réconcilier les branches proprement :

     .. code-block:: bash

        git config pull.rebase true

   - Ensuite, synchronisez avec les dernières modifications :

     .. code-block:: bash

        git pull


2. Visualiser sa documentation en local
=======================================

Pour visualiser votre documentation en local, deux possibilités s'offrent à vous :


   .. tabs::

      .. tab:: Première possibilité : Installer et configurer Esbonio

         
         1. **Installer Esbonio** :

            - Ouvrez **Visual Studio Code**.
            - Accédez à l'onglet des **extensions** (raccourci : `Ctrl+Shift+X`).
            - Recherchez l'extension **Esbonio** et cliquez sur **Installer**.


         2. **Configurer les extensions nécessaires** :

            - Ouvrez un terminal intégré dans VSCode via **Terminal > New Terminal** ou utilisez le raccourci `Ctrl+``.
            - Installez les extensions Python requises dans le fichier `requirements.txt` en exécutant la commande suivante :

            .. code-block:: bash

               python.exe -m pip install -r requirements.txt

            - Si cela ne fonctionne pas, installer manuellement chaque extension présent dans `requirements.txt` avec la commande suivante :

            .. code-block:: bash

               python.exe -m pip install "nom extension"

            - Dans le cas de cette documentation, une extension "mistune < 1.0.0" est présente. Cela indique que nous utilisons une version inférieure à 1.0.0 de l'extension mistune. Pour l'installer, exécutez la commande suivante :
            
            .. code-block:: bash

               python.exe -m pip install "mistune<1.0.0"   
            
            - Si la commande `python.exe` n’est pas reconnue :

               - **Téléchargez et installez Python** :

               Rendez-vous sur le `site officiel de Python <https://www.python.org/downloads/>`_ pour télécharger la dernière version.

               - **Cochez l’option "Add Python to PATH"** :

               Lors de l’installation, assurez-vous de cocher cette option. Cela permet de rendre l’exécutable Python accessible globalement depuis n’importe quel terminal. Vous pourrez alors exécuter des commandes comme `python` ou `pip` sans avoir à spécifier le chemin complet vers l’installation Python.

         3. **Rechargez VSCode** :

            Si les extensions ne sont pas prises en compte immédiatement :

               - Ouvrez la palette de commande avec `Ctrl+Shift+P`.
               - Tapez et sélectionnez **Developer: Reload Window**.


         4. **Prévisualiser votre documentation** :
            
            - Ouvrez un fichier `.rst` dans VSCode.
            - Accédez à la palette de commande avec `Ctrl+Shift+P`.
            - Tapez et sélectionnez **Esbonio: Open preview to the side**.
            - Une fenêtre de prévisualisation s'ouvrira pour afficher la documentation générée.


      .. tab:: Seconde possibilité : Générer directement un fichier .html local

         Vous pouvez générer directement votre documentation au format HTML en utilisant **Sphinx**. Cette méthode crée des fichiers HTML statiques qui peuvent être ouverts dans n'importe quel navigateur.


         1. **Accédez au répertoire source de votre projet** :
            
            - Assurez-vous que vous êtes dans le répertoire contenant vos fichiers de documentation (`source/`).
            - Si vous utilisez un terminal intégré dans VSCode, ouvrez-le via **Terminal > New Terminal** ou utilisez le raccourci `Ctrl+`` (backtick).
            
         2. **Exécutez la commande de génération** :

            - Utilisez la commande suivante pour générer les fichiers HTML dans un répertoire `build/` :

            .. code-block:: bash

               sphinx-build -b html source/ build/
            
            - Des avertissements peuvent apparaître, comme par exemple des fichiers .rst n'apparaissant pas dans un index, mais ils ne devraient pas empêcher la génération de la documentation.
            - Explications des arguments :

            - `-b html` : Spécifie que vous voulez générer une sortie au format HTML.
            - `source/` : Répertoire où sont stockés vos fichiers `.rst`.
            - `build/` : Répertoire de sortie où les fichiers HTML seront enregistrés.


         3. **Ouvrez le fichier HTML généré** :

            - Une fois la génération terminée, ouvrez le fichier `index.html` situé dans le répertoire `build/` avec votre navigateur préféré.
            - Si vous êtes sous Linux ou macOS, vous pouvez utiliser une commande comme celle-ci :

            .. code-block:: bash

               xdg-open build/index.html


            - Sous Windows, naviguez jusqu'au répertoire `build/` avec l'explorateur de fichiers, puis double-cliquez sur `index.html`.


         4. **Modifications ultérieures** :

            - Si vous modifiez vos fichiers `.rst`, vous devez régénérer la documentation en exécutant de nouveau la commande :

            .. code-block:: bash

               sphinx-build -b html source/ build/


            - Cette étape garantit que les fichiers HTML reflètent les changements récents.

  
3. Applications ou extensions optionnelles
==========================================

Captures d'écran
-----------------
Si vous souhaitez réaliser des captures d'écran sur **Ubuntu 24.04**, vous pouvez utiliser le logiciel **Shutter**. 
Pour l'installer, exécutez la commande suivante dans un terminal :

.. code-block:: bash

    sudo apt-get install shutter