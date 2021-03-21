# Jupyter Docker Notebook Matlab OnRamp x Python

Das hier ist ein lokales Jupyter Notebook für den Matlab OnRamp Kurs.
Ich habe mit diesem Projekt versucht, alle OnRamp Kurse von Matlab in Python umzuschreiben.

Verwendet wird die Python Version > 3.9

Das Projekt wurde im Zuge der Übung und Vorlesung Kontinuierliche Simulation an der TU Wien erstellt und dient nur zum Zweck des Selbststudiums.

## Installation

1. Docker installieren: [Windows](https://docs.docker.com/docker-for-windows/install/), [Linux](https://docs.docker.com/engine/install/), [Mac](https://docs.docker.com/docker-for-mac/install/)

2. Empfohlen: Docker-Compose installieren: (Windows und Mac bereits im Client enthalten), [linux](https://docs.docker.com/compose/install/)

3. Dieses Repository klonen. Dafür muss [git installiert](https://git-scm.com/book/de/v2/Erste-Schritte-Git-installieren) sein.

```console
git clone git@github.com:marcomaiermm/KontinuierlicheSimulationTUWien.git
```

4. Docker Container hochfahren

(Empfohlen) Mit Docker-Compose

```console
docker-compose up --build -d
```

Ohne Docker-Compose:

```console
docker build -t jupyter-konti .
docker run -dp 8888:8888 jupyter-konti -v "./notebooks/:/home/jovyan/work" -c "start.sh jupyter lab --LabApp.token=''"
```

Der Container sollte nun laufen und unter <http://localhost:8888> erreichbar sein.

## Nutzung

Um das Notebook zu benutzen, gehe nach der Installation auf <http://localhost:8888>. Dort siehst du in der linken Navigation bereits alle Notebooks aus dem ./notebooks/ Ordner.

Der Ordner ./notebooks/ ist als "volume" mit den Jupyter Docker Container verbunden. Neu erstelle Notebooks erscheinen dort. Du kannst diese hier auch löschen oder herauskopieren.

## Konfiguration

### Port

Der Port über den die App erreichbar ist kann natürlich geändert werden.

./docker-compose.yml

```docker-compose
ports:
    - "8888:8888"
```

Port mapping: Linker Port ist sichtbarer Port außerhalb des Containers. Rechter Port ist der "verbundene" Port, der auf den Linken Port umgeschrieben wird.
Beispielsweise:

```docker-compose
ports:
    - "10000:8888"
```

Um die Änderungen wirksam zu machen:

```console
docker-compose down && docker-compose up -d
```

Das Notebook ist nun unter <http://localhost:10000> erreichbar.

Ohne Docker-Compose:

```console
docker run -dp 10000:8888 jupyter-konti -v "./notebooks/:/home/jovyan/work" -c "start.sh jupyter lab --LabApp.token=''"
```
