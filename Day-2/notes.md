# Day 2 – File Operations, Permissions, Hidden Files, Wildcards, Find & Grep

## Überblick
Am zweiten Tag habe ich meine Linux-Grundlagen deutlich erweitert. Der Fokus lag heute auf dem praktischen Umgang mit Dateien, Verzeichnissen, Berechtigungen und der präzisen Suche nach Dateien oder Inhalten. Dabei ging es nicht nur um das Ausführen von Befehlen, sondern auch darum, die sicherheitsrelevante Bedeutung dieser Befehle zu verstehen.

## Was ich heute gelernt habe

### 1. Dateioperationen
Ich habe gelernt, wie man Dateien und Verzeichnisse erstellt, kopiert, verschiebt, umbenennt und löscht.

Verwendete Befehle:
- `mkdir` → Verzeichnis erstellen
- `touch` → leere Datei erstellen
- `cp` → Dateien oder Verzeichnisse kopieren
- `mv` → Dateien verschieben oder umbenennen
- `rm` → Dateien löschen
- `rm -r` → Verzeichnisse rekursiv löschen

Wichtige Erkenntnisse:
- `cp` erstellt eine Kopie
- `mv` verschiebt eine Datei oder ändert ihren Namen
- `rm` löscht direkt, meistens ohne Papierkorb
- `rm -r` ist gefährlich, wenn man nicht genau weiß, was man tut

### 2. Dateien lesen und bearbeiten
Ich habe gelernt, Dateien auf verschiedene Arten zu lesen und zu bearbeiten.

Verwendete Befehle:
- `cat` → schnelle Ausgabe des Dateiinhalts
- `less` → komfortables Lesen längerer Dateien
- `nano` → Datei im Terminal bearbeiten

Wichtige Erkenntnisse:
- `cat` ist gut für kurze Dateien
- `less` ist besser für lange Inhalte oder Logs
- `nano` ermöglicht direktes Bearbeiten aus dem Terminal

### 3. Umleitung mit `>` und `>>`
Ich habe gelernt, wie man Inhalte in Dateien schreibt.

Beispiele:
- `>` überschreibt den alten Inhalt
- `>>` hängt neuen Inhalt an die bestehende Datei an

Wichtige Erkenntnisse:
- `>` ist praktisch, aber gefährlich, wenn man aus Versehen wichtige Inhalte überschreibt
- `>>` ist sicherer, wenn man etwas ergänzen will

### 4. Berechtigungen und Besitzrechte
Ich habe begonnen zu verstehen, wie Linux-Zugriffsrechte funktionieren.

Verwendete Befehle:
- `ls -l` → Berechtigungen von Dateien anzeigen
- `ls -ld` → Berechtigungen eines Verzeichnisses anzeigen
- `whoami` → aktuellen Benutzer anzeigen
- `id` → Benutzer-ID und Gruppen anzeigen
- `groups` → alle Gruppen des Benutzers anzeigen
- `chmod` → Berechtigungen ändern

Ich habe folgende Berechtigungen praktisch verwendet:
- `600` → nur der Besitzer darf lesen und schreiben
- `644` → Besitzer darf lesen und schreiben, andere nur lesen
- `700` → nur der Besitzer darf lesen, schreiben und ausführen
- `755` → Besitzer hat volle Rechte, Gruppe und andere dürfen lesen und ausführen

Wichtige Erkenntnisse:
- Dateien mit sensiblen Informationen dürfen nicht zu offen gesetzt werden
- Eine Datei mit Berechtigung `644` kann für sensible Inhalte gefährlich sein
- Ein Skript mit Ausführungsrechten kann sicherheitsrelevant sein
- Verzeichnisse mit `700` sind für private Daten sinnvoll

### 5. Versteckte Dateien
Ich habe gelernt, dass Dateien oder Verzeichnisse mit einem Punkt am Anfang als versteckt gelten.

Beispiele:
- `.hidden.txt`
- `.secret_dir`
- `.env`
- `.token`

Verwendete Befehle:
- `ls` → normale Anzeige
- `ls -a` → inklusive versteckter Dateien
- `ls -la` → detaillierte Anzeige inklusive versteckter Dateien

Wichtige Erkenntnisse:
- Versteckt bedeutet nicht sicher
- Sensible Informationen können in versteckten Dateien liegen
- Man darf sich nicht nur auf die normale `ls`-Ausgabe verlassen

### 6. Wildcards und präzise Befehle
Ich habe gelernt, wie Platzhalter funktionieren.

Verwendete Muster:
- `*` → beliebig viele Zeichen
- `?` → genau ein Zeichen
- `[12]` → bestimmte einzelne Zeichen

Beispiele:
- `ls *.txt`
- `ls *.log`
- `ls file?.txt`
- `ls file*.txt`
- `ls file[12].txt`

Wichtige Erkenntnisse:
- `*` ist mächtig, aber gefährlich bei `rm` oder `mv`
- `file?.txt` trifft nur auf Dateinamen mit genau einem Zeichen an dieser Stelle zu
- `file*.txt` trifft auf deutlich mehr Dateien zu
- Vor einem riskanten Befehl sollte man zuerst mit `ls` prüfen, was wirklich ausgewählt wird

### 7. Suchen mit `find`
Ich habe gelernt, wie man Dateien und Verzeichnisse systematisch sucht.

Verwendete Befehle:
- `find .`
- `find . -type f`
- `find . -type d`
- `find . -name "*.txt"`
- `find . -name "*.log"`
- `find . -name "*.conf"`
- `find . -name "*.sh"`
- `find . -name "*secret*"`

Wichtige Erkenntnisse:
- `find` sucht nach Dateien und Verzeichnissen
- Mit `-type f` finde ich nur Dateien
- Mit `-type d` finde ich nur Verzeichnisse
- Mit `-name` kann ich gezielt nach Mustern suchen

### 8. Suchen mit `grep`
Ich habe gelernt, wie man nach Inhalten innerhalb von Dateien sucht.

Verwendete Befehle:
- `grep "failed" logs/auth.log`
- `grep "token" configs/secret.conf`
- `grep -r "mehdi" .`
- `grep -r "admin" .`
- `grep -r "echo" scripts`
- `grep -i "TOKEN" configs/*`

Wichtige Erkenntnisse:
- `grep` durchsucht Inhalte
- `grep -r` durchsucht rekursiv Unterverzeichnisse
- `grep -i` ignoriert Groß- und Kleinschreibung
- Das ist für Logs, Konfigurationen und Sicherheitsanalysen sehr nützlich

## Sicherheitsdenken des Tages
Heute habe ich verstanden, dass Linux-Befehle nicht nur Werkzeuge zur Dateiverwaltung sind, sondern direkt mit Sicherheit zusammenhängen.

Wichtige sicherheitsbezogene Gedanken:
- Wer eine Datei lesen kann, kann Informationen stehlen
- Wer eine Datei schreiben kann, kann Inhalte manipulieren
- Wer eine Datei löschen kann, kann Spuren verwischen oder Systeme beschädigen
- Versteckte Dateien sind nicht automatisch geschützt
- Schlechte Berechtigungen sind ein echtes Sicherheitsproblem
- Unpräzise Wildcards können sehr gefährlich werden
- Mit `find` und `grep` kann man sensible Dateien, Logs oder verdächtige Inhalte schnell aufspüren

## Befehle des Tages
```bash
mkdir
touch
cp
mv
rm
rm -r
cat
less
nano
ls
ls -a
ls -la
ls -l
ls -ld
whoami
id
groups
chmod
find
grep
grep -r
grep -i
-------------------------------------

## Fazit

Day 2 war ein sehr wichtiger Tag. Ich habe nicht nur gelernt, wie man mit Dateien arbeitet, sondern auch, wie Linux-Berechtigungen,
versteckte Dateien, Platzhalter und Suchbefehle in der Praxis funktionieren. Besonders wichtig war heute der sicherheitsrelevante Blick auf Dateien,
Zugriffsrechte und Inhalte. Damit habe ich eine deutlich stärkere Grundlage für die nächsten Schritte im Bereich Cyber Security aufgebaut.
