# Pension Canine du Vieux Chêne

![Logo Pension Canine du Vieux Chêne](docs/images/logo-blanc.png)


## Présentation

Site vitrine officiel de la Pension Canine du Vieux Chêne (Le Petit Tampon, La Réunion).

Ce site a été réalisé en pur HTML/CSS afin de garantir :

- Une totale indépendance technique
- Une propriété complète du site et des fichiers
- Un site rapide et optimisé pour les utilisateurs

Ce site est actuellement hébergé gratuitement via GitHub Pages pour les tests et l'évaluation.

### Hébergement final prévu :

Le site sera hébergé prochainement en local sur une Raspberry Pi 3 avec Matomo installé pour un suivi des statistiques respectueux du RGPD et auto-hébergé.

---

## Fonctionnalités réalisées

- Site full responsive (mobile / tablette / PC)
- Mode sombre (Dark Mode) activable manuellement
- Formulaire de réservation intégré via iframe Brevo (ex Sendinblue)
- Section météo dynamique via API Open Meteo
- Mentions légales conformes RGPD
- Footer complet avec liens de contact et WhatsApp
- SEO optimisé sur toutes les pages (balises Title, Meta Description, arborescence claire)
- Design sobre, naturel et efficace
- Intégration Matomo prévue (déjà en partie scriptée)

---

## Pages disponibles

- Accueil (index.html)
- Services (services.html)
- À propos / Qui sommes-nous (about.html)
- Réservation (reservation.html)
- FAQ (faq.html)
- Contact (contact.html)
- Mentions légales (legal.html)
- Page Merci (merci.html)

---

## Auteur

Benoit GIRAUD-MISSIER

Projet réalisé dans le cadre du BP REA 2024 - Évaluation C7

Saint Gervais d'Auvergne - Avril 2025

---

## Capture d'écran

![Aperçu site](docs/images/capture-site.png)

---

> "Un site simple, rapide, éthique et local — comme notre pension canine."


---
# Guide d'installation complet 🛠️

Instructions pour installer le site de la Pension Canine du Vieux Chêne sur un serveur local (Raspberry Pi 3 ou +) avec Matomo pour les statistiques.

---

## Prérequis 🐿

Matériel :
- Raspberry Pi 3 (ou supérieur)
- Carte microSD 32 Go
- Système : Raspberry Pi OS (Lite ou Desktop)
- Connexion Internet stable
- Accès SSH activé (optionnel mais conseillé)

Logiciels requis :
- Apache2
- PHP
- MariaDB (ou MySQL)
- Matomo (outil statistique libre)

---

## Mise à jour du système 💪

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Installation du serveur Web (Apache + PHP) 🌐

```bash
sudo apt install apache2 php libapache2-mod-php -y
```

Test :
Accédez à votre Pi via :

http://IP_DE_VOTRE_PI

Vous devriez voir la page Apache par défaut.

---

## Installation de MariaDB 📁

```bash
sudo apt install mariadb-server php-mysql -y
```

Sécurisation de la BDD :

```bash
sudo mysql_secure_installation
```

Suivez les instructions (mot de passe, suppression des comptes anonymes, etc).

---

## Installation de Matomo 📊

Se placer dans /var/www/html/ :

```bash
cd /var/www/html/
sudo wget https://builds.matomo.org/matomo-latest.zip
sudo apt install unzip
sudo unzip matomo-latest.zip
sudo chown -R www-data:www-data matomo
```

Configurer ensuite Matomo via :

http://IP_DE_VOTRE_PI/matomo

Suivez l’assistant pour connecter la base de données.

---

## Déploiement de votre site HTML DIY 🚀

Toujours dans :

```bash
cd /var/www/html/
```

Copiez les fichiers de votre site :

```bash
sudo rm index.html  # (supprime la page Apache)
sudo cp -r /chemin/vers/votre/site/* .
```

---

## Configuration finale 🔧

Redémarrer Apache :

```bash
sudo systemctl restart apache2
```

Votre site est maintenant disponible en local à l'adresse :

http://IP_DE_VOTRE_PI

Matomo à l'adresse :

http://IP_DE_VOTRE_PI/matomo

---

> Pensez à sauvegarder régulièrement votre site et vos bases de données !

> Ce tuto est volontairement simplifié pour un usage local et personnel.

---

Fichier rédigé par Benoit GIRAUD-MISSIER — Avril 2025



