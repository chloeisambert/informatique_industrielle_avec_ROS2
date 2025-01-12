==============================
Astuces et outils
==============================

Astuces Git
=======================================

Utiliser `git add -u`
-------------------------

La commande `git add -u` est utilisée pour mettre à jour l'index avec les modifications apportées aux fichiers déjà suivis par Git (modifiés ou supprimés), sans inclure de nouveaux fichiers non suivis.

1. **Ajouter les modifications des fichiers suivis** :

   Utilisez la commande suivante pour ajouter uniquement les modifications des fichiers déjà suivis par Git (et éviter d'ajouter des fichiers non nécessaires et seulement les fichiers que vous venez de modifier) :

   .. code-block:: bash

      git add -u

   - Cette commande met à jour l'index en incluant :

     - Les fichiers modifiés.
     - Les fichiers supprimés.*

   - Les fichiers non suivis (nouveaux fichiers) ne sont pas pris en compte.
   - Une fois la commande exécutée, utilisez `git status` pour vérifier quels fichiers ont été ajoutés à l'index.

2. **Ajouter les modifications dans un répertoire spécifique** :

   Si vous souhaitez limiter l'opération à un répertoire particulier, utilisez :

   .. code-block:: bash

      git add -u <chemin_du_répertoire>

   - Exemple : Ajouter uniquement les modifications dans le dossier `src` :
     ```bash
     git add -u src/
     ```


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



Applications ou extensions optionnelles
=======================================

Captures d'écran
-----------------
Si vous souhaitez réaliser des captures d'écran sur **Ubuntu 20.04**, vous pouvez utiliser le logiciel **Shutter**. 
Pour l'installer, exécutez la commande suivante dans un terminal :

.. code-block:: bash

    sudo apt-get install shutter

Visualiser sa documentation en local
====================================

Pour visualiser votre documentation en local, deux possibilités s'offrent à vous :

Première possibilité : Installer et configurer Esbonio
------------------------------------------------------

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
        Rendez-vous sur le site officiel : https://www.python.org/downloads/.
      - **Cochez l’option "Add Python to PATH"** :
        Lors de l’installation, assurez-vous de cocher cette option. Cela permet de rendre l’exécutable Python accessible globalement depuis n’importe quel terminal. Vous pourrez alors exécuter des commandes comme `python` ou `pip` sans avoir à spécifier le chemin complet vers l’installation Python.



3. **Rechargez VSCode** :

   Si les extensions ne sont pas prises en compte immédiatement :

      - Ouvrez la palette de commande avec `Ctrl+Shift+P`.
        Rendez-vous sur le site officiel : https://www.python.org/downloads/.
      - Tapez et sélectionnez **Developer: Reload Window**.


4. **Prévisualiser votre documentation** :
   
   - Ouvrez un fichier `.rst` dans VSCode.
   - Accédez à la palette de commande avec `Ctrl+Shift+P`.
   - Tapez et sélectionnez **Esbonio: Open preview to the side**.
   - Une fenêtre de prévisualisation s'ouvrira pour afficher la documentation générée.

Seconde possibilité : Générer directement un fichier .html local 
---------------------------------------------------------------

Vous pouvez générer directement votre documentation au format HTML en utilisant **Sphinx**. Cette méthode crée des fichiers HTML statiques qui peuvent être ouverts dans n'importe quel navigateur.


1. **Accédez au répertoire source de votre projet** :
   
   - Assurez-vous que vous êtes dans le répertoire contenant vos fichiers de documentation (`source/`).
   - Si vous utilisez un terminal intégré dans VSCode, ouvrez-le via **Terminal > New Terminal** ou utilisez le raccourci `Ctrl+`` (backtick).
     
2. **Exécutez la commande de génération** :

    - Utilisez la commande suivante pour générer les fichiers HTML dans un répertoire `build/` :
      ```bash
      sphinx-build -b html source/ build/
      ```
    - Des avertissements peuvent apparaître, comme par exemple des fichiers .rst n'apparaissant pas dans un index, mais ils ne devraient pas empêcher la génération de la documentation.
    - Explications des arguments :

     - `-b html` : Spécifie que vous voulez générer une sortie au format HTML.
     - `source/` : Répertoire où sont stockés vos fichiers `.rst`.
     - `build/` : Répertoire de sortie où les fichiers HTML seront enregistrés.


3. **Ouvrez le fichier HTML généré** :

   - Une fois la génération terminée, ouvrez le fichier `index.html` situé dans le répertoire `build/` avec votre navigateur préféré.
   - Si vous êtes sous Linux ou macOS, vous pouvez utiliser une commande comme celle-ci :
     ```bash
     xdg-open build/index.html
     ```
   - Sous Windows, naviguez jusqu'au répertoire `build/` avec l'explorateur de fichiers, puis double-cliquez sur `index.html`.


4. **Modifications ultérieures** :

   - Si vous modifiez vos fichiers `.rst`, vous devez régénérer la documentation en exécutant de nouveau la commande :
     ```bash
     sphinx-build -b html source/ build/
     ```
   - Cette étape garantit que les fichiers HTML reflètent les changements récents.



**Utilisation de GitHub :**

   - Après avoir créé le dépôt, visualisez la documentation via :
  
     - Le projet -> Actions -> *Page Build and Deployment* -> *Deploy*.
     - Ou bien via : Le projet -> *Settings* -> *Pages*.

  - Pour mettre à jour un fork déjà réalisé :
  
     - Vérifier si il y a un upstream -> git remote -v
     - Si aucun upstream est présent, il faut le créer : git remote add upstream git@github.com:yguel/informatique_industrielle_avec_ROS2.git
     - Ensuite il faut récupérer sur cette branche les nouvelles données : git fetch upstream
     - Pour conclure, il faut rebase la nouvelle branche vers la notre (rolling dans notre cas) -> git rebase upstream/rolling
     - Pour obtenir les nouvelles données, il suffit de pull. Pour spécifier comment réconcilier les branches : git config pull.rebase true, puis git pull
  
  