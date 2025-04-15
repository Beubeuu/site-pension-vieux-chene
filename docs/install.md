INSTALLATION - Pension Canine du Vieux Chêne

Objectif

Installation locale complète du site HTML/CSS sur une Raspberry Pi 3 avec Matomo pour le suivi des statistiques. Ce guide vise une mise en service simple, durable, auto-hébergée, respectueuse de la vie privée (RGPD) et totalement indépendante.

🧰 Prérequis Matériels

Raspberry Pi 3 (ou version supérieure)

Carte microSD (16 Go minimum, classe 10 recommandée)

Connexion internet (Ethernet ou Wi-Fi)

Alimentation fiable

Clavier/écran OU accès SSH activé

📥 Installation du système Raspberry Pi OS

Télécharger Raspberry Pi OS Lite depuis :https://www.raspberrypi.com/software/

Flasher l’image sur la carte SD avec Raspberry Pi Imager ou balenaEtcher.

(Optionnel mais recommandé) :

Créer un fichier vide nommé ssh à la racine de la carte SD (pour activer SSH)

Créer un fichier wpa_supplicant.conf si vous utilisez le Wi-Fi (voir doc officielle)

🔧 Mise à jour et installation du serveur web

sudo apt update && sudo apt upgrade -y
sudo apt install apache2 php libapache2-mod-php unzip -y

Tester l’accès à : http://raspberrypi.local ou http://[adresse_IP]

🌐 Déploiement du site

Cloner ou copier vos fichiers (ex : depuis une clé USB ou GitHub)

cd /var/www/html
sudo rm index.html  # Supprime la page par défaut d’Apache
sudo cp -r ~/site-pension-vieux-chene/docs/* .

Vérifier les permissions :

sudo chown -R www-data:www-data /var/www/html

📊 Installation de Matomo (statistiques locales RGPD)

Télécharger Matomo : https://matomo.org/download/

cd /var/www/html
sudo mkdir matomo
cd matomo
sudo wget https://builds.matomo.org/matomo.zip
sudo unzip matomo.zip && sudo rm matomo.zip

Créer une base de données MariaDB (facultatif mais recommandé)

sudo apt install mariadb-server -y
sudo mysql_secure_installation
sudo mysql -u root -p

CREATE DATABASE matomo;
CREATE USER 'matomo'@'localhost' IDENTIFIED BY 'motdepassefort';
GRANT ALL PRIVILEGES ON matomo.* TO 'matomo'@'localhost';
FLUSH PRIVILEGES;
EXIT;

Lancer l’installation via le navigateur :

http://[adresse_IP]/matomo

Suivre les instructions à l’écran.

🔐 Sécurisation basique d’Apache

Activer SSL :

sudo a2enmod ssl
sudo a2ensite default-ssl.conf
sudo systemctl reload apache2

Certificat avec Let's Encrypt (si nom de domaine) :

sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache

💾 Script de sauvegarde simple

Créer un fichier /home/pi/backup.sh :

#!/bin/bash
tar -czf /home/pi/site-backup.tar.gz /var/www/html

Puis rendre exécutable :

chmod +x /home/pi/backup.sh

Et automatiser avec cron :

crontab -e

Ajouter :

0 3 * * * /home/pi/backup.sh

(sauvegarde quotidienne à 3h)

🛠 Astuces optionnelles

IP Fixe locale : utile pour accéder au site facilement

sudo nano /etc/dhcpcd.conf

Ajouter en fin de fichier :

interface eth0
static ip_address=192.168.1.42/24
static routers=192.168.1.1
static domain_name_servers=1.1.1.1 8.8.8.8

Redémarrage automatique Apache :

sudo systemctl enable apache2

✅ Résultat final

Le site HTML/CSS est accessible localement (et publiquement si ouvert).

Les statistiques Matomo sont actives sur l’interface admin.

Le Raspberry Pi fait office de serveur web auto-hébergé, éthique, autonome et libre.

Projet artisanal, local et durable — parfait pour une pension canine indépendante. 🐶

