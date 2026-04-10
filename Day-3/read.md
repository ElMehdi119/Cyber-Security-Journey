DAY 3
Projekt: Cyber Security Journey
Phase: Phase 0 (Foundations Setup)

=====================================================
ZUSAMMENFASSUNG (KURZ & KLAR)
=====================================================

Heute habe ich gelernt:
- Pipes (|) und Redirection (>, >>)
- Wie man Befehle miteinander verbindet
- Wie man große Daten filtert und analysiert
- Wichtige Tools: head, tail, wc, sort, uniq, grep, cut
- Denken wie ein Analyst (nicht alles lesen, nur relevante Daten extrahieren)

Wichtige Erkenntnis:
Ich lese nicht einfach Daten, sondern ich filtere und analysiere sie gezielt.

=====================================================
ARBEITSUMGEBUNG ERSTELLEN
=====================================================

mkdir ~/day3_pipes_lab
cd ~/day3_pipes_lab
mkdir data logs reports

touch data/users.txt
touch data/access.log
touch data/errors.log

=====================================================
DATEIEN MIT INHALT FÜLLEN
=====================================================

nano data/users.txt

ali
sara
mehdi
ali
youssef
sara
amina
ali
karim

nano data/access.log

192.168.1.10 GET /login
192.168.1.11 POST /login
192.168.1.10 GET /dashboard
192.168.1.12 GET /admin
192.168.1.11 POST /login
192.168.1.13 GET /home
192.168.1.10 GET /settings
192.168.1.12 GET /admin
192.168.1.12 GET /admin

nano data/errors.log

ERROR: failed login for admin
WARNING: disk usage high
ERROR: permission denied
INFO: backup completed
ERROR: failed login for root
WARNING: suspicious connection detected

=====================================================
REDIRECTION (>, >>)
=====================================================

# Ausgabe in Datei speichern (überschreibt Inhalt)
ls > reports/files_list.txt

# Inhalt anzeigen
cat reports/files_list.txt

# Beispiel: Überschreiben
echo "first line" > reports/test.txt
echo "second line" > reports/test.txt
cat reports/test.txt

# Ergebnis: nur "second line"

# Beispiel: Anhängen (append)
echo "first line" > reports/test2.txt
echo "second line" >> reports/test2.txt
cat reports/test2.txt

# Ergebnis:
# first line
# second line

=====================================================
PIPES (|)
=====================================================

# Ausgabe von einem Befehl wird an den nächsten weitergegeben
cat data/errors.log | wc -l

# Ergebnis: Anzahl der Zeilen

=====================================================
HEAD & TAIL
=====================================================

# Erste Zeilen anzeigen
head data/access.log

# Erste 3 Zeilen
head -n 3 data/access.log

# Letzte Zeilen
tail data/access.log

# Letzte 3 Zeilen
tail -n 3 data/access.log

=====================================================
WC (WORD COUNT)
=====================================================

# Zeilen zählen
wc -l data/errors.log

# Wörter zählen
wc -w data/errors.log

# Zeichen zählen
wc -c data/errors.log

# Alles zusammen
wc data/errors.log

=====================================================
SORT
=====================================================

# Datei sortieren
sort data/users.txt

# Ergebnis in Datei speichern
sort data/users.txt > reports/sorted_users.txt

=====================================================
UNIQ
=====================================================

# Achtung: funktioniert nur bei sortierten Daten richtig

# Ohne sort (nicht korrekt)
uniq data/users.txt

# Mit sort (korrekt)
sort data/users.txt | uniq

# Häufigkeit zählen
sort data/users.txt | uniq -c

# Ergebnis:
# 3 ali
# 1 amina
# 1 karim
# 1 mehdi
# 2 sara
# 1 youssef

=====================================================
CUT
=====================================================

# Erstes Feld (IP) extrahieren
cut -d ' ' -f1 data/access.log

# Sortieren + zählen
cut -d ' ' -f1 data/access.log | sort | uniq -c

=====================================================
GREP (FILTERING)
=====================================================

# Nur ERROR anzeigen
grep "ERROR" data/errors.log

# Mit Zeilennummer
grep -n "ERROR" data/errors.log

# Anzahl zählen
grep -c "ERROR" data/errors.log

# Alles außer WARNING anzeigen
grep -v "WARNING" data/errors.log

# Groß-/Kleinschreibung ignorieren
grep -i "error" data/mixed.log

=====================================================
GREP + PIPELINES (ANALYSE)
=====================================================

# Nur GET Requests
grep "GET" data/access.log

# Nur POST Requests
grep "POST" data/access.log

# GET Requests analysieren (IPs zählen)
grep "GET" data/access.log | cut -d ' ' -f1 | sort | uniq -c

# Zugriff auf /admin analysieren
grep "/admin" data/access.log | cut -d ' ' -f1 | sort | uniq -c

# Ergebnis:
# 3 192.168.1.12

# Nicht-GET Requests analysieren
grep -v "GET" data/access.log | cut -d ' ' -f1 | sort | uniq -c

=====================================================
COMMAND CHAINING
=====================================================

# Alle Befehle ausführen
pwd ; ls ; date

# Nur wenn erster erfolgreich
mkdir testdir && cd testdir

# Nur wenn erster fehlschlägt
cd /fake/path || echo "directory not found"

=====================================================
ANALYST DENKEN
=====================================================

Fragen:
- Wie viele Zeilen gibt es?
- Welche Einträge sind häufig?
- Gibt es ungewöhnliche Muster?
- Welche IP greift auf sensitive Bereiche zu?
- Gibt es wiederholte Fehler?

Beispiel Analyse:
- ERROR = 3
- WARNING = 2
- GET > POST (normal)
- 192.168.1.12 greift 3x auf /admin zu (verdächtig)

=====================================================
REPORT ERSTELLEN
=====================================================

echo "=== Analysis Report ===" > reports/analysis_report.txt
echo "" >> reports/analysis_report.txt

echo "Total users lines:" >> reports/analysis_report.txt
wc -l < data/users.txt >> reports/analysis_report.txt

echo "Unique users:" >> reports/analysis_report.txt
sort data/users.txt | uniq | wc -l >> reports/analysis_report.txt

echo "Error count:" >> reports/analysis_report.txt
grep "ERROR" data/errors.log | wc -l >> reports/analysis_report.txt

echo "IP frequency:" >> reports/analysis_report.txt
cut -d ' ' -f1 data/access.log | sort | uniq -c >> reports/analysis_report.txt

=====================================================
SECURITY SUMMARY
=====================================================

echo "=== Security Summary ===" > reports/security_summary.txt
echo "" >> reports/security_summary.txt

echo "ERROR count:" >> reports/security_summary.txt
grep -c "ERROR" data/errors.log >> reports/security_summary.txt

echo "WARNING count:" >> reports/security_summary.txt
grep -c "WARNING" data/errors.log >> reports/security_summary.txt

echo "GET requests:" >> reports/security_summary.txt
grep -c "GET" data/access.log >> reports/security_summary.txt

echo "POST requests:" >> reports/security_summary.txt
grep -c "POST" data/access.log >> reports/security_summary.txt

echo "Admin access IP frequency:" >> reports/security_summary.txt
grep "/admin" data/access.log | cut -d ' ' -f1 | sort | uniq -c >> reports/security_summary.txt

cat reports/security_summary.txt

=====================================================
FAZIT
=====================================================

Heute habe ich gelernt:
- Daten gezielt zu filtern statt alles zu lesen
- Logs wie ein Analyst zu analysieren
- Mehrere Tools zu kombinieren (Pipes)
- Muster und Wiederholungen zu erkennen

Das ist die Grundlage für:
- Log Analysis
- SOC Arbeit
- Cyber Security Praxis
