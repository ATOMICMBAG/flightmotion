# Flightmotion

**Ein technisches Cockpit-Trainingswerkzeug — im Browser als installierbare Web-App, als begehbarer 3D-Rundgang durch ein Hubschrauber-Simulatorzentrum und als natives Unreal-Engine-5.8-Standalone mit Hubschrauber-Vehicle.**

🔗 **Live-Demo:** [flightmotion.maazi.de](https://flightmotion.maazi.de/)

---

## Worum es geht

Flightmotion ist kein Flugsimulations-*Spiel*, sondern ein Trainingswerkzeug: Es geht um möglichst realistische Systemtiefe — Schalter, Hebel, Zustände, Instrumente, die sich so verhalten wie in einem echten Cockpit — statt um Arcade-Steuerung. Ziel ist, einen niedrigschwelligen Einstieg in die Bedienlogik eines Cockpits zu geben, wahlweise direkt im Browser oder in einer grafisch aufwendigeren Standalone-Version — ergänzt um einen Blick darauf, wie professionelles Simulatortraining für Hubschrauberpiloten räumlich organisiert ist.

Den Anstoß für das Thema gab eine Auseinandersetzung mit dem anhaltenden Strukturwandel der Krankenhauslandschaft in Deutschland und der damit wachsenden Bedeutung der Luftrettung: Seit 1991 ist die Zahl der Krankenhäuser um rund ein Viertel gesunken, während ADAC und DRF Luftrettung 2025 zusammen auf über 85.000 Einsätze kamen — im Schnitt alle sechs Minuten ein Alarm. Der limitierende Faktor ist dabei zunehmend nicht die Flotte, sondern qualifiziertes fliegendes Personal. Die ausführliche Hintergrundrecherche mit Quellenangaben (Statistisches Bundesamt, BMG, RWI, Bertelsmann Stiftung, ADAC/DRF Luftrettung) steht als PDF über die Live-Demo zum Download bereit.

Dieses Repository ist ein privates Lern- und Demonstrationsprojekt.

## Drei Zugänge, ein Trainingsgedanke

| | Simulatorzentrum 3D | Flightmotion im Browser | Flightmotion für Unreal Engine 5.8 |
|---|---|---|---|
| **Zugang** | Sofort im Browser, VR-fähig (WebXR) | Sofort im Browser, als PWA installierbar | Kompilierte Desktop-Version (Windows/Linux) |
| **Ziel** | Trainingsumgebung erleben: Hallen, Simulatoren, Cockpit, Trainerplatz | Niedrigschwellig, ohne Installation, auch mobil | Höhere visuelle und physikalische Detailtreue |
| **Inhalt** | Vollflug- und Kuppelsimulatoren, mobile Flugchassis, begehbares Cockpit | Flugzeug-Cockpit | Wählbares Hubschrauber-Vehicle |
| **Verfügbarkeit** | [Direkt online](https://flightmotion.maazi.de/halle/) | [Direkt online](https://flightmotion.maazi.de/sim/) | Download über die Live-Demo |

### Simulatorzentrum 3D

Ein Rundgang durch ein nachempfundenes Trainingszentrum für Hubschrauberpiloten: In einer Halle stehen drei Vollflugsimulatoren auf Bewegungsplattformen (Hexapods), erreichbar über eine Galerie mit Brücken zu den Kabinen; in einer zweiten Halle zwei Kuppelsimulatoren mit großer Projektionssphäre und mobile Flugchassis, die je nach Trainingsmuster gewechselt werden. Im Inneren eines Simulators lässt sich das Cockpit samt Trainerplatz begehen — die Außensicht wird, wie im realen Vorbild, auf die Kuppel projiziert.

Die Szene ist eine freie Nachbildung; Hersteller- und Typbezeichnungen (Skypool, Epos, Mixer) sind fiktiv, alle Texturen und Beschriftungen wurden eigens erzeugt.

### Gemeinsame Grundidee

Browser- und Unreal-Version teilen dieselbe Grundidee: ein datengetriebenes Cockpit, in dem jeder Schalter, Hebel und jede Anzeige einem klar definierten, wiederverwendbaren Aktor-Zustand entspricht — 3D-Interaktion und Anzeige laufen dabei nie auseinander, weil beide denselben Zustand spiegeln.

### Impressionen (Unreal-Engine-Version)

<p>
  <img src="https://flightmotion.maazi.de/unreal_engine/screenshots/flightmotion_1.png" width="32%" alt="Flightmotion Unreal Engine Screenshot 1" />
  <img src="https://flightmotion.maazi.de/unreal_engine/screenshots/flightmotion_3.png" width="32%" alt="Flightmotion Unreal Engine Screenshot 3" />
  <img src="https://flightmotion.maazi.de/unreal_engine/screenshots/flightmotion_5.png" width="32%" alt="Flightmotion Unreal Engine Screenshot 5" />
</p>

Weitere Screenshots und der Download befinden sich im Abschnitt „Selbst ausprobieren“ auf [flightmotion.maazi.de](https://flightmotion.maazi.de/).

## Technik im Überblick

**Web-App (Browser-Version)**

- **Frontend:** TypeScript, [Svelte 5](https://svelte.dev/) (Runes-API) über [Babylon.js](https://www.babylonjs.com/) als 3D-Engine für das Cockpit; Vite als Build-Tool, als PWA installierbar (Offline-Shell, App-Icon).
- **Backend:** Node.js mit [Fastify](https://fastify.io/), PostgreSQL über [Prisma](https://www.prisma.io/) als ORM, JWT-basierte Authentifizierung.
- **Architektur:** Ein datengetriebenes Aktor-Modell bildet jeden Schalter, Hebel und jede Anzeige generisch ab — 3D-Interaktion, Detail-Panel und Telemetrie greifen auf denselben Zustand zu, statt eigene Spezialfälle pro Bauteil zu benötigen. Das hält den Aufwand für zusätzliche Instrumente in erster Linie zu einem Inhalts-, nicht zu einem Code-Thema.
- **Betrieb:** Eigener VPS, Prozessverwaltung über PM2, Auslieferung über einen Reverse Proxy.

**Simulatorzentrum 3D**

- **Modellierung:** [Blender](https://www.blender.org/) 5.2, gesteuert über die MCP-Server-Integration aus dem Blender Lab. Die komplette Welt — Hallen, Simulatoren, Hexapods, Treppen, Schläuche, Cockpit — entsteht prozedural aus einem Python-Generator und lässt sich jederzeit reproduzierbar neu erzeugen.
- **Austauschformat:** Ein einziges glTF-Binary (GLB) dient zugleich der Web-App und als Grundlage für die Unreal-Engine-Version — Änderungen am Modell fließen so ohne Konvertierungsschritte in beide Welten.
- **Darstellung:** Babylon.js mit Kamerapunkten und Infotexten, Orbit-Ansicht mit von außen durchsichtigen Hallen, freiem Begehen (WASD, optional mit Schwerkraft) und VR-Teleport über WebXR, sobald eine Brille erkannt wird.

**Unreal-Engine-Version**

- **Engine:** Unreal Engine 5.8.
- **Fokus:** Höhere Render- und Physik-Qualität als im Browser realistisch möglich, mit wählbarem Hubschrauber-Vehicle.
- Folgt demselben Grundprinzip datengetriebener, klar definierter Cockpit-Zustände wie die Web-Version.

## Status

Das Projekt befindet sich in aktiver Entwicklung. Die Live-Demo ist online und wird laufend um weitere Aktoren, Instrumente und Trainingsinhalte erweitert.

Der Quellcode dieses Repositories wird veröffentlicht, sobald ein stabiler Funktionsumfang erreicht ist. Bis dahin dient dieses README als Projektübersicht — eine ausführliche technische Bauanleitung folgt mit der Code-Veröffentlichung.

## Lizenz

Wird mit der Code-Veröffentlichung ergänzt.

---

© 2026 Flightmotion — ein privates Lern- und Demonstrationsprojekt.
