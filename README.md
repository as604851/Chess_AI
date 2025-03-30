## Convert PGN-string into vector:

Der Code verarbeitet eine Liste von Schachzügen aus einer Datei, simuliert die Spielverläufe und speichert die daraus resultierenden Brettzustände in einer CSV-Datei. Dabei wird jedes Schachbrett in eine numerische Vektorform umgewandelt, die sich für maschinelles Lernen nutzen lässt.
Zunächst wird ein Schachbrett als Datenstruktur implementiert:
![image](https://github.com/user-attachments/assets/dafa72e7-3be9-4b41-8a9b-388d0a97e709)

Es besteht aus einer 8×8-Matrix, in der leere Felder durch Punkte und Schachfiguren durch ihre jeweiligen Zeichen dargestellt werden. Zusätzlich wird festgehalten, welcher Spieler am Zug ist. Die Umwandlung des Bretts in eine numerische Darstellung erfolgt über eine Zuordnung von Zahlenwerten zu den einzelnen Figuren. Ein weißer Bauer ist als -1 und ein schwarzer als 1 kodiert werden, während der aktuelle Spieler als zusätzliche Information (0 für Weiß, 1 für Schwarz) mitgespeichert wird:
![image](https://github.com/user-attachments/assets/eed2e9fe-9727-41ef-9df8-142f0995cbb8)

Die Verarbeitung der Züge beginnt mit dem Einlesen einer Textdatei, die eine Sequenz von Schachzügen enthält. Diese Züge werden analysiert und nach festgelegten Regeln interpretiert. Für jeden Zug wird die entsprechende Figur auf dem virtuellen Schachbrett platziert, wobei darauf geachtet wird, dass Schwarz und Weiß korrekt unterschieden werden. Nach jedem Zug wird der aktuelle Brettzustand in einen Zahlenvektor umgewandelt und in eine CSV-Datei geschrieben. Dabei wird auch das Spielergebnis gespeichert, das entweder einen Sieg für Weiß (1-0), einen Sieg für Schwarz (0-1) oder ein Unentschieden widerspiegelt.
Während der Verarbeitung wird überprüft, ob die Züge gültig sind. Falls ein ungültiger Zug auftritt, wird eine Warnung ausgegeben. Am Ende steht eine CSV-Datei, die für jedes Brett eine numerische Repräsentation enthält, ergänzt durch das finale Spielergebnis. Diese Datenstruktur könnte beispielsweise für maschinelles Lernen genutzt werden, um Muster in Schachpartien zu erkennen oder eine KI zu trainieren.

## Training AI: 

Der gegebene Code implementiert ein neuronales Netzwerk zur Klassifikation von Schachpartien basierend auf einer CSV-Datei mit Spielinformationen. Zunächst werden die notwendigen Bibliotheken importiert, darunter pandas für die Datenverarbeitung, scikit-learn für das Aufteilen der Daten und die Umwandlung der Labels, tensorflow.keras für das Erstellen und Trainieren des Modells sowie matplotlib und networkx für die Visualisierung.
Die Daten werden aus einer CSV-Datei geladen, wobei die Spalte mit den Labels (Label:1-0) von den Eingangsmerkmalen (X) getrennt wird. Die Zielwerte (y) werden anschließend in numerische Kategorien umgewandelt und in das One-Hot-Format gebracht, um sie für das neuronale Netzwerk nutzbar zu machen. Danach werden die Daten in ein Trainings- und ein Testset aufgeteilt.
Das neuronale Netzwerk wird mit der Sequential-API von Keras erstellt. Es besteht aus einer Eingabeschicht, die sich an der Anzahl der Eingangsmerkmale orientiert, zwei versteckten Schichten mit 64 bzw. 32 Neuronen und einer Ausgabeschicht, deren Größe der Anzahl der Klassifikationsmöglichkeiten entspricht. Die Aktivierungsfunktion in den versteckten Schichten ist ReLU, während in der Ausgabeschicht softmax verwendet wird, um Wahrscheinlichkeiten für die verschiedenen Klassen zu erzeugen. Das Modell wird mit der categorical_crossentropy-Verlustfunktion und dem adam-Optimierer kompiliert.
Beim Training des Modells wird ein Mechanismus zum Early Stopping verwendet, der das Training automatisch beendet, wenn sich die Validierungsverlustwerte über mehrere Epochen hinweg nicht verbessern. Nach dem Training wird das Modell gespeichert und anschließend erneut geladen, um Vorhersagen auf dem Testdatensatz zu treffen.
Zum Schluss wird mithilfe der networkx-Bibliothek ein gerichteter Graph erstellt, der die Struktur des neuronalen Netzes visualisiert. 
![image](https://github.com/user-attachments/assets/dc44d258-3500-4470-8156-58b5e66a4a95)

Dabei werden die Neuronen der verschiedenen Schichten als Knoten und die Verbindungen zwischen ihnen als gewichtete Kanten dargestellt. Ein auskommentierter Codeabschnitt zeigt zudem eine Möglichkeit, die Verbindungen farblich zu visualisieren.

