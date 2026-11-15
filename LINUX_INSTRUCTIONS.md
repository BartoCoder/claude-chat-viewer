# Linux Guide

Claude Chat Viewer for Linux is distributed as a portable **AppImage** file.

## 📥 Installation

1. Download the latest `.AppImage` file.
2. Open your terminal and navigate to the folder where the file was downloaded.
3. Make the script executable and run the installation script:

```bash
chmod +x Claude*.AppImage
```

4. Run the following command to automatically extract the icon and add the app to your application menu:

```bash
APP=$(ls -t Claude*.AppImage | head -n1)
chmod +x "$APP"
./"$APP" --appimage-extract >/dev/null
ICON=$(find squashfs-root -name "*.png" | head -n1)
cp -L "$ICON" ~/.local/share/icons/claude-chat-viewer.png

cat > ~/.local/share/applications/claude-chat-viewer.desktop <<EOL
[Desktop Entry]
Name=Claude Chat Viewer
Exec=$(pwd)/$APP %U
Icon=$HOME/.local/share/icons/claude-chat-viewer.png
Type=Application
Categories=Utility;
Terminal=false
EOL

rm -rf squashfs-root
update-desktop-database ~/.local/share/applications/ 2>/dev/null || true
echo "✅ Success! App added to menu."
```

## 🗑️ Uninstallation
To completely remove the application shortcut and icon, run:

```bash
rm -f ~/.local/share/applications/claude-chat-viewer.desktop
rm -f ~/.local/share/icons/claude-chat-viewer.png
update-desktop-database ~/.local/share/applications/ 2>/dev/null || true
echo "✅ Claude Chat Viewer has been removed from your application menu."
```

## 🔄 Updates
The application supports automatic updates. If a new version is available, it will download and replace the AppImage file automatically.

---

## Note
The shortcut in your application menu will continue to work, as long as you do not move or rename the AppImage file after installation.
