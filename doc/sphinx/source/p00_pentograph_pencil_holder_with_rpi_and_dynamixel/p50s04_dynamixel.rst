==============================
Premier pas avec les dynamixel
==============================

Suivre le tuto vidéo jusqu'à 1min17 : dans la commande git clone, remplacer "$ROS_DISTRO" par "humble". ROS_DISTRO correspond à la version de ROS installé sur l'ordinateur. Le tuto est en ROS humble, comme notre ordinateur est en ROS jazzy, nous ne devons pas mettre notre ROS_DISTRO mais forcer à être en humble.

Se placer dans le dossier robotis_ws. Normalement, si vous faites
"ros2" 
La commande n'est pas trouvé. Il faut définir la source : 
nano /bashrc
Et rajouter à la fin : 
source /opt/ros/jazzy/setup.bash
Puis vérifier que ros2 à récupérer tout ses packages en écrivant ros2.
Il faut setup dans le fichier install : 
dans robotis_ws, écrire "source install/setup.bash"
Puis vous pouvez build : 
colcon build --symlink-install

Run un projet : 

Il faut se donner les permissions : 
sudo usermod -aG dialout <linux_account> et remplacer <linux_account> par votre nom de compte
Pour checker son nom de compte : whoami dans la console

Redémarrer votre machine pour rendre effectif les changements de permissions

Ensuite, dans visual studio code, aller dans votre projet robotis_ws

Ouvrir : src > DynamixelSDK > dynamixel_sdk_examples > src > read_write_node.cpp

Et modifier les lignes 42 à 46 par le code suivant :
// Control table address for X series (except XL-320)
#define ADDR_OPERATING_MODE 255
#define ADDR_TORQUE_ENABLE 24
#define ADDR_GOAL_POSITION 30
#define ADDR_PRESENT_POSITION 36

Puis changer le protocol de communication par : 
"#define PROTOCOL_VERSION 1.0" à la ligne 49

Puis changer le baudrate par 115200, enregistrer.

revenir à robotis_ws, build avec : 
colcon build --symlink-install

Et resourcer : 
source install/setup.bash

Puis rentrer la commande suivante : 
ros2 run dynamixel_sdk_examples read_write_node

Vous êtes en mode controle du moteur, ouvrez un nouveau terminal, se mettre dans le dossier robotis_ws, sourcer avec source install/setup.bash et écrire : 

ros2 topic pub -1 /set_position dynamixel_sdk_custom_interfaces/msg/SetPosition "{id: 1, position: 500}"

Votre moteur tourne !
