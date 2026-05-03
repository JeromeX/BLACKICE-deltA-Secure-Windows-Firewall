# 🛡️ BLACKICE deltA V28.04 - NEURAL PULSE

![Version](https://img.shields.io/badge/VERSION-28.04_NEURAL_PULSE-00FFFF?style=for-the-badge)
![Security](https://img.shields.io/badge/SECURITY-MAIN_FIREWALL_OVERRIDE-RED?style=for-the-badge)
![License](https://img.shields.io/badge/LICENSE-PROPRIETARY-RED?style=for-the-badge)
![Tech](https://img.shields.io/badge/TECH-C%23_|_WPF_|_WFP-8A2BE2?style=for-the-badge)
![Platform](https://img.shields.io/badge/PLATFORM-WINDOWS_10_/_11-0078D6?style=for-the-badge&logo=windows)
![Architecture](https://img.shields.io/badge/ARCHITECTURE-X64_|_AMD64-ORANGE?style=for-the-badge)

**BLACKICE deltA** ist eine hochperformante **Main-Firewall-Suite**, die als vollständiger Ersatz für die Windows-Firewall-Logik konzipiert wurde. Basierend auf der **Windows Filtering Platform (WFP)** bietet sie Kernel-nahe Sicherheit, gepaart mit einer reaktionsschnellen Cyber-Matrix-Oberfläche.
<img width="1450" height="850" alt="2026-05-03 15_00_25-BlackIce deltA Suite" src="https://github.com/user-attachments/assets/e4ebb4df-7778-467e-ad44-7e51aac62e6a" />
<img width="1448" height="850" alt="2026-05-03 15_04_10-BlackIce deltA Suite" src="https://github.com/user-attachments/assets/0ef7945e-0a8a-41fd-9e28-54bec40bc19a" />

---

## ⚠️ KRITISCHES SICHERHEITSPROTOKOLL: LIZENZ & LOCKOUT
Um die Integrität des Systems ab der ersten Sekunde zu gewährleisten, nutzt BLACKICE deltA ein **Pre-Activation Lockout System**:

1.  **Globaler Lock:** Sofort nach der Installation wird jeglicher ein- und ausgehende Internetverkehr blockiert.
2.  **Lizenz-Validierung:** Das System erfordert einen gültigen Lizenzkey, der kryptografisch an die Hardware-ID (HWID) gebunden ist (SHA-256 Checksumme).
3.  **Freischaltung:** Erst nach erfolgreicher Verifizierung wird der Netzwerkstack freigegeben. Dies verhindert Zero-Day-Kommunikation von Schadsoftware während der Setup-Phase.

---

## ⚡ Core Features & Funktionen

### 🧩 Main-Firewall Override & Dienst-Modus
*   **Volle System-Kontrolle:** Übernimmt alle Funktionen der nativen Windows-Firewall.
*   **Kernel-Level-Service:** Operiert als privilegierter Windows-Dienst (`BlackIceDeltASvc`). Er startet vor dem Benutzer-Login und schützt den Boot-Vorgang.
*   **Persistence:** Manipulationsgeschützte Dienst-Struktur, die unbefugtes Deaktivieren verhindert.

### 📊 Neural Pulse Dashboard (V28.04 Spezial)
*   **Neural EKG Engine:** Echtzeit-Header-Scanner, der Hostname und Zeit in einer flüssigen EKG-Animation visualisiert.
*   **Time-Synced Monitoring:** Die EKG-Linien in der Prozessliste sind mit der Systemzeit synchronisiert, um flüssige, unterbrechungsfreie Animationen bei Daten-Refreshes zu garantieren.
*   **Cyber-Blue Interaction:** Fenstermanagement-Buttons (Minimieren/Schließen) in **Bold**-Optik mit intensivem **DeepSkyBlue-Neon-Glow** bei Mouseover.

### 🛡️ Erweiterte Abwehrmechanismen
*   **Life Saver (Killswitch):** Sofortige Isolation vom Internet (WAN), während lokale Netzwerkressourcen (LAN) erreichbar bleiben.
*   **App-Inquisitor:** Permanente Isolation spezifischer ausführbarer Dateien (.exe) vom Netzwerk.
*   **Domain-Neural-Resolve:** Dynamische Sperrung von Domains durch automatische, asynchrone Hintergrund-Auflösung aller zugehörigen IP-Adressen.
*   **NOVA AI Assistant:** Kontextsensitive Analyse der Firewall-Regeln zur Erkennung von Fehlkonfigurationen.

---

## 🛠️ Technische Spezifikationen

### Architektur & Stack
*   **Programmiersprache:** C# 12.0
*   **Framework:** .NET 8 / .NET 9 (LTS)
*   **UI-Engine:** WPF (Windows Presentation Foundation) mit hardwarebeschleunigtem Vektor-Rendering.
*   **Datenhaltung:** AES-256 verschlüsselte **SQLite** Datenbank für Logs und Regelwerke.
*   **Schnittstellen:** Direkte Integration in die **Windows Filtering Platform (WFP)** API.

### Anforderungen
*   **OS:** Windows 10 (1903+) / Windows 11 (x64/ARM64).
*   **Privilegien:** Administratorrechte zwingend erforderlich.
*   **Ressourcen:** <30MB RAM im Dienst-Modus; optimiert für minimale CPU-Last trotz Neural-Pulse-Animationen.

---

## 🔑 Lizenzierung
Dieses Projekt ist proprietär. Jede Installation erfordert eine Hardware-gebundene Lizenz.
*   **Hardware-ID:** Gebunden an Mainboard & CPU.
*   **Updates:** Lebenslanger Zugriff auf Definitions-Updates innerhalb der Hauptversion V28.

### © 2026 | Malte Speck | BLACKICE deltA - Neural Pulse Project
