# 🎫 Déploiement, Configuration et Sécurisation d'une Plateforme de Service Desk (Ticketing) : GLPI

## 📝 Présentation du Projet
Dans le cadre de ma formation en Administration Systèmes, Réseaux et Sécurité, j'ai réalisé la mise en production complète et le durcissement d'une plateforme de **Service Desk (Ticketing)** basée sur la solution Open Source **GLPI (Gestionnaire Libre de Parc Informatique)**.

L'objectif de cette mission est de fournir à une infrastructure d'entreprise un point de contact unique pour la gestion des incidents et des demandes d'assistance, structuré selon les bonnes pratiques du référentiel ITIL. Cette solution permet de centraliser les demandes des utilisateurs, d'optimiser le temps de traitement des techniciens et d'assurer un suivi rigoureux du parc informatique.

### 🛠️ Spécifications de l'Environnement Technique
Pour garantir l'isolation et la stabilité des services, l'infrastructure s'appuie sur la pile technologique suivante :
* **Hyperviseur :** Microsoft Hyper-V (Hébergement de la machine virtuelle sur un commutateur interne isolé).
* **Système d'Exploitation :** Linux Ubuntu Server 22.04 LTS.
* **Serveur Web :** Apache2.
* **Gestionnaire de Base de Données :** MariaDB (Fork open-source de MySQL).
* **Environnement d'Exécution :** PHP 8.1 avec l'ensemble des modules requis pour GLPI.

---

## 💻 Étape 1 : Interconnexion Réseau et Validation IP

La première phase absolue avant d'installer le moindre composant applicatif consiste à valider la connectivité réseau de notre serveur Linux Ubuntu. Cette étape permet de s'assurer que la machine virtuelle communique correctement à travers le commutateur virtuel de l'hyperviseur et qu'elle peut joindre sa passerelle réseau.

Pour ce faire, j'ai exécuté un test d'interconnexion à l'aide de la commande `ping` vers l'adresse IP cible de la passerelle de l'infrastructure (`192.168.1.200`).
![Test d'interconnexion réseau](02-test-ping-interconnexion.png)
*Validation de la connectivité réseau avec 0% de perte de paquets lors du test de ping.*

---

## 💻 Étape 2 : Installation de l'Environnement Serveur LAMP

Une fois la connectivité réseau validée, l'étape suivante consiste à préparer le serveur à recevoir l'application GLPI. Pour cela, j'ai déployé l'environnement indispensable **LAMP** (Linux, Apache2, MariaDB, PHP). 

Cette phase installe le serveur Web chargé de distribuer les pages, le moteur de base de données relationnelle ainsi que PHP 8.1 avec les extensions applicatives requises pour le traitement des scripts.

<br>

![Installation de l'environnement LAMP](03-installation-environnement-lamp.png)

<br>

*Suivi de la fin du processus d'installation des paquets et bascule automatique vers le module Apache mpm_prefork.*

---
