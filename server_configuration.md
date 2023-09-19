# Apache2 Konfigurationsdatei

**apache2.conf** ist die Hauptkonfigurationsdatei (diese Datei). Sie fügt die Teile zusammen, indem sie alle verbleibenden Konfigurationsdateien beim Start des Webservers einbezieht.

**ports.conf** wird immer von der Hauptkonfigurationsdatei eingeschlossen. Es soll die Empfangsports für eingehende Verbindungen bestimmen, die jederzeit angepasst werden können.

Konfigurationsdateien in den Verzeichnissen **mods-enabled/**, **conf-enabled/** und **sites-enabled/** enthalten bestimmte Konfigurationsschnipsel, die Module verwalten, globale Konfigurationsfragmente oder virtuelle Host-Konfigurationen, respectively.

Sie werden aktiviert, indem verfügbare Konfigurationsdateien aus ihren jeweiligen **-available/** Gegenstücken verknüpft werden. Diese sollten mit unseren Hilfsprogrammen `a2enmod/a2dismod`, `a2ensite/a2dissite` und `a2enconf/a2disconf` verwaltet werden. Siehe die entsprechenden Handbuchseiten für detaillierte Informationen.

Die ausführbare Datei heißt **apache2**. Aufgrund der Verwendung von Umgebungsvariablen muss apache2 in der Standardkonfiguration mit `/etc/init.d/apache2` oder `apache2ctl` gestartet/beendet werden. Das direkte Aufrufen von `/usr/bin/apache2` funktioniert nicht mit der Standardkonfiguration.

## Globale Konfiguration

- **ServerRoot**: Die Spitze des Verzeichnisbaums, unter dem die Konfigurations-, Fehler- und Protokolldateien des Servers gespeichert sind. Beachten Sie, dass kein Schrägstrich am Ende des Verzeichnispfads hinzugefügt werden sollte.

- **Mutex**: Die Lock-Datei für die Serialisierung der Akzeptanz MUSS AUF EINEM LOKALEN DATENTRÄGER GESPEICHERT WERDEN.

- **DefaultRuntimeDir**: Das Verzeichnis, in dem SHM und andere Laufzeitdateien gespeichert werden.

- **PidFile**: Die Datei, in der der Server seine Prozesskennung aufzeichnen sollte, wenn er gestartet wird.

- **Timeout**: Die Anzahl der Sekunden, bevor Empfangs- und Sendevorgänge ablaufen.

- **KeepAlive**: Ob persistente Verbindungen (mehr als eine Anforderung pro Verbindung) erlaubt sind oder nicht. Auf "Off" setzen, um zu deaktivieren.

- **MaxKeepAliveRequests**: Die maximale Anzahl von Anfragen, die während einer persistierenden Verbindung erlaubt sind.

- **KeepAliveTimeout**: Anzahl der Sekunden, die auf die nächste Anforderung des gleichen Clients auf derselben Verbindung gewartet wird.

- **User** und **Group**: Diese Einstellungen müssen in `/etc/apache2/envvars` gesetzt werden.

- **HostnameLookups**: Protokollieren der Namen von Clients oder nur ihrer IP-Adressen.

- **ErrorLog**: Der Speicherort der Fehlerprotokolldatei.

- **LogLevel**: Steuern Sie die Schwere der in die `error_log` protokollierten Nachrichten.

- **Include**: Einbinden von Modul- und Port-Konfigurationen.

## Verzeichnis-Konfiguration

Es folgen Konfigurationen für verschiedene Verzeichnisse:

- Die Standardeinstellung **<Directory />** verbietet den Zugriff und erlaubt keine Overrides.

- **<Directory /usr/share>** erlaubt den Zugriff und erlaubt alle Berechtigungen.

- **<Directory /var/www/>** erlaubt den Zugriff, erlaubt Indexseiten und erlaubt alle Berechtigungen.

- **AccessFileName**: Der Name der Datei, nach der in jedem Verzeichnis für zusätzliche Konfigurationsdirektiven gesucht wird.

- Es wird verhindert, dass Dateien mit dem Namen **.ht** von Webclients angezeigt werden.

## Log-Formate

Es werden verschiedene Log-Formate definiert, die für Protokolle verwendet werden.

## Einbindung von Konfigurationsdateien

Es werden Module und Konfigurationen einbezogen.

- **IncludeOptional mods-enabled/*.load**
- **IncludeOptional mods-enabled/*.conf**
- **Include ports.conf**

## Virtuelle Host-Konfiguration

Es wird das Standard-Sicherheitsmodell des Apache2 HTTPD-Servers festgelegt und der Zugriff auf das Wurzelverzeichnis außerhalb von `/usr/share` und `/var/www` wird nicht erlaubt. Die Konfiguration für andere Verzeichnisse ist auskommentiert.

- **AccessFileName**: Der Name der Datei, nach der in jedem Verzeichnis für zusätzliche Konfigurationsdirektiven gesucht wird.

- Es wird verhindert, dass Dateien mit dem Namen **.ht** von Webclients angezeigt werden.

- Es werden verschiedene Log-Formate definiert, die für Protokolle verwendet werden.

- Einbindung von Konfigurationsdateien.

