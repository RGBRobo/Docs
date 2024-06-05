# HiveMQ

> **Information**
>
> Genutzt wird die neuste Version des OpenSource Brokers HiveMQ, welcher ebenso wie unser Programm
> in Java geschrieben ist. Welches das Einbinden in unser Programm um einiges erleichtert.

## FAQ

<deflist collapsible="true">
    <def title="Warum habt ihr euch für MQTT entschieden?" default-state="collapsed">
        MQTT bietet entscheidende Vorteile gegenüber OPC UA und REST, insbesondere für IoT- und Automatisierungsanwendungen. 
        Es ist leichtgewichtig und effizient, was es ideal für begrenzte Bandbreite und Energieressourcen macht. 
        Die Publish/Subscribe-Architektur ermöglicht skalierbare und flexible asynchrone Kommunikation. 
        Mit verschiedenen QoS-Stufen und Unterstützung für SSL/TLS bietet MQTT hohe Zuverlässigkeit und Sicherheit. 
        Im Vergleich zu OPC UA ist MQTT einfacher zu implementieren und zu warten, während es gegenüber REST effizienter für kontinuierliche Datenerfassung ist. 
        Zudem wird MQTT von vielen Plattformen unterstützt, was die Integration erleichtert.
    </def>
    <def title="Wieso HiveMQ und nicht Mosquitto?" default-state="collapsed">
        HiveMQ bietet gegenüber Mosquitto Vorteile, insbesondere für Java-basierte Anwendungen. 
        Es integriert sich nahtlos mit Java und ermöglicht eine einfache Einbindung und Erweiterung durch eine umfangreiche API. 
        HiveMQ ist für hohe Skalierbarkeit und Zuverlässigkeit ausgelegt und unterstützt Cluster-Bildung, um Lasten effizient zu verteilen. 
        Zudem bietet es erweiterte Sicherheitsfunktionen, eine benutzerfreundliche Weboberfläche zur Verwaltung und umfassende Monitoring-Tools. 
        Diese Merkmale machen HiveMQ zur besseren Wahl für professionelle und groß angelegte IoT-Implementierungen im Vergleich zu Mosquitto, das eher für kleinere, einfache Setups geeignet ist.
    </def>
        
</deflist>