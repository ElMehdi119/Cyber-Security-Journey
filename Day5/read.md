# Day 5 - Prozesse verstehen und überwachen

## Kurze Zusammenfassung
Heute habe ich gelernt, wie Prozesse in Linux funktionieren und wie man sie analysiert. Ich habe ps, top, pgrep und pidof verwendet, um laufende Prozesse zu sehen, zu filtern und zu verstehen. Außerdem habe ich gelernt, wie man CPU- und RAM-Verbrauch interpretiert, die Prozessstruktur (PPID) liest und grundlegende Signals sowie den sicheren Umgang mit kill versteht.

## Was ich heute konkret gemacht habe
1. Prozesse mit ps und ps aux angezeigt
2. Prozesse mit grep gefiltert (bash, ssh)
3. Eigene Prozesse mit ps -u $USER analysiert
4. Prozessbaum mit ps -ef --forest untersucht
5. Live-Überwachung mit top durchgeführt
6. Prozesse nach CPU und RAM sortiert
7. STAT und PPID verstanden und interpretiert
8. Prozesse gezielt mit pgrep und pidof gefunden
9. Signals mit kill -l kennengelernt
10. Unterschied zwischen kill und kill -9 verstanden
11. Erste Erfahrung mit foreground und background Prozessen gemacht

## Befehle + Erklärung + Beispiele (alles zusammen)

# ps
# Bedeutung:
# Zeigt Prozesse der aktuellen Terminal-Session

# Beispiel:
ps

# Ergebnis:
PID TTY          TIME CMD
1591 pts/0    00:00:00 zsh
2773 pts/0    00:00:00 ps

# ps aux
# Bedeutung:
# Zeigt alle Prozesse im System mit Details

# Beispiel:
ps aux

# Ergebnis:
USER   PID %CPU %MEM COMMAND
root     1  0.3  0.3 /sbin/init
mehdi  1591 0.2  0.1 /usr/bin/zsh

# ps aux | head
# Bedeutung:
# Zeigt nur die ersten Zeilen der Prozessliste

# Beispiel:
ps aux | head

# Ergebnis:
USER   PID %CPU %MEM COMMAND
root     1  0.1  0.3 /sbin/init
root     2  0.0  0.0 [kthreadd]

# ps aux | grep bash
# Bedeutung:
# Sucht nach Prozessen mit dem Namen bash

# Beispiel:
ps aux | grep bash

# Ergebnis:
mehdi 5738 0.0 0.0 grep --color=auto bash

# ps aux | grep ssh
# Bedeutung:
# Sucht nach ssh-Prozessen

# Beispiel:
ps aux | grep ssh

# Ergebnis:
mehdi 1162 0.0 0.0 /usr/bin/ssh-agent -s

# ps -u $USER
# Bedeutung:
# Zeigt alle Prozesse des aktuellen Benutzers

# Beispiel:
ps -u $USER

# Ergebnis:
PID CMD
1011 xfce4-session
1533 qterminal
1591 zsh

# ps -ef --forest
# Bedeutung:
# Zeigt die Prozessstruktur (Parent-Child Beziehung)

# Beispiel:
ps -ef --forest

# Ergebnis:
qterminal
 └── zsh
     └── ps -ef --forest

# top
# Bedeutung:
# Zeigt Prozesse live mit CPU- und RAM-Nutzung

# Beispiel:
top

# Ergebnis:
Tasks: 151 total
%CPU(s): 99.0 id
PID USER %CPU %MEM COMMAND
709 root 0.3 2.4 Xorg

# ps aux --sort=-%cpu | head
# Bedeutung:
# Sortiert Prozesse nach CPU-Verbrauch (höchste zuerst)

# Beispiel:
ps aux --sort=-%cpu | head

# Ergebnis:
root 709 0.4 Xorg
mehdi 1591 0.3 zsh

# ps aux --sort=-%mem | head
# Bedeutung:
# Sortiert Prozesse nach RAM-Verbrauch

# Beispiel:
ps aux --sort=-%mem | head

# Ergebnis:
mehdi 1174 3.4 xfwm4
root 709 2.4 Xorg

# ps -eo pid,ppid,user,%cpu,%mem,stat,cmd
# Bedeutung:
# Zeigt Prozesse mit detaillierten Spalten

# Beispiel:
ps -eo pid,ppid,user,%cpu,%mem,stat,cmd

# Ergebnis:
PID PPID USER %CPU %MEM STAT CMD
1591 1533 mehdi 0.2 0.1 Ss /usr/bin/zsh

# pgrep zsh
# Bedeutung:
# Findet die PID von zsh

# Beispiel:
pgrep zsh

# Ergebnis:
1591

# pgrep -a zsh
# Bedeutung:
# Zeigt PID + vollständigen Befehl

# Beispiel:
pgrep -a zsh

# Ergebnis:
1591 /usr/bin/zsh

# pidof zsh
# Bedeutung:
# Alternative Methode zur PID-Suche

# Beispiel:
pidof zsh

# Ergebnis:
1591

# kill -l
# Bedeutung:
# Zeigt alle verfügbaren Signals

# Beispiel:
kill -l

# Ergebnis:
HUP INT TERM KILL STOP CONT

# sleep 200 &
# Bedeutung:
# Startet einen Prozess im Hintergrund

# Beispiel:
sleep 200 &

# Ergebnis:
[1] 7021

# pgrep -a sleep
# Bedeutung:
# Findet laufende sleep-Prozesse

# Beispiel:
pgrep -a sleep

# Ergebnis:
7021 sleep 200

# kill 7021
# Bedeutung:
# Beendet einen Prozess sauber (SIGTERM)

# Beispiel:
kill 7021

# Ergebnis:
Prozess wird beendet
