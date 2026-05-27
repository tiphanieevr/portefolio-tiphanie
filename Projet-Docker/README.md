# 🐳 Déploiement Industrialisé et Sécurisé d'un Serveur Web avec Docker

## 📝 Présentation du projet
Dans le cadre de ma veille technologique sur la modernisation des infrastructures, j'ai réalisé la mise en production complète d'un serveur web conteneurisé. L'objectif de ce projet est de répondre aux problématiques actuelles des entreprises : isolation des applications, rapidité de déploiement (Infrastructure as Code) et automatisation de la sécurité des flux.

## 🛠️ Architecture et Environnement Technique
* **Hyperviseur :** Microsoft Hyper-V (Machine virtuelle isolée)
* **Système d'Exploitation :** Linux Ubuntu Server 24.04 LTS
* **Moteur de Conteneurisation :** Docker Engine & Docker Compose
* **Serveur Web & Reverse Proxy :** Nginx
* **Sécurisation :** Chiffrement SSL/TLS (Let's Encrypt), isolation par réseaux virtuels Docker (Bridge) et restriction des privilèges (mode non-root).

---

## 💻 Étapes de Réalisation Technique

### Étape 1 : Installation et configuration de Docker
Mise à jour des dépôts de l'hôte Ubuntu et installation des paquets officiels de Docker :
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
version: '3.8'

services:
  reverse-proxy:
    image: nginx:alpine
    container_name: nginx_proxy
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./certs:/etc/ssl/certs:ro
    networks:
      - web_network
    restart: always

  web-app:
    image: httpd:alpine
    container_name: internal_web_site
    networks:
      - web_network
    restart: always

networks:
  web_network:
    driver: bridge
docker compose up -d
