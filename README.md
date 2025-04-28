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

Node 1:

Node 2:
git clone git@github.com:Code99it/pulse.git ~/pulse-stack
cd ~/pulse-stack
docker stack deploy -c docker-compose.yml pulse

Node 3:
git clone git@github.com:Code99it/pulse.git ~/pulse-stack
cd ~/pulse-stack
docker stack deploy -c docker-compose.yml pulse

## Lizenz

Dieses Projekt steht unter der [Business Source License 1.1](LICENSE).  
Das exklusive Recht zur öffentlichen Bereitstellung als SaaS liegt bei Code99 (Christian Wilhelm).

Hinweis: Verstöße gegen die Lizenzbestimmungen, insbesondere unerlaubte SaaS-Nutzung, werden konsequent verfolgt. 😎

## Kontakt

Weitere Informationen findest du auf: [www.code99.it](https://www.code99.it)
