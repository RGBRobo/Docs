# Service

Die zentrale Komponente, welche sowohl die Datenbank bereitstellt für die Roboter, als auch den Broker,
der die zentrale Schnittstelle zu den Robotern darstellt. Ebenfalls wird das WebUI von dem Service bereitgestellt.


````mermaid
gitGraph
    commit id: "916a8b4" tag: "Initial Commit"
    branch dev
    checkout dev
    commit id: "dcfccb8"
    commit id: "52f4526" tag: "Refactoring"
    checkout main
    merge dev id: "e758d4b"
    checkout dev
    commit id: "fd7e033" tag: "New Kit v1.9.6"
    commit id: "14e2869"
    commit id: "caac4e8"
    commit id: "5040446"
    branch feature/Service-09
    checkout feature/Service-09
    commit id: "1a4bdd9"
    commit id: "9508232" tag: "Anlegen der Detailspage"
    checkout dev
    branch feature/Service-10
    checkout feature/Service-10
    commit id: "0ece830" tag: "Account Übersicht"
    checkout dev
    merge feature/Service-10 id: "963e3a5"
    commit id: "a2fa390" tag: "New Kit v2.0.5"
    merge feature/Service-09 id: "346f8e7"
    checkout dev
    commit id: "5c78d56" tag: "Performance Optimization"
    commit id: "ac36f21"
    commit id: "d9c8ab3"
    commit id: "a37fe3c" tag: "Secure Restart Implemented."
    checkout main
    merge dev id: "4fc0668"
    branch bugfix/Service-14

````



