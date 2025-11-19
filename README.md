## ️ Projektbeschreibung

*Vernetztes System – Containerisierte Entwicklungs- und Testumgebung*

**Kurzbeschreibung:**
In vielen Entwicklungsprojekten fehlt eine klar strukturierte und wiederholbare Entwicklungs- sowie Testumgebung, die alle Dienste konsistent orchestriert – was zu Zeitverlusten, Konfigurationsdrift und Fehlern führt.
Das Projekt ist ein skalierbares Entwicklungs- und Test-Setup mithilfe von Docker-Containern zur effizienten Integration und Service-Orchestrierung, das sowohl Backend- als auch Frontend-Anforderungen vollständig unterstützt.

**Tech-Stack:**

* Docker (Container)
* Services: z. B. W. MariaDB, Apache HTTP Server, HAProxy, LateX-Server, Tomcat.
* Skripte zur Automatisierung: init.sh, run-all.sh, undeploy.sh 
* Versionsverwaltung via Git / GitHub

Durch den Aufbau einer containerisierten Umgebung wurden alle relevanten Dienste in isolierten Containern aufgesetzt.
Ein zentrales Skript („run-all.sh“) stellt die Umgebung mit einem Schritt bereit, automatisiert den Start und stellt sicher, dass die Umgebung reproduzierbar ist.

**Architekturübersicht (leicht verständlich):**

* Jeder Dienst läuft in einem eigenen Docker-Container.
* Der Load-Balancer (HAProxy) verteilt ggf. Last auf Applikationsserver (Apache und Tomcat je nach Anfrage).
* Der Webserver (Apache) dient als Frontdoor oder statisches Asset-Server.
* Die Datenbank (MariaDB) stellt persistente Speicherung bereit.
* Skripte übernehmen das Starten, Stoppen und Entfernen der Umgebung, wodurch Setup-Zeit drastisch reduziert wird.
* Kommunikation zwischen den Containern erfolgt über Docker-Netzwerke, womit Dienste sauber voneinander isoliert sind.

Alles klar — hier ist ein **komplett neues, professionelles und strukturiertes README.md** für dein Projekt.
Du kannst es **eins-zu-eins** in dein Repository übernehmen.

*Eine containerisierte Multi-Service-Systemlandschaft für Entwicklung, Test und Demonstration*

## **Enthaltene Services**

### **1. Apache Webserver (`apache/`)**

* Eigener Docker-Build
* Unterstützt CGI-Skripte & PHP
* Beispiel-Frontend (`html/index.html`)
* CGI-Skripte z. B.:
    * `adder.sh` (Rechenoperationen)
    * `moin.sh` (Dynamische Ausgabe)
    * `namefromdb.sh` (Datenbankabfrage)

* Eigene Konfiguration (`000-default.conf`)
* Init- und Run-Skripte zur Automatisierung

### **2. HAProxy Load-Balancer (`haproxy/`)**

* Individueller Docker-Container
* Routing zu Tomcat-Services
* Konfiguriert über `haproxy.cfg`
* Logging & Startskripte


### **3. MariaDB Datenbank (`mariadb/`)**

* Eigener MariaDB-Container
* Eigene DB-Konfiguration (`my.cnf`)
* Initialisierungsskripte (`myinit.sh`)
* Automatischer Start über `run.sh`
* Bereitstellung persistenter Daten


### **4. Tomcat Applikationsserver (`tomcat/`)**

* Individuelles Tomcat-Image
* Enthält:

    * Tomcat 10.1.x
    * Jakarta EE API
    * JDBC-Treiber
* Spezial-Konfiguration:

    * `server.xml`, `server-new.xml`
    * `context.xml`, `tomcat-users.xml`
* Automatisierte Downloads & Setup
* Backend-Service-Simulation

### **5. LaTeX-PDF-Service (`latex/`)**

* Vollständige LaTeX-Engine im Container
* Generiert PDF-Dokumente aus TeX-Vorlagen
* Tools & Skripte:

    * `genpdf.sh`
    * `gensimple.sh`
    * `testlong.sh`
* Beispielvorlagen im Ordner `letter/`
* Eingebaute Schriftarten (Lora, Poppins)

### **6. Worker-System mit FIFO-IPC (`work/`)**

* Demonstriert Interprozesskommunikation über Named Pipes (FIFOs)
* Services:

    * `sender.sh`
    * `listener.sh`
    * `interpreter.sh`
    * `abarbeiter.sh`
* Pipelines & Automatisierte Tests (`testordner/`)

## **Orchestrierung & Steuerung**

### **Start aller Services**

```bash
./run-all.sh
```

Startet alle Container, setzt Netzwerk & IP-Adressen und initialisiert jeden Service automatisch.

### **Initialisierung**

```bash
./init.sh
```

Bereitet Ordner, Berechtigungen und sonstige Systemvoraussetzungen vor.

### **Umgebung vollständig stoppen & entfernen**

```bash
./undeploy.sh
```

### **Logging**

Jeder Container schreibt Logs nach:

```
*/outer/<service-name>/docker.log
```

##  **Architekturübersicht**

```text
┌───────────────┐       ┌──────────────┐
│   Apache       │  <--  │   HAProxy    │  <--  Client
└───────┬───────┘       └──────┬───────┘
        │                       │
        ▼                       ▼
   CGI/PHP App             Tomcat Backend
        │                       │
        └──────────┬────────────┘
                   ▼
              MariaDB
                   
LaTeX-Service & Worker-System laufen separat und können von Apache/Tomcat genutzt werden.
```

##  **Technologien**

* Docker & Docker-Networking
* Bash/Shell-Skripte
* Apache HTTP Server
* HAProxy
* MariaDB
* Tomcat 10
* LaTeX / TeX-Engine
* Named Pipes (FIFO IPC)
* Linux-Server-Struktur
* Git

##  **Zweck des Projekts**

* Bereitstellung einer realitätsnahen Multi-Service-Architektur
* Demonstration von Backend-Integration
* Testing von Datenbank-Kommunikation
* Simulation eines Full-Stack-Systems
* PDF-Erstellung über Containerservices
* Experimentieren mit IPC-Mechanismen
* Automatisierte Setup-/Teardown-Prozesse
