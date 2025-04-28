# Deployment

Willkommen beim offiziellen Deployment des Pulse-Projekts von Code99.

## Inhalt

- Produktionsbereites Deployment
- Load Balanced Service für mehrere Webserver
- Zukunftssicher ausgelegt für Autoscaling und Failover

## Nutzung

- Eigene Installation auf privaten oder internen Servern ist gestattet.
- Öffentliche SaaS-Angebote basierend auf diesem Code sind **nicht** erlaubt (siehe Lizenz).

Installation auf 3 VPS

Folge diesen Schritten, um deine Pulse-Infrastruktur auf drei Debian 12-VPS-Instanzen einzurichten:

1. Voraussetzungen
Drei Debian 12-Server mit öffentlicher und privater IP
VPS 1: z. B. vps1.example.com / 10.0.0.1
VPS 2: z. B. vps2.example.com / 10.0.0.2
VPS 3: z. B. vps3.example.com / 10.0.0.3
Auf jedem Server:
SSH-Zugang mit Root-Rechten
Firewall geöffnet für Ports: 2377, 7946, 4789, 80, 81, 443, 26257
GitHub-Repo Code99it/pulse mit folgenden Dateien und Verzeichnissen:
pulse/
├── docker-compose.yml
└── nginx/
└── conf.d/
└── default.conf

3. Git-Repo klonen
Auf allen drei VPS ausführen:
git clone git@github.com:Code99it/pulse.git ~/pulse
cd ~/pulse

4. Docker installieren
Auf jedem VPS:
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
echo "deb [arch=amd64] https://download.docker.com/linux/debian bookworm stable" \
| sudo tee /etc/apt/sources.list.d/docker.list
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
Optional: Nutzer zur Docker-Gruppe hinzufügen
sudo usermod -aG docker $USER

5. Swarm-Cluster initialisieren
Nur auf VPS 1 ausführen:
docker swarm init --advertise-addr <PRIVATE_IP_VPS1>
Notiere dir den angezeigten Join-Befehl.

Auf VPS 2 und VPS 3 ausführen:
docker swarm join \
--token SWMTKN-1-… \
<PRIVATE_IP_VPS1>:2377

5. Overlay-Netzwerke anlegen
Zurück auf VPS 1:
docker network create --driver overlay frontend
docker network create --driver overlay backend

6. Stack deployen
Auf VPS 1:
cd ~/pulse
docker stack deploy -c docker-compose.yml pulse

7. CockroachDB initialisieren
Auf VPS 1:
CID=$(docker ps -qf "name=pulse_cockroachdb.1")
docker exec -it $CID cockroach init --insecure

8. Nginx-App testen
Optional: nginx/conf.d/default.conf anpassen
Service neu starten:
docker service update --force pulse_nginx-app
Im Browser aufrufen:
https://<PUBLIC_IP_VPS1>
– Du solltest deine Testseite sehen.

10. Nginx Proxy Manager UI
Zugriff im Browser: http://<PUBLIC_IP_VPS1>:81
Standard-Login: admin@example.com / changeme
Lege unter Proxy Hosts einen Host für pulse.code99.it an
Lege unter Streams einen TCP-Stream für Port 26257 an

Damit läuft deine SaaS-Infrastruktur mit:

3 CockroachDB-Replikaten
3 Nginx-App-Instanzen
1 Nginx Proxy Manager im Docker Swarm

## Lizenz

Dieses Projekt steht unter der [Business Source License 1.1](LICENSE).  
Das exklusive Recht zur öffentlichen Bereitstellung als SaaS liegt bei Code99 (Christian Wilhelm).

Hinweis: Verstöße gegen die Lizenzbestimmungen, insbesondere unerlaubte SaaS-Nutzung, werden konsequent verfolgt. 😎

## Kontakt

Weitere Informationen findest du auf: [www.code99.it](https://www.code99.it)
