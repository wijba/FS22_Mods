!addplugindir /x86-unicode "$%userprofile%\Downloads\Nsisunz\Plugin unicode"

!include LogicLib.nsh

; Simples Script um eine zip aus dem Internet herunterzuladen und dann zu entpacken.

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
	;inetc-plugin um eine zip herunterzuladen
    inetc::get /POPUP "" /CAPTION "FS22 Mods" "https://cloud.philos-stuff.de/s/bBxxW8GcSYq7TYZ/download" "$EXEDIR\mods.zip"
    Pop $0 # return value = exit code, "OK" if OK
    MessageBox MB_OK "Download Status: $0"

SectionEnd
Section
;mithilfe von nsiunz wird die zip in ein angegebenes Verzeichnis entpackt
nsisunz::Unzip "$EXEDIR\mods.zip" $INSTDIR
Pop $0
DetailPrint $0 ; "success"

SectionEnd