# Day 4 - Linux Permissions & Ownership (Security Thinking)

## Kurze Zusammenfassung
Heute habe ich mein Verständnis von Linux-Berechtigungen vertieft. Ich habe gelernt, wie man Permissions mit Symbolen ändert, wie Ownership funktioniert und warum Schreibrechte (write) gefährlich sind. Außerdem habe ich SetUID kennengelernt und verstanden, wie dadurch Privilege Escalation möglich wird.

## Was ich heute konkret gemacht habe
1. Symbolische Permissions mit chmod verwendet (u, g, o)
2. Schreib-, Lese- und Ausführungsrechte gezielt geändert
3. Ownership mit chown verändert (owner und group)
4. Sicherheitsrisiken von write-Rechten analysiert
5. SetUID (u+s) praktisch angewendet
6. Eine Bash mit root-Rechten ausgeführt (Privilege Escalation)

## Befehle + Erklärung + Beispiele (alles zusammen)

# chmod u+x file
# Bedeutung:
# Fügt dem Owner Ausführungsrechte hinzu

# Beispiel:
chmod u+x test_perm.txt

# Ergebnis:
-rwxrwx--x


# chmod g+w file
# Bedeutung:
# Fügt der Gruppe Schreibrechte hinzu

# Beispiel:
chmod g+w test_perm.txt

# Ergebnis:
-rwxrwx--x


# chmod o-r file
# Bedeutung:
# Entfernt Leserechte für andere Benutzer

# Beispiel:
chmod o-r test_perm.txt

# Ergebnis:
-rwxrwx---


# chmod u+rwx,g+rx,o-rwx file
# Bedeutung:
# Setzt kombinierte Rechte für Owner, Gruppe und andere

# Beispiel:
chmod u+rwx,g+rx,o-rwx test_perm.txt

# Ergebnis:
-rwxr-x---


# chmod +x file
# Bedeutung:
# Fügt Ausführungsrechte für alle hinzu

# Beispiel:
chmod +x test_perm.txt

# Ergebnis:
-rwxr-xr-x


# sudo chown root file
# Bedeutung:
# Ändert den Besitzer der Datei zu root

# Beispiel:
sudo chown root attack.txt

# Ergebnis:
-rwxrwxrwx 1 root mehdi


# sudo chown user:group file
# Bedeutung:
# Ändert Besitzer und Gruppe gleichzeitig

# Beispiel:
sudo chown mehdi:root secure.txt

# Ergebnis:
-rw-r----- 1 mehdi root


# chmod 777 file
# Bedeutung:
# Gibt allen vollständige Rechte (lesen, schreiben, ausführen)

# Beispiel:
chmod 777 public.txt

# Ergebnis:
-rwxrwxrwx


# chmod 600 file
# Bedeutung:
# Nur Owner darf lesen und schreiben

# Beispiel:
chmod 600 private.txt

# Ergebnis:
-rw-------


# chmod 755 file
# Bedeutung:
# Owner hat volle Rechte, andere dürfen lesen und ausführen

# Beispiel:
chmod 755 script.sh

# Ergebnis:
-rwxr-xr-x


# cp /bin/bash mybash
# Bedeutung:
# Kopiert die Bash in eine neue Datei

# Beispiel:
cp /bin/bash mybash

# Ergebnis:
-rwxr-xr-x mybash


# sudo chown root mybash
# Bedeutung:
# Setzt root als Besitzer der Datei

# Beispiel:
sudo chown root mybash

# Ergebnis:
-rwxr-xr-x root


# sudo chmod u+s mybash
# Bedeutung:
# Setzt das SetUID-Bit (Ausführung als Owner)

# Beispiel:
sudo chmod u+s mybash

# Ergebnis:
-rwsr-xr-x


# ./mybash -p
# Bedeutung:
# Startet Bash mit gesetztem SetUID

# Beispiel:
./mybash -p

# Ergebnis:
root


# whoami
# Bedeutung:
# Zeigt den aktuellen Benutzer

# Beispiel:
whoami

# Ergebnis:
root
