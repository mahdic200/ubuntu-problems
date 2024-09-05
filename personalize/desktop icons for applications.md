navigate to `~/.local/share/applications` . there should be some file with prefix `.desktop` . if it's not then you can create one . this is an example of how to do it .

```shell
nano dev.zed.Zed-Preview.desktop
```

then put these lines in it :
```config
[Desktop Entry]
Version=1.0
Type=Application
Name=Zed
GenericName=Text Editor
Comment=A high-performance, multiplayer code editor.
TryExec=/home/mahdi/.local/zed-preview.app/libexec/zed-editor
StartupNotify=true
Exec=/home/mahdi/.local/zed-preview.app/libexec/zed-editor %U
Icon=zed
Categories=Utility;TextEditor;Development;IDE;
Keywords=zed;
MimeType=text/plain;inode/directory;x-scheme-handler/zed;
Actions=NewWorkspace;

[Desktop Action NewWorkspace]
Exec=/home/mahdi/.local/zed-preview.app/libexec/zed-editor --new %U
Name=Open a new workspace
Icon=zed

```

you can specify the executable binary , the Icon and the path etc .