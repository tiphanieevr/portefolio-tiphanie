# 🎫 Déploiement, Configuration et Sécurisation d'une Plateforme de Service Desk (Ticketing) : GLPI

## 📝 Présentation Globale du Projet
Ce projet consiste en la mise en production, l'optimisation et la sécurisation complète de la solution Open Source **GLPI (Gestionnaire Libre de Parc Informatique)** au sein d'un environnement virtualisé d'entreprise.

L'objectif central de cette réalisation technique est de fournir au service informatique un outil de **Service Desk (Ticketing)** et de gestion des incidents moderne, structuré selon les bonnes pratiques ITIL. Cette plateforme centralise l'intégralité des demandes d'assistance des collaborateurs, planifie les interventions des équipes techniques et assure la continuité de service des infrastructures de l'entreprise.

---

## 🛠️ Spécifications de l'Environnement Technique
Pour garantir la stabilité de l'application de ticketing, l'infrastructure s'appuie sur une architecture système et réseau robuste :
* **Hyperviseur de Virtualisation :** Microsoft Hyper-V (Création, allocation des ressources et gestion des commutateurs virtuels pour la communication réseau de la VM).
* **Système d'Exploitation :** Linux Ubuntu Server 22.04 LTS (Système d'exploitation hébergeant l'application).
* **Serveur Web :** Apache2 (Gestion et distribution des requêtes HTTP/HTTPS de l'interface de support).
* **Gestionnaire de Base de Données :** MariaDB SQL (Stockage relationnel complet des tickets, historiques, utilisateurs et éléments du parc).
* **Environnement d'Exécution :** PHP 8.1 avec la pile technologique LAMP (Linux, Apache, MySQL/MariaDB, PHP).

---

## 🚀 L'Architecture du Système de Ticketing & Support Informatique
L'application GLPI a été configurée pour segmenter les accès et modéliser de bout en bout le cycle de vie d'une demande d'assistance :

1. **Le Profil Demandeur / Utilisateur (Interface Self-Service) :** Un collaborateur standard peut se connecter via son navigateur pour déclarer une panne informatique, ouvrir un ticket, y joindre des éléments de contexte (captures d'écran) et suivre en temps réel l'avancement de sa demande d'aide.
2. **Le Profil Technicien (Gestion des Interventions) :** Les membres du support reçoivent les alertes sur leur tableau de bord central. Ils ont la charge de qualifier le ticket, de définir un niveau de priorité (criticité de la panne), de s'attribuer la tâche, d'échanger avec l'utilisateur et d'apporter une solution technique.
3. **Traçabilité et Historique :** Chaque ticket résolu est historisé et automatiquement corrélé aux fiches d'inventaire des matériels (ordinateurs, serveurs, commutateurs), permettant d'obtenir des statistiques de fiabilité sur le parc informatique de l'entreprise.

---

## 🔧 Journal de Déploiement & Résolution des Incidents Techniques

### 1. Initialisation, Conflit SQL et Résolution en Ligne de Commande (CLI)
Lors de la phase initiale d'installation via l'assistant web, un incident majeur est survenu : un blocage dû à une mauvaise initialisation de la structure des tables SQL de test dans la base de données. 

Pour corriger ce bug et repartir sur un environnement de ticketing sain, une intervention manuelle en ligne de commande (CLI) directement sur le moteur MariaDB a été menée pour réinitialiser les droits et la base de données dédiée :

```bash
# Connexion sécurisée à l'interface de gestion MariaDB
sudo mysql -u root -p

# Nettoyage de l'environnement : Suppression de la base corrompue
DROP DATABASE glpidb;

# Recréation d'une base de données vierge et saine pour le ticketing
CREATE DATABASE glpidb;

# Attribution des privilèges d'administration à l'utilisateur dédié
GRANT ALL PRIVILEGES ON glpidb.* TO 'glpiuser'@'localhost';

# Actualisation de la table des droits et déconnexion
FLUSH PRIVILEGES;
EXIT;
