# DevOps 09 Deployment Docker
| | |
| -------- | ------- |
| Mein Repository | [Mein GitHub-Repo](https://github.com/tercabey/DevOps-09-Deployment-Docker) |
| Zusammenarbeit mit | Gedik, Hande |
| Repo URL ÜbungspartnerIn | [Repository auf GitHub](https://github.com/gedikhan/DevOps-09-Deployment-Docker) |

## Lernjournal

### 1. Vorbereitung des Repositories
- Repository [DevOpsNodeWebApp](https://github.com/Beyzatrcn/DevOpsNodeWebApp.git) auf GitHub forked und mit VS-Code verknüpft.

### 2. Jenkins-Konfiguration (lokal)
- Jenkins lokal über Docker gestartet.
- Docker-Socket verbunden (`tcp://host.docker.internal:2375`).

### 3. Jenkins-Build-Job erstellt: `DevOpsNodeWebAppDockerBuild`
- Aufgabe: Docker-Image lokal bauen mit dem Tag `beyzatrcn/node-web-app`.
- Build-Kontext: `$WORKSPACE`.
- Docker-Plugin verwendet.

### 4. Jenkins-Deploy-Job erstellt: `DevOpsNodeWebAppDockerDeploy`
- Aufgabe: Container aus gebautem Image starten.
- Port 3000:3000 gesetzt.
- Trigger: Startet nach erfolgreichem Build-Job.

### 5. Jenkins-Render-Job erstellt: `DevOpsNodeWebAppRenderDeploy`
- Aufgabe: Deployment bei Render.com triggern.
- Schritte:
  - Checkout
  - Docker Push nach DockerHub
  - API-Call an Render Deployment Endpoint.
- Trigger: Startet nach erfolgreichem Deploy-Job.

### 6. Jenkins RenderDeploy erfolgreich

![Jenkins RenderDeploy](Screenshots/Jenkins_DevOpsNodeWebAppRenderDeploy_ausgeführt.png)


### 7. Jenkins-Triggerkette

- Build-Triggers korrekt konfiguriert:

  ![Trigger DevOpsNodeWebAppDockerDeploy nach Build](Screenshots/Starte_DevOpsNodeWebAppDockerDeploy_nachdem_DevOpsNodeWebAppDockerBuild.png)

### 8. Jenkins prüft regelmässig Änderungen

![Alle 2 Minuten](Screenshots/Alle_2_min_abfragen_Build_Trigger.png)

### 9. DockerHub Repository
- Name: `tercabey/node-web-app`.
- Image wird mit `--platform linux/amd64` gepusht (kompatibel mit Render).

### 10. Render.com Konfiguration
- Neues Web Service erstellt mit bestehendem Docker-Image (`tercabey/node-web-app:latest`).
- Zugang mit DockerHub-Credentials.
- Deployment wird ausgelöst durch Render-Pipeline von Jenkins.

### 11. End-to-End-Test

- Änderung in `server.js` vorgenommen (z. B. "Test: Build Trigger").
- Commit und Push nach GitHub mit VS Code durchgeführt:
- Jenkins erkennt die Änderung, Build wird automatisch angestossen:
- Container wird aktualisiert und läuft lokal auf Port 3000:

  ![Container läuft](Screenshots/tercabey-web-app-container_verfügbar.png)
  
  ![WebApp läuft lokal](Screenshots/WebApp_lokal_ist_online.png)

- Änderung auf WebApp sichtbar:

  ![Änderung sichtbar](Screenshots/Test_Build_Trigger_auf_Webapp_ersichtlich.png)

### 12. Docker Image auf DockerHub veröffentlicht

![DockerHub Repository](Screenshots/docker_Repo_published_tercabey:node-web-app.png)

### 13. Automatisiertes Deployment bei Render und auf Cloud

- Die App wird nach dem Push bei DockerHub automatisch bei Render.com deployed.
- Die Render-Instanz ist live:

  ![Render-Deployment](Screenshots/render_node_web_app_devops_tercabey_online.png)

- Die App auf Cloud ist live:

  ![Render auf Cloud](Screenshots/Render_auf_Cloud.png)


