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

