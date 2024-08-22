# GitHub/GitLab (K4.0057_2.0_VZ)
Prüfungsabgabe 

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