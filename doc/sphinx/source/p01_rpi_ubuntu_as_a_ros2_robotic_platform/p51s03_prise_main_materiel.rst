==========================
Prise en main du matériel
==========================

1. Préparation du matériel
===========================

- **Installer le radiateur sur la Raspberry Pi :**
  - Retirer le cache du connecteur JST avant installation.
  - Suivez les instructions fournies dans la `notice d'installation du radiateur <https://datasheets.raspberrypi.com/cooling/raspberry-pi-active-cooler-product-brief.pdf>`_.

- **Installer le dissipateur thermique et le disque dur :**
    - Retirer l'opercule du dissipateur thermique (lame bleue) et le coller sur le disque dur.
    - Insérer le disque dur dans l'encoche de la carte NVMe BASE Pimoroni (attention au détrompeur).
    - Fixer avec une vis de référence (vis-écrou-disque dur-écrou).
    - Installer les 4 entretoises sur la base.
    - Connecter la base à la Raspberry Pi en respectant les sens de branchement.
    - Positionner et visser la Raspberry sur la base.
    - Référez-vous au `support du disque dur Pimoroni <https://learn.pimoroni.com/article/getting-started-with-nvme-base>`_.

2. Installer l'OS
=================

- **Préparation initiale :**
    - Insérez la carte SD contenant Raspbian dans la Raspberry Pi.
    - Branchez le câble HDMI et l'alimentation.
    - Si la carte SD est utilisée pour la première fois :
      - Configurez les paramètres (langue : français, etc.).
      - Identifiants par défaut : username : `pi`, password : `pi`.
      - Configurez un partage de connexion avec votre téléphone pour accéder à Internet.
      - Définissez Firefox comme navigateur par défaut, mettez à jour, puis redémarrez.

- **Installation du système sur le disque NVMe :**
  - Ouvrez un terminal et suivez la section *"Installing your OS onto the NVMe SSD"* dans le `guide de support Pimoroni <https://learn.pimoroni.com/article/getting-started-with-nvme-base>`_.
  - À l'étape *"OS Installation Options"*, utilisez l'option 1 : *Install a new OS using Raspberry Pi OS Desktop* avec Raspberry Pi Imager.

- **Partitionnement du disque dur :**
  - Installez l'outil GParted : ``sudo apt-get install gparted``.
  - Ouvrez GParted (Menu -> Outil système).
  - Sélectionnez en haut à droite : `/dev/nvme0n1`.
  - Créez une table de partition (type : msdos).
  - Définissez une nouvelle partition :
    - Taille : 122000 (la moitié du disque).
    - Étiquette : nom personnalisé.
  - Appliquez toutes les modifications (bouton check vert).
  - Fermez GParted.

- **Installer Ubuntu LTS 24.04 :**
  - Utilisez l'Imager pour sélectionner :
    - Modèle : Raspberry Pi 5.
    - Système d'exploitation : Ubuntu LTS 24.04 Desktop.
    - Stockage : choisissez le groupe créé lors du partitionnement.
  - Confirmez les messages d'avertissement (perte de données) et définissez un mot de passe.
  - Consultez la `documentation officielle Ubuntu <https://ubuntu.com/tutorials/how-to-install-ubuntu-desktop-on-raspberry-pi-4#2-prepare-the-sd-card>`_ pour plus de détails.

3. Outils
=========

- **Sécurité :**
  - Pour éviter tout risque d'électrocution, touchez la masse des tables de travail pour vous décharger.

- **Captures d'écran :**
  - Utilisez le logiciel Shutter : ``sudo apt-get install shutter``.

4. Utilisation de GitHub
========================

- Après avoir créé le dépôt, visualisez la documentation via :
  - Le projet -> Actions -> *Page Build and Deployment* -> *Deploy*.
  - Ou bien via : Le projet -> *Settings* -> *Pages*.

- Pour mettre à jour un fork déjà réalisé :
  - il faut vérifié si il y a un upstream -> git remote -v
  - Si aucun upstream est présent, il faut le créer : git remote add upstream git@github.com:yguel/informatique_industrielle_avec_ROS2.git
  - Ensuite il faut récupérer sur cette branche les nouvelles données : git fetch upstream
  - Pour conclure, il faut rebase la nouvelle branche vers la notre (rolling dans notre cas) -> git rebase upstream/rolling
  - Pour obtenir les nouvelles données, il suffit de pull. Pour spécifier comment réconcilier les branches : git config pull.rebase true, puis git pull
  