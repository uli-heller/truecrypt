Verschlüsselter USB-Stick mit TrueCrypt
=======================================

Dieses Dokument beschreibt Erstellung und Handhabung eines mit TrueCrypt verschlüsselten USB-Sticks.
Der Stick soll unter Linux und Windows verwendbar sein und (zumindest) einen Browser und einen Email-Client
bereitstellen samt zugehöriger Nutzdaten.

Partitionierung und Formatierung
--------------------------------

* FAT32 (VFAT) ... Dateigröße ist limitiert auf 4GB
* NTFS ... funktioniert relativ problemlos
* exFAT ... funktioniert relativ problemlos

Grundeinrichtung
----------------

* Dateien von Uli's Beispielstick auf den USB-Stick kopieren (Details zu den Dateien stehen um Abschnitt "Dateien")
* TrueCrypt-Volume auf dem USB-Stick anlegen
* Dateien von Uli's Beispiel-Truecrypt-Volume "uli.tc" in das neue TrueCrypt-Volume reinkopieren
* Falls bereits vorhanden: Profile-Verzeichnis von Firefox kopieren nach .../firefox-profile
* Test: Firefox starten mittels `./firefox.sh` oder `.\firefox.bat` -> Sind die Firefox-Daten (bspw. Lesezeichen) vorhanden?
* Falls bereits vorhanden: Profile-Verzeichnis von Thunderbird kopieren nach .../thunderbird-profile
* Test: Thunderbird starten mittels `./thunderbird.sh` oder `.\thunderbird.bat` -> Sind die Thunderbird-Daten (bspw. Konten) vorhanden?

Verwendung
----------

* Firefox: Immer starten über das Start-Skript im TrueCrypt-Volume vorhandene `./firefox.sh` oder `.\firefox.bat`
* Thunderbird: Immer starten über das Start-Skript im TrueCrypt-Volume vorhandene `./thunderbird.sh` oder `.\thunderbird.bat`

Aktualisierung
--------------

Die Aktualisierung von Firefox und Thunderbird läuft grundsätzlich so ab:

* Ermitteln der aktuell laufenden Version, bspw. 35.0.1
* Sichten: Gibt es dafür bereits ein Sicherungsverzeichnis für die aktuelle Umgebung?
  Sicherstellen, dass es das Sicherungsverzeichnis .../linux-x64/firefox-35.0.1 gibt
  und nicht nur .../linux-x64/firefox.
* Falls Sicherungsverzeichnis nicht vorhanden: Sicherungsverzeichnis erstellen
    * `cp -a .../linux-x64/firefox  .../linux-x64/firefox-35.0.1`
* Aktualisierung innerhalb von Firefox/Thunderbird durchführen
* Neustart von Firefox/Thunderbird
* Ermitteln der neuen Version, bspw. 36.0
* Sichten: Funktioniert "alles"?
* Falls ja: Firefox/Thunderbird beenden, neues Sicherungsverzeichnis erstellen
    * `cp -a .../linux-x64/firefox  .../linux-x64/firefox-36.0`
* Falls nein: Zurückdrehen
    * `rm -rf .../linux-x64/firefox; cp -a .../linux-x64/firefox-35.0.1  .../linux-x64/firefox`

Dateien
-------

### Außerhalb des TrueCrypt-Volumes

* README.txt ... diese Datei
* environment.sh ... Hilfsdatei
* truecrypt.sh ... Start-Skript für TrueCrypt
* mozilla ... Installationsdateien für Firefox (Browser) und Thunderbird (Email)
    * thunderbird-31.4.0_x86.tar.bz2 ... für 32-Bit-Linux
    * thunderbird-31.4.0_x64.tar.bz2 ... für 64-Bit-Linux [von hier](ftp://ftp.mozilla.org/pub/thunderbird/releases/31.4.0/linux-x86_64/de/)
    * Thunderbird 31.4.0.dmg ... für MacOSX
    * Thunderbird Setup 31.4.0.exe ... für Windows
    * firefox-35.0.1_x86.tar.bz2 ... für 32-Bit-Linux
    * firefox-35.0.1_x64.tar.bz2 ... für 64-Bit-Linux
    * Firefox 35.0.1.dmg ... für MacOSX
    * Firefox Setup 35.0.1.exe ... für Windows
* truecrypt ... Festplattenverschlüsseler, heruntergeladen von heise.de
    * truecrypt-7.1a-linux-x86.tar.gz ... für 32-Bit-Linux
    * truecrypt-7.1a-linux-x64.tar.gz ... für 64-Bit-Linux
    * truecrypt_7.1a_mac_os_x.dmg ... für MacOSX
    * truecrypt_setup_7.1a.exe ... für Windows (Installer)
    * truecrypt.zip ... für Windows (Portable)
* linux-x86
    * truecrypt
* linux-x64
    * truecrypt
* win ... Portable Version von TrueCrypt für Windows
* debs ... Installationsdateien für ExFAT unter Linux
* uli.tc ... Beispiel-TrueCrypt-Volume "uli"

### Innerhalb des TrueCrypt-Volumes

* environment.sh ... Hilfsdatei
* firefox.sh ... Start-Skript für Firefox (Linux)
* thunderbird.sh ... Start-Skript für Thunderbird (Linux)
* firefox.bat ... Start-Skript für Firefox (Windows)
* thunderbird.bat ... Start-Skript für Thunderbird (Windows)
* linux-x64 ... Programme für 64-Bit-Linux
    * firefox ... Installationsverzeichnis für den aktiv verwendeten Firefox
    * firefox-{version} ... Sicherungsverzeichnis
    * thunderbird ... Installationsverzeichnis für den aktiv verwendeten Thunderbird
    * thinderbird-{version} ... Sicherungsverzeichnis
* linux-x86 ... Programme für 32-Bit-Linux
    * firefox ... Installationsverzeichnis für den aktiv verwendeten Firefox
    * firefox-{version} ... Sicherungsverzeichnis
    * thunderbird ... Installationsverzeichnis für den aktiv verwendeten Thunderbird
    * thunderbird-{version} ... Sicherungsverzeichnis
* win ... Programme für Windows
    * firefox ... Installationsverzeichnis für den aktiv verwendeten Firefox
    * firefox-{version} ... Sicherungsverzeichnis
    * thunderbird ... Installationsverzeichnis für den aktiv verwendeten Thunderbird
    * thunderbird-{version} ... Sicherungsverzeichnis
* firefox-profile ... Nutzdaten vom Firefox
* thunderbird-profile ... Nutzdaten vom Thunderbird

Linux
-----

### Bittigkeit ermitteln

Ermitteln, ob man ein 32- oder 64-Bit-System hat: Kommando
`uname -m`

* x86_64 ... 64 Bit
* i686 ... 32 Bit

### EXFAT

* Altes Toshiba-Laptop - 32 bit Ubuntu 12.04
  *exfat*-Pakete aus debs/12.04 installieren

* Neues Laptop - Ubuntu 14.04
  exfat-Pakete per "Softwareauswahl" installieren
  ODER *exfat*-Pakete aus debs/{14.04,14.04.64} installieren

### TrueCrypt

Im Verzeichnis "truecrypt" befinden sich die Installationsdateien
von heise.de. Für den Einsatz unter Linux muß TrueCrypt nicht
installiert werden, es können die vorab ausgepackten Versionen
verwendet werden.

* `./linux-x64/truecrypt` ... startet die 64-Bit-Version
* `./linux-x86/truecrypt` ... startet die 32-Bit-Version

Wenn man versucht, auf einem 64-Bit-System die 32-Bit-Version von TrueCrypt
zu starten, dann erscheint eine Fehlermeldung dieser Art:

```
uli@mypc:$ ./linux-x86/truecrypt 
bash: ./linux-x86/truecrypt: Datei oder Verzeichnis nicht gefunden
```

#### TrueCrypt-Volume mit exFAT

Hinweis: Das machen wir vorerst nicht mehr auf diese Art und Weise,
der ganze Abschnitt ist obsolet.
Mir ist einmal ein exFAT-Volume "kaputt" gegangen und ich konnte es nicht
mehr reparieren. `exfatfsck` Version 1.1.1 kann nicht reparieren!

1. Volume wie üblich anlegen und einbinden
2. Ermitteln: Wie heißt das zugehörige Gerät?

    $ mount
    ...
    /dev/mapper/truecrypt1 on /media/truecrypt1 type vfat (rw,uid=1000,gid=1000,umask=077)

3. Aushängen (nicht über die TrueCrypt-Oberfläche durchführen!):
   `sudo umount /media/truecrypt1`
4. ExFAT-Dateisystem anlegen:
   `sudo  mkfs.exfat -n Uli_TrueCrypt /dev/mapper/truecrypt1`
5. Aushängen über die TrueCrypt-Oberfläche
6. Einhängen über die TrueCrypt-Oberfläche

#### TrueCrypt-Volume mit NTFS

1. Volume wie üblich anlegen und einbinden
2. Ermitteln: Wie heißt das zugehörige Gerät?

    $ mount
    ...
    /dev/mapper/truecrypt1 on /media/truecrypt1 type vfat (rw,uid=1000,gid=1000,umask=077)

3. Aushängen (nicht über die TrueCrypt-Oberfläche durchführen!):
   `sudo umount /media/truecrypt1`
4. ExFAT-Dateisystem anlegen:
   `sudo  mkfs.ntfs -n Uli_TrueCrypt /dev/mapper/truecrypt1`
5. Aushängen über die TrueCrypt-Oberfläche
6. Einhängen über die TrueCrypt-Oberfläche

Tests
-----

### Linux

Alle Tests mit diesen Randbedingungen durchführen:

* Erster Parameter-Satz
    * USB-Stick: FAT-Format (... das geht mit "Laufwerke")
    * TrueCrypt-Volume: FAT-Format (... das geht über die TrueCrypt-Oberfläche)
* Zweiter Parameter-Satz
    * USB-Stick: exFAT-Format
    * TrueCrypt-Volume: FAT-Format (... das geht über die TrueCrypt-Oberfläche)
* Dritter Parameter-Satz
    * USB-Stick: FAT-Format
    * TrueCrypt-Volume: NTFS-Format (... siehe Beschreibung)
* Vierter Parameter-Satz
    * USB-Stick: exFAT-Format
    * TrueCrypt-Volume: NTFS-Format (... siehe Beschreibung)
* Fünfter Parameter-Satz
    * USB-Stick: NTFS-Format
    * TrueCrypt-Volume: NTFS-Format (... siehe Beschreibung)
* Sechster Parameter-Satz
    * USB-Stick 2 Partitionen: sdb1 - FAT-Format, sdb2 - nicht formatiert
    * TrueCrypt-Volume auf sdb2: FAT-Format (... siehe Beschreibung)

Der betreffende USB-Stick muß für jeden Test-Zyklus neu formatiert werden!

Hier die Tests im einzelnen:

1. Funktioniert die Anleitung grundsätzlich?
2. Klappt der Start von Firefox?
3. Klappt der Start von Thunderbird?
4. Klappt dieser Zyklus: (nur testen, wenn vorige Tests OK sind)
    * USB-Stick einstecken
    * TrueCrypt-Volume einbinden
    * Daten auf das TrueCrypt-Volume schreiben
    * Daten auf den USB-Stick schreiben
    * TrueCrypt-Volume aushängen
    * USB-Stick aushängen
    * USB-Stick abziehen
   Zyklus 10-mal durchführen, dabei immer sichten, ob die geschriebenen Daten beim nächsten Zyklus sichtbar sind!
5. Klappt dieser Zyklus: (nur testen, wenn vorige Tests inkl. voriger Zyklus OK sind)
    * USB-Stick einstecken
    * TrueCrypt-Volume einbinden
    * Daten auf das TrueCrypt-Volume schreiben
    * Daten auf den USB-Stick schreiben
    * TrueCrypt-Volume aushängen
    * USB-Stick nicht aushängen, nur `sync` ausführen (dauert evtl. ein wenig, also Wartezeit)
    * USB-Stick abziehen
   Zyklus 5-mal durchführen, dabei immer sichten, ob die geschriebenen Daten beim nächsten Zyklus sichtbar sind!
6. Klappt dieser Zyklus: (nur testen, wenn vorige Tests inkl. voriger Zyklus OK sind)
    * USB-Stick einstecken
    * TrueCrypt-Volume einbinden
    * Daten auf das TrueCrypt-Volume schreiben
    * Daten auf den USB-Stick schreiben
    * TrueCrypt-Volume aushängen
    * USB-Stick nicht aushängen, nicht warten, kein `sync`
    * USB-Stick abziehen
   Zyklus 10-mal durchführen, dabei immer sichten, ob die geschriebenen Daten beim nächsten Zyklus sichtbar sind!
7. Klappt dieser Zyklus: (nur testen, wenn vorige Tests inkl. voriger Zyklus OK sind)
    * USB-Stick einstecken
    * TrueCrypt-Volume einbinden
    * Daten auf das TrueCrypt-Volume schreiben
    * Daten auf den USB-Stick schreiben
    * TrueCrypt-Volume nicht aushängen, nur `sync` ausführen (dauert evtl. ein wenig, also Wartezeit)
    * USB-Stick nicht aushängen, nicht warten, kein `sync`
    * USB-Stick abziehen
   Zyklus 10-mal durchführen, dabei immer sichten, ob die geschriebenen Daten beim nächsten Zyklus sichtbar sind!
8. Klappt dieser Zyklus: (nur testen, wenn vorige Tests inkl. voriger Zyklus OK sind)
    * USB-Stick einstecken
    * TrueCrypt-Volume einbinden
    * Daten auf das TrueCrypt-Volume schreiben
    * Daten auf den USB-Stick schreiben
    * TrueCrypt-Volume nicht aushängen, nicht warten, kein `sync`
    * USB-Stick nicht aushängen, nicht warten, kein `sync`
    * USB-Stick abziehen
   Zyklus 10-mal durchführen, dabei immer sichten, ob die geschriebenen Daten beim nächsten Zyklus sichtbar sind!
