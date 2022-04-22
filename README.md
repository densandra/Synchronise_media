1. Funktionalitäten, die unterstützt werden (Stand 25.01.21):
- Die API Calls selbst wurden in einer separaten Datei implementiert und befinden sich nicht in diesem Verzeichnis.
- Synchronisation lokal zu online
- Es gibt 2 Synchronisierungs-Modi: Nur neue Dateien hochladen oder lokale Verzeichnisstruktur vollständig abbilden.
- Kategorien können per Skript erstellt, überarbeitet, gelöscht und zugewiesen werden.
- Dateien können per Skript erstellt, überarbeitet und gelöscht werden.
- Modulreiterspezifische Konfigurationen (außer des Testmodulreiters) wurden aus diesem Skript entfernt.
- Attributwerte werden aus dem Dateinamen bezogen. Deshalb gelten die in validate_generic_file_name definierten Regeln für Dateinamen.
- Voraussetzung für Synchronisation von Kategorien ist, dass je Verzeichnis eine .folder_info enthalten ist, in der die Kategorie-ID steht.
- Kategoriezuweisungen funktionieren unter den gegebenen Voraussetzungen prinzipiell, allerdings ist die Methode ineffizient, da bei jeder Synchronisierung alle Zuweisungen aufgelöst werden müssen und dann neu gesetzt werden (mehr dazu in 2.1)
- keine Vorraussetzung, aber eine Empfehlung für die korrekte Synchronisierung ist, dass jedem Modulreiter, der regelmäßig synchronisiert werden soll, ein md5-Hash als Pflichtattribut gesetzt wird, da die API eine hochgeladene Datei, während sie noch rendert, nicht abfragen kann und es dadurch zum Hochladen von Duplikaten kommen kann.
- Implementierungsfehler werden geloggt. Fehler, die ein Nutzer selbstständig beheben kann (z.B. falsch benannte Dateinamen) werden in einer separaten Datei geloggt, die im Verzeichnis generiert wird, das der Funktion local_to_online übergeben wurde.

2. Funktionalitäten, die noch nicht unterstützt werden (Stand 25.01.21):
- 2.1 selektives Entfernen von Kategoriezuweisungen. Der entsprechende API call ist fehlerhaft und entfernt ALLE Kategorienzuweisungen einer Datei, anstatt nur der Angegebenen.
- 2.2 Synchronisation online zu lokal
- 2.3 Wenn eine Datei einmal einer Rootcategory zugeordnet wurde, lässt sich diese Zuweisung nie wieder löschen. Außerdem lässt sich per API nicht abfragen, zu welcher Rootcategory eine Datei gehört. Bei Unterkategorien funktioniert Zuweisung normal.
