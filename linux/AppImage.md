
download .appImage
place in /home/jake/data/applications
create applicationName.desktop in
/usr/share/applications

application file should look like so:


[Desktop Entry]
Exec=/home/jake/data/applications/Obsidian-1.1.9.AppImage
Name=Obsidian
Type=Application
StartupWMClass=obsidian
Icon=obsidian
Comment=Markdown Notetaking App
Terminal=false
GenericName=Text Editor
MimeType=x-scheme-handler/obsidian;

if no icon is found you can download it and place it in
/usr/share/pixmaps
