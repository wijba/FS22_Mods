!addplugindir /x86-unicode "$%userprofile%\Downloads\Nsisunz\Plugin unicode"

!include LogicLib.nsh
; example1.nsi
;
; This script is perhaps one of the simplest NSIs you can make. All of the
; optional settings are left to their default settings. The installer simply 
; prompts the user asking them where to install, and drops a copy of example1.nsi
; there. 
;
; example2.nsi expands on this by adding a uninstaller and start menu shortcuts.

;--------------------------------

; The name of the installer
Name "FS22_Lucky_Farm-Mod_Installer"

; The file to write
OutFile "C:\Users\Erik\Desktop\fs22test\FS22_Lucky_Farm-Mod_Installer.exe"

; Request application privileges for Windows Vista
RequestExecutionLevel user

; Build Unicode installer
Unicode True

; The default installation directory
InstallDir "$PROFILE\Documents\My Games\FarmingSimulator2022\mods"

;--------------------------------

; Pages

Page directory
Page instfiles

;--------------------------------

Section "Dummy Section" SecDummy

    inetc::get /POPUP "" /CAPTION "FS22 Mods" "https://cloud.philos-stuff.de/s/bBxxW8GcSYq7TYZ/download" "$EXEDIR\mods.zip"
    Pop $0 # return value = exit code, "OK" if OK
    MessageBox MB_OK "Download Status: $0"

SectionEnd
Section

nsisunz::Unzip "$EXEDIR\mods.zip" $INSTDIR
Pop $0
DetailPrint $0 ; "success"

SectionEnd