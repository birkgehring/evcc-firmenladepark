# AGENTS.md — Codex-Arbeitsauftrag: EVCC Firmenladepark

## Priorität 1: EVCC auf dem LXC-Container installieren und vorführbar machen

**Erster Meilenstein ist eine laufende, im Browser erreichbare EVCC-Instanz auf dem vom Betreiber bereitgestellten Proxmox-LXC-Container.** Nicht zuerst ein eigenes Dashboard oder RFID-Verwaltung entwickeln. Der Betreiber erstellt den LXC parallel und übermittelt anschließend SSH-Zugang beziehungsweise Host/IP, Benutzer, Betriebssystem und erforderliche Berechtigungen.

### Vorgehen
1. Vor Änderungen den Container und vorhandene Dienste prüfen: Linux-Distribution, Architektur, Netzwerk, Rechte, Ports, Speicherplatz. Container-Zugangsdaten nicht ins Git-Repository schreiben.
2. Die offizielle EVCC-Dokumentation und das Upstream-Projekt https://github.com/evcc-io/evcc sowie aktuelle Installationsvoraussetzungen prüfen; eine für die LXC-Umgebung geeignete, wartbare Installationsart wählen. Keine veralteten Installationsbefehle blind übernehmen.
3. EVCC installieren, einen persistenten Konfigurations-/Datenpfad, Autostart (z. B. systemd, sofern unterstützt), Logs und Update-/Backup-Vorgehen einrichten. Keine Secrets committen.
4. EVCC zunächst ohne reale Wallbox-Zugangsdaten so weit wie offiziell unterstützt starten. Test-/Demo-Konfiguration nur verwenden, wenn von EVCC dokumentiert; keinesfalls reale Ladevorgänge vortäuschen. Fehlende Hardware- und Stromtarifdetails als offene Punkte dokumentieren.
5. Start, Dienststatus, Logs, HTTP-Erreichbarkeit und Neustartverhalten überprüfen. Die tatsächliche URL einschließlich Port nennen, sobald die IP bekannt ist. Keine öffentliche Portfreigabe ohne ausdrückliche Freigabe.
6. README.md mit Installationsweg, Voraussetzungen, Bedienung, Zugangs-URL (ohne Zugangsdaten), Konfigurationspfaden, Diagnose-, Update- und Backup-Anleitung erstellen.
7. Bericht mit tatsächlich ausgeführten Schritten, Prüfresultaten, Version und noch benötigten Angaben liefern. Nicht behaupten, die Installation sei abgeschlossen, bevor die Instanz wirklich erreichbar und getestet ist.

**Wichtig:** Wenn der LXC oder SSH-Zugriff noch nicht bereitsteht, bereite überprüfte Installationsskripte und Dokumentation im Repo vor und warte mit der Remote-Installation, bis die Daten zur Verfügung stehen. Keine erfundenen IPs, Zugangsdaten oder Hardwaremodelle.

## Priorität 2: Geräte anbinden und Grundfunktion prüfen
- Welche Wallboxen und wie viele Ladepunkte vorhanden sind, muss noch geklärt werden.
- EVCC mit den tatsächlich vorhandenen, kompatiblen Wallboxen und ggf. Zählern verbinden.
- Prüfen, ob EVCC Ladevorgänge, Leistung und kWh korrekt erfasst. Erst mit Testdaten, dann kontrolliert im realen Betrieb.
- Vor Änderungen der Lade-/Steuerungsparameter Rücksprache halten, damit kein betrieblicher Ladebetrieb unerwartet unterbrochen wird.

## Priorität 3: Firmenladepark-Funktionen (nach lauffähiger EVCC-Basis)
Die Anforderungen sind fachlich besprochen, aber **noch keine Freigabe für eine bestimmte Architektur**. Technische Möglichkeiten und Grenzen von EVCC, seinen Schnittstellen, Lizenzbedingungen und der Wallbox-Hardware zuerst prüfen.

- Mehrere Ladeboxen; eine Ladebox kann heute von Frau Müller und morgen von jemand anderem benutzt werden.
- Jeder Mitarbeiter nutzt im Ausgangsfall ein festes, personenbezogenes Firmenfahrzeug und einen eigenen RFID-Chip. Datenmodell später für Fahrzeug-/Chipwechsel erweiterbar.
- Jede Ladesitzung soll, soweit Hardware/Protokoll die Identifikation ermöglicht, anhand RFID dem Mitarbeiter und Fahrzeug zugeordnet werden — unabhängig davon, an welcher Box geladen wird.
- Keine dauerhafte Zuordnung „Ladebox = Mitarbeiter“. Fehlende RFID-Erkennung transparent als nicht zugeordnet kennzeichnen; keine Identität raten.
- Admin-Auswertungen: kWh und Ladevorgänge je Wallbox (welche Box wird am meisten genutzt?), je Mitarbeiter und je Fahrzeug, einstellbare Zeiträume, nach Möglichkeit Export, optional Kosten.
- Prüfen, wie Ereignisse, Ladehistorie und RFID-/Benutzerinformationen tatsächlich gewonnen werden können; nicht voraussetzen, dass EVCC selbst alle Daten bereitstellt.
- Datenschutz: rollenbasierter Zugriff, keine öffentlichen personenbezogenen Ladedaten, sichere RFID-Verwaltung, angemessene Aufbewahrung und Auditierung.

## Entwicklungsregeln
- Arbeite in klaren Schritten, beginnend mit der Installation. Kleine, überprüfbare Commits.
- Nutze den vorhandenen Stand des Repositories und dokumentiere Entscheidungen.
- Keine Zugangsdaten, Tokens, RFID-Rohwerte oder private Schlüssel in Git.
- Für zusätzliche Software nur nach ermitteltem Bedarf eine wartbare Architektur wählen; keine unnötig große Eigenentwicklung vor der ersten EVCC-Vorführung.
- Bei Unklarheiten zu Hardware, LXC-Zugang oder Netzwerk gezielt fehlende Angaben anfordern.
