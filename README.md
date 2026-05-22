# m300 – Plattformübergreifende Dienste in ein Netzwerk integrieren

Lernender: David Martin Felicio Reichlin


---

## Übersicht

Dieses Repository enthält alle Artefakte für das Modul-300-Projekt.  
Ziel ist der Aufbau einer vollständigen CI/CD-Pipeline mit automatisiertem  
Deployment auf einem Kubernetes-Cluster (k3s).

Da der Fokus auf der CI/CD-Pipeline und dem Kubernetes-Cluster liegt, ist eine simple app enthalten, die mit python und
flask aufgebaut ist und redis und sqlite verwendet.

**Tech-Stack:**

- GitHub Actions – CI/CD-Pipeline
- Docker – Containerisierung der Applikation
- k3s – Kubernetes-Cluster (lokal)
- GitHub Container Registry (GHCR) – Image Registry
- Minimale Flask-App (Link Shortener) - App zu deployen

---

## Projektstruktur

**Wird laufend ausgefüllt**

```
C:.
│   README.md
├───.github
│   └───workflows
│           ci-cd.yml
└───docs
        arbeitsjournal.md
        konzept.md
        projektanforderungen.md
        reflexion.md
        testprotokoll.md
```

---

## Dokumentation

| Dokument                                             | Beschreibung                                   |
|------------------------------------------------------|------------------------------------------------|
| [Projektanforderungen](docs/projektanforderungen.md) | Auftrag, Ziele, Bewertungsraster               |
| [Konzept](docs/konzept.md)                           | Architekturdiagramm, technische Entscheidungen |
| [Arbeitsjournal](docs/arbeitsjournal.md)             | Fortschritt pro Arbeitsphase                   |
| [Testprotokoll](docs/testprotokoll.md)               | Durchgeführte Tests und Ergebnisse             |

---

## Schnellstart (lokal)

### Voraussetzungen

- Docker Desktop oder Rancher Desktop
- k3s installiert (`curl -sfL https://get.k3s.io | sh -`)
- kubectl konfiguriert
- Git

### App lokal starten (Docker Compose)

```bash
git clone https://github.com/reidavid/m300.git
cd m300
docker compose up
```

### Auf Kubernetes deployen

```bash
kubectl apply -f k8s/
kubectl get pods
kubectl get services
```

---

## CI/CD-Pipeline

Die Pipeline wird automatisch ausgelöst bei jedem Push auf den `main`-Branch.

```
Push auf main >>
Tests ausführen >>
Docker Image bauen & taggen >>
Image pushen → GHCR >>
Deploy auf k3s-Cluster >>
```

Pipeline-Konfiguration: [`.github/workflows/ci-cd.yml`](.github/workflows/ci-cd.yml)

---

## Kubernetes

Der Cluster besteht aus folgenden Komponenten:

| Ressource  | Datei                 | Beschreibung                       |
|------------|-----------------------|------------------------------------|
| Deployment | `k8s/deployment.yaml` | App mit 2 Replicas, Rolling Update |
| Service    | `k8s/service.yaml`    | Interner Zugriff auf die Pods      |
| Ingress    | `k8s/ingress.yaml`    | Externes Routing                   |
| ConfigMap  | `k8s/configmap.yaml`  | Umgebungsvariablen                 |
| Secret     | `k8s/secret.yaml`     | Sensible Konfigurationswerte       |

Status prüfen:

```bash
kubectl get all -n default
```

---

## Arbeitsjournal

Das Arbeitsjournal wird laufend in [`docs/arbeitsjournal.md`](docs/arbeitsjournal.md) geführt.  
Jede Arbeitsphase enthält: Datum, geleistete Arbeit, Probleme und Lösungen und eine kurze Reflexion.

---

## Projektanforderungen

Die vollständigen Projektanforderungen (Auftrag, Lieferobjekte, Bewertungsraster)  
sind unter [`docs/projektanforderungen.md`](docs/projektanforderungen.md) zu finden.

---

## Reflexion

> Wird am Ende des Projekts in [`docs/reflexion.md`](docs/reflexion.md) ergänzt.

---

*Modul 300 - Plattformübergreifende Dienste in ein Netzwerk integrieren | Technische Berufsschule Zürich*