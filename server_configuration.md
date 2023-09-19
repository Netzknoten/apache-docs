# Apache2 Konfigurationsdatei

Dies ist die Hauptkonfigurationsdatei des Apache-Servers. Sie enthält die Konfigurationsanweisungen, die dem Server seine Anweisungen geben. Detaillierte Informationen zu den Anweisungen finden Sie unter [httpd.apache.org/docs/2.4/](http://httpd.apache.org/docs/2.4/) und spezifische Hinweise zu Debian unter [Debian-spezifischen Hinweisen](/usr/share/doc/apache2/README.Debian).

## Zusammenfassung zur Funktionsweise der Apache 2-Konfiguration in Debian:

Die Konfiguration des Apache 2-Webservers in Debian unterscheidet sich erheblich von der empfohlenen Methode zur Konfiguration des Webservers von Upstream. Dies liegt daran, dass die Standardinstallation von Apache2 in Debian versucht, das Hinzufügen und Entfernen von Modulen, virtuellen Hosts und zusätzlichen Konfigurationsanweisungen so flexibel wie möglich zu gestalten, um Änderungen zu automatisieren und die Verwaltung des Servers so einfach wie möglich zu gestalten.

Die Konfiguration ist in mehrere Dateien unterteilt, die die hierarchische Struktur der Konfiguration im Verzeichnis /etc/apache2/ bilden:

- **/etc/apache2/**
  - **apache2.conf**
    - **ports.conf**
  - **mods-enabled**
    - \*.load
    - \*.conf
  - **conf-enabled**
    - \*.conf
  - **sites-enabled**
    - \*.conf

Jede dieser Dateien und Verzeichnisse hat eine spezielle Funktion in der Apache 2-Konfiguration.

- **apache2.conf**: Die Hauptkonfigurationsdatei, die alle anderen Konfigurationsdateien einbezieht und die grundlegenden Einstellungen für den Server enthält.

- **ports.conf**: Hier werden die Ports festgelegt, auf denen der Server auf eingehende Verbindungen hört.

- **mods-enabled**: In diesem Verzeichnis werden Module aktiviert. Die Dateien mit der Erweiterung \*.load laden die Module, während die Dateien mit der Erweiterung \*.conf die Konfigurationen für die Module enthalten.

- **conf-enabled**: Hier können zusätzliche Konfigurationsdateien aktiviert werden, die nicht direkt mit Modulen oder virtuellen Hosts zusammenhängen.

- **sites-enabled**: Dieses Verzeichnis enthält die Konfigurationen für virtuelle Hosts, die aktiviert sind und somit vom Server verarbeitet werden.

Dieses hier ist ein kommentierter Auszug aus der Apache2-Konfigurationsdatei, in dem die verschiedenen Teile der Konfiguration erklärt werden.

# Globale Konfiguration

## ServerRoot
Der `ServerRoot` ist das oberste Verzeichnis, unter dem die Konfigurations-, Fehler- und Protokolldateien des Servers gespeichert sind. Beachten Sie, dass Sie keinen Schrägstrich am Ende des Verzeichnispfads hinzufügen sollten. Beispiel: `ServerRoot "/etc/apache2"`

## Mutex
Die `Mutex` ist eine Datei zur Serialisierung der Akzeptanz, die AUF EINEM LOKALEN DATENTRÄGER GESPEICHERT WERDEN MUSS. Weitere Informationen finden Sie in der Mutex-Dokumentation unter <URL:http://httpd.apache.org/docs/2.4/mod/core.html#mutex>).

## DefaultRuntimeDir
Das Verzeichnis, in dem SHM (Shared Memory) und andere Laufzeitdateien gespeichert werden, wird durch `DefaultRuntimeDir` festgelegt. Beispiel: `DefaultRuntimeDir ${APACHE_RUN_DIR}`

## PidFile
Die `PidFile` ist die Datei, in der der Server seine Prozesskennung aufzeichnet, wenn er gestartet wird. Dies muss in `/etc/apache2/envvars` festgelegt werden. Beispiel: `PidFile ${APACHE_PID_FILE}`

## Timeout
Die `Timeout` gibt die Anzahl der Sekunden an, bevor Empfangs- und Sendevorgänge ablaufen. Beispiel: `Timeout 300`

## KeepAlive
Die `KeepAlive`-Einstellung legt fest, ob persistente Verbindungen (mehr als eine Anforderung pro Verbindung) erlaubt sind oder nicht. Auf "On" setzen, um zu aktivieren. Beispiel: `KeepAlive On`

## MaxKeepAliveRequests
`MaxKeepAliveRequests` ist die maximale Anzahl von Anfragen, die während einer persistierenden Verbindung erlaubt sind. Auf 0 setzen, um eine unbegrenzte Anzahl zu erlauben. Beispiel: `MaxKeepAliveRequests 100`

## KeepAliveTimeout
Die `KeepAliveTimeout` ist die Anzahl der Sekunden, die auf die nächste Anforderung desselben Clients auf derselben Verbindung gewartet wird. Beispiel: `KeepAliveTimeout 5`

## Benutzer und Gruppe
Die Einstellungen für Benutzer und Gruppe müssen in `/etc/apache2/envvars` gesetzt werden. Beispiel: `User ${APACHE_RUN_USER}` und `Group ${APACHE_RUN_GROUP}`

## HostnameLookups
Die `HostnameLookups` legt fest, ob die Namen von Clients oder nur ihre IP-Adressen protokolliert werden sollen. Beispiel: `HostnameLookups Off`

## ErrorLog
Der `ErrorLog` gibt den Speicherort der Fehlerprotokolldatei an. Beispiel: `ErrorLog ${APACHE_LOG_DIR}/error.log`

## LogLevel
Die `LogLevel` steuert die Schwere der in die `error_log` protokollierten Nachrichten. Beispiel: `LogLevel warn`

## Einbindung von Modulkonfigurationen
Die `IncludeOptional`-Anweisungen ermöglichen die Einbindung von Modulkonfigurationen und Listen von Ports, die gehört werden sollen.

## Standard-Sicherheitsmodell
Die Einstellungen legen das Standard-Sicherheitsmodell des Apache2 HTTPD-Servers fest. Der Zugriff auf das Wurzelverzeichnis außerhalb von `/usr/share` und `/var/www` wird nicht erlaubt. Beispielkonfigurationen für verschiedene Verzeichnisse sind vorhanden.

## AccessFileName
Der `AccessFileName` gibt den Namen der Datei an, nach der in jedem Verzeichnis für zusätzliche Konfigurationsanweisungen gesucht wird. Beispiel: `AccessFileName .htaccess`

## Verhinderung der Anzeige von .htaccess-Dateien
Die nachfolgenden Anweisungen verhindern, dass Dateien mit dem Namen `.htaccess` und `.htpasswd` von Webclients angezeigt werden.

## Log-Formate
Es werden verschiedene Log-Formate definiert, die für Protokolle verwendet werden. Die Formatierungen ermöglichen die Anzeige verschiedener Informationen in den Protokollen.

## Einbindung von Konfigurationsdateien
Es werden Anweisungen zum Einbinden von Modul- und Konfigurationsdateien gegeben.

