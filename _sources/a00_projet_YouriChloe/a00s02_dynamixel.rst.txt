==============================
Premier pas avec les Dynamixel
==============================

Préparation
-----------

1. **Suivre le tuto vidéo jusqu'à 1min17 :**
    
    Dans la commande `git clone`, remplacer ``$ROS_DISTRO`` par ``humble``. ``ROS_DISTRO`` correspond à la version de ROS installée sur l'ordinateur. Le tuto est basé sur ROS Humble. Comme notre ordinateur utilise ROS Jazzy, nous devons forcer l'utilisation de Humble.


2. **Configurer l'environnement ROS :**
   
    - Naviguez dans le dossier ``robotis_ws``.
    - Vérifiez si la commande ``ros2`` est reconnue. Si ce n'est pas le cas :
  
         - Ouvrez le fichier ``.bashrc`` : ``nano ~/.bashrc``
         - Ajoutez à la fin du fichier : ``source /opt/ros/jazzy/setup.bash``
         - Rechargez le terminal pour appliquer les modifications.


3. **Vérifier les packages ROS :**
    
    Tapez la commande ``ros2`` pour vous assurer que tout est en place.


4. **Configurer et construire le projet :**
    
    Dans le dossier ``robotis_ws``, exécutez : 
    
    .. code-block:: bash

      source install/setup.bash
      colcon build --symlink-install


Exécution d’un projet
----------------------

1. **Configurer les permissions :**

Ajoutez votre utilisateur au groupe ``dialout`` pour accéder aux ports série :

.. code-block:: bash

   sudo usermod -aG dialout <linux_account>

Remplacez ``<linux_account>`` par votre nom d'utilisateur Linux. Pour connaître votre nom d'utilisateur, utilisez : ``whoami``. Puis redémarrez la machine pour appliquer les modifications.

2. **Ouvrir et modifier le code source :**

- Dans Visual Studio Code, naviguez vers : src > DynamixelSDK > dynamixel_sdk_examples > src > read_write_node.cpp
- Remplacez les lignes 42 à 46 par le code suivant : 

.. code-block:: bash

   // Control table address for X series (except XL-320)
   #define ADDR_OPERATING_MODE 255
   #define ADDR_TORQUE_ENABLE 24
   #define ADDR_GOAL_POSITION 30
   #define ADDR_PRESENT_POSITION 36


- Modifiez la ligne 49 pour définir le protocole de communication : ``#define PROTOCOL_VERSION 1.0``
- Changez la valeur du baudrate en ``115200``. Enregistrez vos modifications.

3. **Reconstruire, resourcer et lancer le programme :**

Revenez dans le dossier ``robotis_ws`` et exécutez : 

.. code-block:: bash

   colcon build --symlink-install
   source install/setup.bash

Puis, tapez la commande suivante : 

.. code-block:: bash

   ros2 run dynamixel_sdk_examples read_write_node


Contrôle du moteur
------------------

Pour envoyer une commande de position :

- Ouvrez un nouveau terminal.
- Naviguez dans le dossier ``robotis_ws`` et exécutez : 

.. code-block:: bash

   source install/setup.bash

.. end codeblock

- Lancez la commande suivante : 

.. code-block:: bash

   ros2 topic pub -1 /set_position dynamixel_sdk_custom_interfaces/msg/SetPosition "{id: 1, position: 500}"

Votre moteur devrait tourner !