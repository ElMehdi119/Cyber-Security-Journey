# Day 1 — Linux Grundlagen (Navigation & Permissions)

## 🧾 Zusammenfassung (Kurz & Klar)
Heute habe ich gelernt:
- Wie ich mich im Linux-System bewege (Navigation)
- Wie ich Dateien und Ordner aufliste
- Wie ich Details von Dateien sehe
- Wie Berechtigungen (Permissions) funktionieren
- Wie ich Berechtigungen ändere (chmod)
- Warum falsche Berechtigungen ein Sicherheitsrisiko sind

---

## 📂 Navigation Befehle

### Befehl:
pwd

### Erklärung:
Zeigt den aktuellen Pfad (wo ich mich im System befinde)

### Beispiel:
pwd
→ /home/mehdi

---

### Befehl:
ls

### Erklärung:
Listet alle Dateien und Ordner im aktuellen Verzeichnis

### Beispiel:
ls
→ Bilder Dokumente Downloads ...

---

### Befehl:
ls -l

### Erklärung:
Zeigt detaillierte Informationen:
- Permissions
- Owner
- Größe
- Datum

### Beispiel:
ls -l
→ drwxr-xr-x 2 mehdi mehdi 4096 Apr 7 Bilder

---

### Befehl:
cd

### Erklärung:
Wechselt das Verzeichnis

### Beispiele:
cd Downloads
cd ..
cd ~

---

## 🔐 Permissions (Berechtigungen)

### Grundprinzip:
r = read (lesen) = 4  
w = write (schreiben) = 2  
x = execute (ausführen) = 1  

---

### Struktur:
rwx | r-x | r-x  
Owner | Group | Others

---

### Beispiel:
-rw-rw-r--

Erklärung:
- Owner: lesen + schreiben
- Group: lesen + schreiben
- Others: nur lesen

---

## ⚙️ Datei erstellen

### Befehl:
touch test.txt

### Erklärung:
Erstellt eine leere Datei

### Beispiel:
touch test.txt
ls -l
→ -rw-rw-r-- test.txt

---

## 🔒 Permissions ändern (chmod)

### Befehl:
chmod 000 test.txt

### Erklärung:
Niemand hat Zugriff

### Ergebnis:
---------- test.txt

---

### Befehl:
chmod 600 test.txt

### Erklärung:
Nur Owner darf lesen + schreiben

### Ergebnis:
-rw------- test.txt

---

### Befehl:
chmod 777 test.txt

### Erklärung:
Jeder darf alles (lesen, schreiben, ausführen)

### Ergebnis:
-rwxrwxrwx test.txt

⚠️ Gefahr:
Jeder kann Datei verändern → Sicherheitsrisiko

---

## 🧪 Mini Lab (Praxis)

### Befehle:
mkdir cyber_day1
cd cyber_day1

touch fileA fileB
mkdir secret_folder

chmod 700 secret_folder
chmod 600 fileA
chmod 777 fileB

ls -l

---

## 🔍 Analyse

### secret_folder:
drwx------

→ Nur Owner hat Zugriff

---

### fileA:
-rw-------

→ Nur Owner kann lesen und schreiben

---

### fileB:
-rwxrwxrwx

→ Jeder kann alles → gefährlich

---

## ⚠️ Sicherheitsverständnis

- 777 = komplett unsicher
- 600 = privat & sicher
- 700 = sicherer Ordner

- 4 = read (r)
- 2 = write (w)
- 1 = execute (x)

👉 Kontrolle über Permissions = Grundlage von Cyber Security

---
