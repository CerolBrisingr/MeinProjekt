# GitHub/GitLab (K4.0057_2.0_VZ)
## Prüfungsabgabe  
* Codeblöcke bzw. Konsoleneingaben innerhalb dieses Readme verwenden C-Syntax für Kommentare
* Screenshots liegen im Zip-File in den Verzeichnissen a, b und c passend zu den Übungsaufgaben

## a) GitHub Repository Setup
* Benutzerkonto auf GitHub ist vorhanden: *CerolBrisignr*
* Projekt ist zu finden unter: https://github.com/CerolBrisingr/MeinProjekt

## b) SSH-Schlüssel erstellen
* SSH-Schlüssel wurden anlässlich des passenden Kapitels hinzugefügt
* Aus der git-bash unter Windows ausgeführt landeten die SSH-Dateien im lokalen Verzeichnis
* Dateien nach ~/.ssh verschoben und ~/.ssh/config angelegt
```
        Host github.com
            ForwardAgent yes
            HostName github.com
            IdentityFile ~/.ssh/git_id
```
* Das Einrichten des ssh-Agenten unter Windows ist etwas umständlich:
```
        eval "$(ssh-agent -s)"
        ssh-add ~/.ssh/git_id
```
* Für den Moment bringe ich diese Prozedur in einer ./bashrc Datei unter. Möglicherweise bevorzuge ich in Zukunft ein Makro/Alias.

## c) Lokales Repository einrichten und Workflow
* Das Klonen mit dem durch GitHub selbst vorgeschlagenen Pfad schlägt zunächst fehl, nach Test mit ssh bei denen sich kein unerwartetes Verhalten zeigt funktioniert das Klonen. Möglich, dass der Zugang durch GitHub nicht unmittelbar freigeschaltet wurde.
```
        ssh -T git@github.com
        ssh -T CerolBrisingr@github.com
```
* Der erste Commit erscheint im Log noch mit den Standard-Credentials von GitHub, anschließend ist die neue Konfiguration gesetzt. Evtl. nicht zu clever, wenn's um Spam geht.
```
 8) cd ProjectParent
 9) git clone git@github.com:CerolBrisingr/MeinProjekt.git
10) cd MeinProjekt
11) git config user.name "Sebastian Baur"
    git config user.email "bastianbaur@gmx.de"
12) touch main.py // leer da Inhalt soweit irrelevant
    git add main.py
    git commit -m "Initialer Commit"
13) git switch -c feature
14) mkdir utils
    touch utils/database.py // leer da Inhalt irrelevant
    git add utils/database.py
    git commit -m "Neue Funktion hinzugefügt"
15) git switch main // GitHub verwendet "main", nicht "master"
16) notepad++ main.py
    git add main.py
    git commit -m "Hauptdatei aktualisiert"
17) git merge feature
    /*
    Beachte: Der in der Aufgabe angesprochene
    Merge-Konflikt passiert nicht, da main.py auf dem
    Feature-Branch zu keinem Zeitpunkt modifiziert wird.
     Im Anschluss wird noch ein Merge-Konflikt mit einem
    weiteren Feature-Branch provoziert.
    */
```

## Bonus
```
git switch -c feature2 // could have deleted feature 1 and gone again
notepad++ main.py // Modified main.py, more in the conflict
git add main.py
git commit -m "made an actual python file out of main.py"
git switch main
notepad++ main.py // Modified main.py
git add main.py
git commit -m "changed the existing line in main.py"
git merge feature2 // Keeping changes from feature branch
git add main.py
git commit
git push
```
Der auftretende Konflikt wird durch konkurrierende Änderungen auf den beiden merged Branches verursacht. Auf beiden Branches geschehen Änderungen an der selben Zeile in main.py.  
Ein Branch (main) ändert lediglich die vorhandene Zeile. Der andere Branch (feature2) ändert die komplette Datei, damit auch die existierende Zeile. Der Konflikt sieht dabei wie folgt aus:
```
<<<<<<< HEAD
# changing this line
=======
def sayHello():
    print("Hallo Welt und VelpTEC!")
    
sayHello()
>>>>>>> feature2
```
In diesem Fall behalten wir einfach den Inhalt von feature2.