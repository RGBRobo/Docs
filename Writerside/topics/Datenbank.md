# Datenbank

> **Information**
>
> Nach Absprache mit Herrn Stolz, am 04.06.2024, dürfen wir die Datenbank MariaDB verwenden.


Zum Speichern unserer (Mess-) daten nutzen wir MariaDB in kombination mit einer
Persistenzschicht für Java. Spezifisch wird in diesem Programm die neuste Version
von Hibernate-ORM verwendet.

```mermaid
classDiagram
class Account {
    -username String
    -password String
    +isSystem() boolean
}
class DBObject {
    -id String
    -version int
}
class Produktion {
    -name String
    -datum LocalDateTime
    -anzahlFertig Integer
    -bauteile List
}
class Bauteil {
    -nummer Integer
    -energieaufwand Double
    -farbe String
    -messung Messung
    -produktion Produktion
}
class Messung {
    -nummer Integer
    -temperatur Double
    -luftfeuchtigkeit Double
    -ergebnis String
    -date LocalDateTime
    -bauteil Bauteil
}
class ServiceAccount {
    -enabled Boolean
    +isSystem() boolean
}

DBObject <|-- Produktion
DBObject <|-- Bauteil
DBObject <|-- Messung
DBObject <|-- Account
Account <|-- ServiceAccount
Bauteil "N" --> "1" Produktion
Bauteil "1" --> "1" Messung
```

## FAQ 
<deflist collapsible="true">
    <def title="Warum Hibernate-ORM anstelle von Hibernate-OGM?" default-state="collapsed">
        Hibernate-ORM wird noch aktiv von den Entwicklern gewartet und entwickelt, 
        während Hibernate-OGM keinen Support und Bugfixes mehr erhält. Ebenso setzt das Kit,
        welches wir verwenden auf Hibernate-ORM und deswegen besteht eine inkompatibilität
        zu Hibernate-OGM.
    </def>
    <def title="Warum MariaDB?" default-state="collapsed">
        MariaDB ist eine bekannte, performante und von einer großen OpenSource Community
        entwickelte Datenbank. Die Datenbank selbst ist OpenSource und ist somit kostenlos.
        Deswegen eignet sich diese Datenbank besonders gut für dieses Projekt.
    </def>
    <def title="Wie genau sprecht ihr die Datenbank an?" default-state="collapsed">
        Das sogenannte heavy lifting betreibt hier Hibernate, welches für uns die Persistenz
        der erstellten Java-Objekte übernimmt. Diese Objekte werden Serialisiert und auf
        Datenbankfelder gemappt. Hinter Hibernate läuft der normale JDBC-Treiber von MariaDB,
        welcher die Verbindung zur Datenbank bereitstellt.
    </def>
</deflist>