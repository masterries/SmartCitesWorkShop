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

```javascript
// Initial coordinates
var latitude = flow.get('latitude') || 48.239068;
var longitude = flow.get('longitude') || 16.377577;

msg.payload = {
    name: "male",
    lat: latitude,
    lon: longitude,
    icon: "male",
    layer: "drawing"
};

return msg;


```

### Menschliche Bewegung
Passen sie Ihrem Flow eine Funktion hinzu, die die untenstehende Logik verwendet, um die Koordinaten der Menschen zu aktualisieren:

```javascript
// Random shift
var randomLatShift = (Math.random() - 0.5) * 0.001;
var randomLonShift = (Math.random() - 0.5) * 0.001;

latitude += randomLatShift;
longitude += randomLonShift;

flow.set('latitude', latitude);
flow.set('longitude', longitude);


```

## Verbindungswege (Tracks)

Konfigurieren Sie einen weiteren Node, um Verbindungswege zwischen den Bewegungspunkten zu zeichnen.


## Poly-Tools
- Verwenden Sie eine Funktion, um auf die draw und drawdelete Events von der Weltkarte zu hören.
- Speichern und löschen Sie Polygone entsprechend im Flow-Speicher.

```javascript
if (msg.payload.action === "draw" && msg.payload.type === "Rectangle") {
    flow.set('polygon', msg.payload.area);
}
else if (msg.payload.action === "drawdelete") {
    flow.set('polygon', null);

}
```


## GeoFence
Integrieren Sie GeoFence, um spezifische Bereiche auf der Karte zu überwachen und Ereignisse basierend auf dem Eintritt/Austritt der Menschen zu generieren.


```javascript
const point = [msg.payload.lat, msg.payload.lon];
const polygon = flow.get('polygon') || [];


function isPointInPolygon(point, polygon) {
    let isInside = false;
    let x = point[1], y = point[0];

    for (let i = 0, j = polygon.length - 1; i < polygon.length; j = i++) {
        let xi = polygon[i].lng, yi = polygon[i].lat;
        let xj = polygon[j].lng, yj = polygon[j].lat;

        if ((yi > y) !== (yj > y) &&
            (x < (xj - xi) * (y - yi) / (yj - yi) + xi)) {
            isInside = !isInside;
        }
    }
    return isInside;
}


const isInside = isPointInPolygon(point, polygon);


msg.payload.isInside = isInside;

if (isInside) {
    msg.payload.iconColor = "green";
} else {
    msg.payload.iconColor = "red";
}

msg.payload.layer = "pointsLayer";

return msg;

```
