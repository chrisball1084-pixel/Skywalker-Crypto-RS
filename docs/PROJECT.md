# Skywalker Crypto RS — technische Projektdokumentation

## Zweck

Skywalker Crypto RS ist eine mobile Web-App zur Relative-Strength- und Marktbreitenanalyse im Kryptomarkt. Sie wird auf dem iPhone genutzt und über GitHub Pages ausgeliefert.

## Source-of-Truth-Regel

- Der aktuelle Code ist maßgeblich dafür, was tatsächlich implementiert ist.
- Dieses Dokument enthält dauerhafte technische Regeln und Architekturwissen.
- Das zugehörige Notion-Dokument ist die Product Source of Truth für neue Ideen, Bugs, offene Anforderungen, Produktentscheidungen und den aktuellen Produktstatus.
- Historische Notion-Changelogs nur lesen, wenn sie für die aktuelle Aufgabe relevant sind.

## Architektur

Die App besteht aktuell aus einer einzelnen `index.html` mit HTML, CSS und JavaScript. Änderungen müssen deshalb besonders vorsichtig und lokal erfolgen, um unbeabsichtigte Seiteneffekte zu vermeiden.

Hosting erfolgt über GitHub Pages auf dem `master`-Branch.

## Daten und externe Quellen

Die App arbeitet mit Marktdaten und berechnet Relative-Strength-/Breadth-Auswertungen clientseitig. Im bisherigen Produktkontext sind insbesondere folgende Bereiche relevant:

- Relative Strength von Kryptowährungen
- Bitcoin als zentrale Vergleichs-/Marktreferenz in mehreren Auswertungen
- ETH/BTC-Auswertung als eigener Sonderfall
- Altcoin-Breadth, unter anderem als Anteil von Coins, die relativ zu BTC Stärke zeigen
- historische Kursdaten und lokaler Cache, damit Auswertungen nicht bei jedem Aufruf vollständig neu geladen werden müssen

Konkrete Datenanbieter, Endpunkte, Zeitfenster und Berechnungsparameter immer aus dem aktuellen Code lesen. Keine veralteten Werte aus Notion oder alten Chats übernehmen.

## Dauerhafte technische Regeln

### Validierte Logik schützen

- Bestehende RS- und Breadth-Berechnungen nicht beiläufig verändern.
- Wenn eine Formel oder ein Benchmark geändert werden soll, zuerst aktuelle Implementierung, Datenbasis und Produktentscheidung prüfen.
- Vergleichswerte, Bezugstage und historische Fenster sind fachlich relevant und dürfen nicht als reine UI-Details behandelt werden.

### Datenkonsistenz

- Historische Reihen müssen zeitlich sauber ausgerichtet sein.
- Sonderreihen wie ETH/BTC dürfen nicht versehentlich wie normale USD-/USDT-Paare behandelt werden, wenn der Code dafür eigene Logik verwendet.
- Breadth-Werte nur aus dem tatsächlich verfügbaren und vorgesehenen Coin-Universum berechnen.
- Fehlende Daten nicht stillschweigend als neutrale/Null-Werte interpretieren, wenn dadurch Rankings oder Breadth verfälscht würden.

### Mobile Web-App / iOS

- Die App ist primär für mobile Nutzung gedacht; Layoutänderungen auf schmalen iPhone-Viewports prüfen.
- iOS kann JavaScript im Hintergrund einfrieren. Keine Funktion als echte Hintergrundausführung dokumentieren, wenn sie technisch nur im Vordergrund zuverlässig läuft.
- Cache- und Reload-Verhalten bei Änderungen an Datenlogik berücksichtigen.

## Sicherheit

- Keine API-Keys, Tokens oder Secrets in Git, README, Agent-Dateien oder Notion speichern.
- Falls ein Nutzer-Schlüssel benötigt wird, soll er lokal auf dem Gerät gespeichert/eingegeben werden, sofern die bestehende Architektur das so vorsieht.
- Bereits exponierte Secrets sind zu rotieren statt nur aus der Dokumentation zu entfernen.

## Tests und Validierung

Das Repository enthält derzeit keine standardisierte Test-Suite als eigene Dateien. Deshalb bei Änderungen mindestens:

1. Syntax-/Laufzeitfehler im betroffenen Code prüfen.
2. Betroffene Berechnung mit bekannten Beispieldaten oder bestehenden Referenzwerten validieren.
3. Mobile Darstellung prüfen, wenn UI betroffen ist.
4. Lade-/Cache-Verhalten prüfen, wenn Datenabruf betroffen ist.
5. Keine feste Testzahl in Agent-Dokumentation eintragen.

Wenn künftig automatisierte Tests ergänzt werden, diese hier als dauerhaften Workflow dokumentieren.

## Deployment

Live-App:

`https://chrisball1084-pixel.github.io/Skywalker-Crypto-RS/`

Vor einem Release den aktuellen Branch-/GitHub-Pages-Mechanismus prüfen. Keine Deployment-Annahmen aus anderen Skywalker-Projekten übertragen, wenn sie hier nicht im Code/Repo bestätigt sind.

## Notion-Sync-Workflow

Der Befehl **„Notion Sync durchführen“** bedeutet:

1. `AGENTS.md` bzw. `CLAUDE.md` und dieses Dokument lesen.
2. Im Notion Product Hub primär `CURRENT STATE`, `INBOX`, `OPEN` und relevante `PRODUCT DECISIONS` lesen.
3. Historisches Archiv nur bei Bedarf heranziehen.
4. Neue Anforderungen gegen den aktuellen Code verifizieren.
5. Als Bug, Feature, Verbesserung, Frage oder Nutzerentscheidung klassifizieren.
6. Klar definierte Änderungen klein und nachvollziehbar implementieren.
7. Relevante Berechnungen, Datenabrufe und mobile Darstellung validieren.
8. Dieses Dokument nur bei dauerhaft relevanten technischen Änderungen aktualisieren.
9. Notion aufräumen und Status/Changelog kompakt aktualisieren.
10. Abschließend Änderungen, Validierung und offene Entscheidungen berichten.
