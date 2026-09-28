# Flightmotion

**Ein technisches Cockpit-Trainingswerkzeug — im Browser als installierbare Web-App und als natives Unreal-Engine-5.8-Standalone mit Hubschrauber-Vehicle.**

🔗 **Live-Demo:** [flightmotion.maazi.de](https://flightmotion.maazi.de/)

---

## Worum es geht

Flightmotion ist kein Flugsimulations-*Spiel*, sondern ein Trainingswerkzeug: Es geht um möglichst realistische Systemtiefe — Schalter, Hebel, Zustände, Instrumente, die sich so verhalten wie in einem echten Cockpit — statt um Arcade-Steuerung. Ziel ist, einen niedrigschwelligen Einstieg in die Bedienlogik eines Cockpits zu geben, wahlweise direkt im Browser oder in einer grafisch aufwendigeren Standalone-Version.

Den Anstoß für das Thema gab eine Auseinandersetzung mit dem anhaltenden Strukturwandel der Krankenhauslandschaft in Deutschland und der damit wachsenden Bedeutung der Luftrettung: Seit 1991 ist die Zahl der Krankenhäuser um rund ein Viertel gesunken, während ADAC und DRF Luftrettung 2025 zusammen auf über 85.000 Einsätze kamen — im Schnitt alle sechs Minuten ein Alarm. Der limitierende Faktor ist dabei zunehmend nicht die Flotte, sondern qualifiziertes fliegendes Personal. Die ausführliche Hintergrundrecherche mit Quellenangaben (Statistisches Bundesamt, BMG, RWI, Bertelsmann Stiftung, ADAC/DRF Luftrettung) steht als PDF über die Live-Demo zum Download bereit.

Dieses Repository ist ein privates Lern- und Demonstrationsprojekt.

## Zwei Varianten, ein Trainingsgedanke

| | Flightmotion im Browser | Flightmotion für Unreal Engine 5.8 |
|---|---|---|
| **Zugang** | Sofort im Browser, als PWA installierbar | Kompilierte Desktop-Version (Windows/Linux) |
| **Ziel** | Niedrigschwellig, ohne Installation, auch mobil | Höhere visuelle und physikalische Detailtreue |
| **Vehicle** | Flugzeug-Cockpit | Wählbares Hubschrauber-Vehicle |
| **Verfügbarkeit** | [Direkt online](https://flightmotion.maazi.de/) | Download über die Live-Demo |

Beide Varianten teilen dieselbe Grundidee: ein datengetriebenes Cockpit, in dem jeder Schalter, Hebel und jede Anzeige einem klar definierten, wiederverwendbaren Aktor-Zustand entspricht — 3D-Interaktion und Anzeige laufen dabei nie auseinander, weil beide denselben Zustand spiegeln.

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
