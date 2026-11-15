# GitHub-Einrichtung für BlackIce FW

## Repository-Einstellungen

- Vorgeschlagener Repository-Name: `blackice-fw`
- Sichtbarkeit: **Private**
- Standardbranch: `main`
- Paketstand: BlackIce `v29.14.4`, UI Fix 27

**Nicht auf Public umstellen.** Der aktuelle Quellstand enthält noch die aktive V1-Lizenzkompatibilität mit eingebettetem gemeinsamem Prüfgeheimnis. Siehe `PUBLIC_RELEASE_BLOCKER.md`.

## Paket lokal entpacken

Das ZIP enthält einen Ordner `BlackIce-FW`. Entpacken Sie das Archiv in einen lokalen Arbeitsordner und öffnen Sie PowerShell in diesem Ordner.

## Repository initialisieren und hochladen

Nach dem Erstellen eines privaten GitHub-Repositorys `blackice-fw` die folgenden Befehle aus dem entpackten Ordner `BlackIce-FW` ausführen. `<OWNER>` durch den eigenen GitHub-Benutzernamen oder die Organisation ersetzen:

```powershell
git init
git add .
git status
git commit -m "Prepare BlackIce FW v29.14.4 UI Fix 27"
git branch -M main
git remote add origin https://github.com/<OWNER>/blackice-fw.git
git push -u origin main
```

Vor `git commit` die Ausgabe von `git status` prüfen. Es dürfen keine lokalen Tresor-, Datenbank-, DPAPI-, Recovery-, API-Key- oder Lizenzdateien vorgemerkt sein.

## GitHub Release anlegen

Erst nach einem erfolgreichen vollständigen Windows-Build und den dort dokumentierten Funktionstests ein GitHub Release erstellen:

- Tag: `v29.14.4`
- Titel: `BlackIce Δ v29.14.4 — UI Fix 27`
- Release-Beschreibung: `docs/RELEASE_NOTES_v29.14.4.md`
- Release-Dateien: die sechs Komponenten-Artefakte und das kombinierte Release-ZIP aus dem `dist`-Ordner gemäß `README-COMPLETE-BUILD.md`, dazu die SHA-256-Manifeste.

Das hier gelieferte Repository-ZIP ist ein **Quellcode-/Entwicklerpaket**, kein fertiges Kundeninstallationspaket. Die Installer und binären Client-ZIPs müssen auf Windows gebaut werden.
