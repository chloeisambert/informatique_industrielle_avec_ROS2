======================================
Premier pas avec les moteurs Dynamixel
======================================

1. Préparation
--------------
1. **Mise en place de la maquette**

   .. tabs::

      .. tab:: Suivre un tutoriel vidéo dédié 

         Rendez-vous sur `ce tutoriel <https://www.youtube.com/watch?v=E8XPqDjof4U>`_ et suivre jusqu'à **1min17** si vous utilisez `ROS2 Jazzy`.
         
         Dans la commande `git clone`, remplacer ``$ROS_DISTRO`` par ``humble``. ``ROS_DISTRO`` correspond à la version de ROS installée sur l'ordinateur. Le tuto est basé sur ROS Humble. Comme notre ordinateur utilise ROS Jazzy, nous devons forcer l'utilisation de Humble.

      .. tab:: Suivre un tutoriel écrit

         .. figure:: img/diagDynamixel.png
            :align: right
            :width: 60%

            Diagramme de câblage Dynamixel

         - A partir de l'image ci-dessus, réalisez le câblage du moteur Dynamixel en suivant les étapes ci-dessous :

         - Connectez le moteur Dynamixel à la carte de contrôle U2D2 en utilisant le câble fourni.
         - Branchez la carte de contrôle U2D2 à votre ordinateur via un câble USB.
         - Assurez-vous que les connexions sont sécurisées et que le moteur est correctement alimenté.

         - Ensuite, sur votre ordinateur, lancer un terminal et exécutez les commandes suivantes :

         - Créer l'espace de travail : 

         .. code-block:: bash

            mkdir -p ~/robotis_ws/src

         - Naviguez dans le dossier ``src``:

         .. code-block:: bash

            cd ~/robotis_ws/src

         - Clonez le dépôt ``DynamixelSDK`` :

         .. code-block:: bash

            git clone -b humble-devel https://github.com/ROBOTIS-GIT/DynamixelSDK


2. **Configurer l'environnement ROS :**
   
    - Revenir dans le dossier ``robotis_ws``.
    - Vérifiez si la commande ``ros2`` est reconnue. Si ce n'est pas le cas :
  
         - Ouvrez le fichier ``.bashrc`` : 

         .. code-block:: bash

            nano ~/.bashrc

         - Ajoutez à la fin du fichier : ``source /opt/ros/jazzy/setup.bash``
         - Rechargez le terminal pour appliquer les modifications.


3. **Vérifier les packages ROS :**
    
    Tapez la commande ``ros2`` pour vous assurer que tout est en place.


4. **Configurer et construire le projet :**
    
    Dans le dossier ``robotis_ws``, exécutez : 
    
    .. code-block:: bash

      source install/setup.bash
      colcon build --symlink-install


2. Exécution d’un projet
------------------------

1. **Configurer les permissions :**

Ajoutez votre utilisateur au groupe ``dialout`` pour accéder aux ports série :

.. code-block:: bash

   sudo usermod -aG dialout <linux_account>

Remplacez ``<linux_account>`` par votre nom d'utilisateur Linux. Pour connaître votre nom d'utilisateur, utilisez : ``whoami``. Puis redémarrez la machine pour appliquer les modifications.

2. **Ouvrir et modifier le code source :**

- Dans Visual Studio Code, naviguez vers : src > DynamixelSDK > dynamixel_sdk_examples > src > read_write_node.cpp
- Remplacez les lignes **42 à 46** par le code suivant : 

.. code-block:: bash

   // Control table address for X series (except XL-320)
   #define ADDR_OPERATING_MODE 255
   #define ADDR_TORQUE_ENABLE 24
   #define ADDR_GOAL_POSITION 30
   #define ADDR_PRESENT_POSITION 36


- Modifiez la ligne **49** pour définir le protocole de communication : ``#define PROTOCOL_VERSION 1.0``
- Changez la valeur du baudrate en **115200**. Enregistrez vos modifications.

3. **Reconstruire, resourcer et lancer le programme :**

Revenez dans le dossier ``robotis_ws`` et exécutez : 

.. code-block:: bash

   colcon build --symlink-install
   source install/setup.bash

Puis, tapez la commande suivante : 

.. code-block:: bash

   ros2 run dynamixel_sdk_examples read_write_node


3. Contrôle du moteur
----------------------

Pour envoyer une commande de position :

- Ouvrez un nouveau terminal.
- Naviguez dans le dossier ``robotis_ws`` et exécutez : 

.. code-block:: bash

   source install/setup.bash

.. end codeblock

- Lancez la commande suivante pour faire tourner votre moteur, par exemple, à une position ``500`` : 

.. code-block:: bash

   ros2 topic pub -1 /set_position dynamixel_sdk_custom_interfaces/msg/SetPosition "{id: 1, position: 500}"

Votre moteur devrait tourner !

.. note:: La position des moteurs est codée sur 10 bits, donc la commande peut prendre des valeurs de 0 à 1023. La position 500 correspond à, environ, la moitié de la course du moteur. Il est possible de changer le moteur que l'on souhaite tourner avec l'ID du moteur. Par exemple, pour le moteur 2, remplacez ``id: 1`` par ``id: 2``.
   
