# Pulse Kubernetes Deployment

Willkommen beim offiziellen Kubernetes-Deployment des Pulse-Projekts von Code99.

## Inhalt

- Produktionsbereites Deployment für WebApp-Main
- Load Balanced Service für mehrere Webserver
- Ingress-Controller (Traefik) für externen Zugriff
- Zukunftssicher ausgelegt für Autoscaling und Failover

## Nutzung

- Eigene Installation auf privaten oder internen Servern ist gestattet.
- Öffentliche SaaS-Angebote basierend auf diesem Code sind **nicht** erlaubt (siehe Lizenz).

## Installation

- sudo apt update
- sudo apt install apt-transport-https ca-certificates curl software-properties-common
- curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
- sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
- sudo apt update

## Lizenz

Dieses Projekt steht unter der [Business Source License 1.1](LICENSE).  
Das exklusive Recht zur öffentlichen Bereitstellung als SaaS liegt bei Code99 (Christian Wilhelm).

Hinweis: Verstöße gegen die Lizenzbestimmungen, insbesondere unerlaubte SaaS-Nutzung, werden konsequent verfolgt. 😎

## Kontakt

Weitere Informationen findest du auf: [www.code99.it](https://www.code99.it)
