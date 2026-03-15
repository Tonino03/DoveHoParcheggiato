# 🚗 DoveHoParcheggiato - Smart Parking Assistant
[![Kotlin](https://img.shields.io/badge/Kotlin-1.9+-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)](https://kotlinlang.org/)
[![Android](https://img.shields.io/badge/Android-SDK%2024+-3DDC84?style=for-the-badge&logo=android&logoColor=white)](https://developer.android.com/)
[![Room](https://img.shields.io/badge/Database-Room-orange?style=for-the-badge&logo=sqlite&logoColor=white)](#)
[![Google Maps](https://img.shields.io/badge/Google%20Maps-API-4285F4?style=for-the-badge&logo=googlemaps&logoColor=white)](https://developers.google.com/maps)

> Un'applicazione nativa Android che combina geolocalizzazione, sensori di movimento e persistenza dati per eliminare lo stress della ricerca del veicolo.

---

## 🌟 Obiettivi del Progetto
L'app nasce per fornire uno strumento **affidabile e immediato**. A differenza di molte app simili che automatizzano il salvataggio (spesso fallendo in zone con scarso segnale), **DoveHoParcheggiato** punta sul controllo manuale semplificato per garantire precisione massima e risparmio energetico della batteria.

### ✨ Funzionalità Core
* **📍 Salvataggio Manuale GPS:** Registrazione esplicita del parcheggio con associazione della targa.
* **🗺️ Mappa Interattiva & Orientamento:** Supporto al magnetometro per una mappa che ruota seguendo la direzione dell'utente (effetto bussola).
* **🚶 Navigazione Pedonale:** Tracciamento del percorso tramite **Polyline** dinamiche grazie all'integrazione delle Google Directions API.
* **⏲️ Parking Timer:** Notifiche di sistema per avvisare della scadenza della sosta (ideale per zone blu).
* **🌐 Multilingua Dinamico:** Supporto a Italiano, Inglese e Spagnolo gestito a runtime.
* **🌓 Tema Adattivo:** Supporto nativo alla Dark Mode per Google Maps e interfaccia.

---

## 🛠️ Architettura Tecnica & Classi
Il progetto segue i moderni standard di sviluppo Android, gestendo la complessità dei permessi e delle operazioni asincrone.

| Modulo | Componente | Responsabilità |
| :--- | :--- | :--- |
| **UI Layer** | `MapActivity` / `MainActivity` | Gestione mappa, permessi runtime e coordinamento sensori. |
| **Data Layer** | `Room` (AppDatabase) | Persistenza della posizione e della targa anche dopo la chiusura dell'app. |
| **Networking** | `Retrofit` | Interfacciamento con Google Directions API per il parsing dei percorsi JSON. |
| **Background** | `BroadcastReceiver` | Gestione delle notifiche e dei promemoria sosta in background. |
| **Sensors** | `Magnetometer/Gyroscope` | Orientamento dinamico della camera per un'esperienza di navigazione fluida. |

---

## 🧠 Deep Dive: Sfide Sviluppate

### 🛡️ Gestione Permessi Runtime
Implementazione di un flusso robusto per `ACCESS_FINE_LOCATION` e notifiche, con gestione dei casi di rifiuto utente tramite `PermissionScreen` dedicato.

### 🧵 Concorrenza e Coroutine
Per evitare freeze della UI (Main Thread), tutte le operazioni sul database Room e le chiamate API di navigazione sono gestite tramite **Kotlin Coroutines** (`lifecycleScope.launch`).

### 🌍 Localizzazione Dinamica
Implementazione manuale di un `ContextWrapper` per forzare il cambio lingua nell'app senza richiedere il riavvio completo del dispositivo, superando i limiti standard del sistema Android.

---

## 🆚 Perché questo approccio? (Related Work)
Molte app usano l'accelerometro per "indovinare" il parcheggio. Abbiamo scelto il **salvataggio manuale potenziato** perché:
1. **Affidabilità:** Non fallisce nei parcheggi interrati o zone urbane dense.
2. **Efficienza:** Zero monitoraggio passivo dei sensori = durata della batteria raddoppiata.
3. **Trasparenza:** L'utente sa esattamente dove e quando la posizione è stata salvata.

---

## 👥 Contributors
Questo progetto è stato realizzato in collaborazione da:
* **[Antoniopio Giurranna](https://github.com/Tonino03)** - Sviluppo logica e integrazione API.
* **[Francesco D'Angelo](https://github.com/Vuot00)** - Sviluppo UI e gestione database.
