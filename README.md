# Node-RED Worldmap Human Tracker

Diese Node-RED-Flow bietet eine interaktive Weltkarte, auf der Benutzer "Humans" generieren und deren zufällige Bewegungen auf der Karte in Wien verfolgen können. Die Karte zeigt auch Verbindungslinien zwischen den Punkten und bietet die Möglichkeit, Zeichnungen und Geofences zu erstellen und zu verwalten.

## Features
**Weltkarte**: Eine ansprechende farbige Weltkarte mit Fokus auf Wien.  
**Zoomlevel**: Angepasstes Zoomlevel für eine bessere Übersicht der Stadt Wien.  
**UI-Layout**: Breite Ansicht der Karte in der UI.    
**Spawn Human Button**: Ein Button, der einen Menschen mit einem spezifischen Icon an vordefinierten Koordinaten auf der Karte erstellt.  
**Bewegungstracking**: Jeder "Human" bewegt sich zufällig, um menschliche Aktivität zu simulieren.  
**Verbindungswege**: Zeichnet Linien zwischen den Bewegungspunkten, um einen Pfad darzustellen.  
**Poly-Tools**: Ermöglicht das Zeichnen und Löschen von Polygonen auf der Karte, die im Flow-Speicher verwaltet werden.  
**GeoFence Integration**: Verknüpfung der Karte mit GeoFence-Funktionen zur Bereichsüberwachung.  

## Installation
Stellen Sie sicher, dass Sie Node-RED bereits auf Ihrem System installiert haben. Importieren Sie dann die bereitgestellte .json-Flow-Datei in Ihre Node-RED-Instanz.

## Konfiguration
- Fügen Sie einen worldmap-Node hinzu, um Ihre Karte zu initialisieren.
- Setzen Sie den Mittelpunkt auf Wien mit den Koordinaten 48.239068, 16.377577.
- Wählen Sie ein ansprechendes Karten-Theme aus und stellen Sie das Zoomlevel ein.

## UI-Layout
Passen Sie die Breite der Weltkarte in der Dashboard-Konfiguration an (20).
### Spawn Human Button
Erstellen Sie einen Dashboard-Button, der eine Funktion zum Generieren von Menschen auslöst.

### Menschliche Bewegung
Passen sie Ihrem Flow eine Funktion hinzu, die die untenstehende Logik verwendet, um die Koordinaten der Menschen zu aktualisieren:

## Verbindungswege (Tracks)

Konfigurieren Sie einen weiteren Node, um Verbindungswege zwischen den Bewegungspunkten zu zeichnen.


## Poly-Tools
- Verwenden Sie eine Funktion, um auf die draw und drawdelete Events von der Weltkarte zu hören.
- Speichern und löschen Sie Polygone entsprechend im Flow-Speicher.

## GeoFence
Integrieren Sie GeoFence, um spezifische Bereiche auf der Karte zu überwachen und Ereignisse basierend auf dem Eintritt/Austritt der Menschen zu generieren.

