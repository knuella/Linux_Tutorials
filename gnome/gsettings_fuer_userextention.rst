gsettings für eine gnome-shell-extention, die vom user installiert wurde
==================================================================

Problem:
Alle Enstellungen werden von gnome in einer Datenbank verwaltet und können mit
gsettings (Terminal) und dconf-editor (gui) gelesen und verändert werden.
Werden Shell-Erweiterungen über die gnome inet-Seite
(https://extensions.gnome.org/) installiert, haben diese kein Schema und
erscheinen zwar im dconf-editor, können aber mit gsettings nicht erreicht
werden. gsettings greift meines Wissens nur über die Schemata auf die
Einstellungen zu (bitte korrigiert mich, wenn es andere Möglichkeiten gibt). 

Gnome scheint nur die Schemata einzulesen, die unter
"/usr/share/glib-2.0/schemas/" liegen. Die vom user installierten liegen aber
unter "~/.local/share/gnome-shell/extentions/.../schemas/".

Die Datei im home-Verzeichnis kann mit root-Rechten in das globale Verzeichnis
kopiert werden. 

Z.B. für die Shell Erweiterung TodoTxt:

.. code:: bash

  sudo cp org.gnome.shell.extensions.TodoTxt.gschema.xml /usr/share/glib-2.0/schema 

Danach muss das Schema kompiliert... (gleiches Beispiel)

.. code:: bash

  sudo glib-compile-schemas /usr/share/glib-2.0/schemas/org.gnome.shell.extensions.TodoTxt.gschema.xml 

... und die dconf datenbank aktualisiert werden: 

.. code:: bash

  sudo dconf update

Fertig!!!

Jetzt kann über gsettings und das Schema auf die Einstellungswerte zugegriffen werden: (immernoch gleiches Beispiel :-))

.. code:: bash

  gsettings get org.gnome.shell.extensions.TodoTxt todotxt-location


