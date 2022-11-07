Titel:        Dokumentation von Git/GitHub Repository
Date:        03.11.2022
Author:      Christopher Zwick
Keywords:   Git, GitHub, Linux



# Git Repository lokal erstellen
[ArchWiki](https://wiki.archlinux.org "ArchWiki")
![Alt-Text](Bilder/Archlinux.jpg)





## Projekt-Umgebung vorbereiten
### SSH Schluessel erstellen



   ssh-keygen



#### Kopieren PublicKey in GitHub



   cat .ssh/id_rsa.pub
    
#### Ueberpruefen die Verbindung mit GitHub



ssh -T git@github.com
git remote add origin



#### Erstellen Sie ein Verzeichnis mit dem Namen Projekt1



   cd
    mkdir Projekt1
    
#### Dateien und Verzeichnisse für das Projekt "Statische Webseite"



   touch index.html style.css backend.py
    mkdir Secret
    cd Secret
    touch Geheimnisse.txt
    cd ..
    mkdir Bilder
    cd Bilder
    touch Bild1.jpg Bild2.jpg Bild3.jpg Bild1.png Bild2.png
    cd ..
    touch .gitignore
    
#### Falls dass Sie sensible Daten verstecken wollen, schreiben Sie welche in .gitignore Datei



   nano .gitignore



Code-Blocke



   Secret/
    Bilder/*.png



#### Git-Umgebung vorbereiten
    
    git config --global user.name "Name Nachname"
    git config --global user.email "valid email"



#### git-Kontrollversionierung initialisieren



   git init
    
#### From Working Area nach Staging Area nach Repository
    
    git status
    git add -A
    git commit -m "Erstes Commit"
    git status



#### Lokal Repository "Push" zum GitHub



   git push -u origin master
