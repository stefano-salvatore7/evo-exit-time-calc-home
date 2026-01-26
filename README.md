# EVO Exit Time Calculator (HOME)

Questo script Tampermonkey/Greasemonkey è progettato per il sistema di gestione delle presenze EVO (usato su `https://personale-unibo.hrgpi.it/`). Calcola automaticamente l'orario di uscita previsto per la giornata corrente direttamente dalla **pagina HOME/Dashboard**, tenendo conto delle timbrature, dell'eventuale pausa e della propria linea oraria.

**(Versione Script: 2.1)**

## Caratteristiche

* **Calcolo Flessibile dell'Orario di Uscita tramite Switch:**
    * **Per 7 ore e 12 minuti (7:12):** Determina l'orario di uscita necessario per completare le 7 ore e 12 minuti di lavoro **nette**, a cui viene aggiunta la pausa.
    * **Per 6 ore e 1 minuto (6:01):** Determina l'orario di uscita necessario per completare le 6 ore e 1 minuto di lavoro **nette**, a cui viene aggiunta la pausa.
    * La modalità di calcolo (7:12 o 6:01) può essere selezionata tramite un **switch toggle compatto** e la tua scelta viene **salvata automaticamente** e ricaricata alla visita successiva della pagina.
* **Gestione Fascia Oraria di Ingresso:**
    * Include un **selettore a discesa** che permette di scegliere la fascia oraria desiderata per l'ingresso (`07:30 - 08:30`, `08:00 - 09:00`, `08:30 - 09:30`).
    * L'orario di ingresso considerato per entrambi i calcoli sarà il **maggiore** tra la prima timbratura di ingresso effettiva e il limite inferiore della fascia oraria selezionata.
    * La preferenza della fascia oraria viene **salvata automaticamente** e ricaricata alla visita successiva della pagina.
* **Compatibilità con la Dashboard HOME:**
    * Lo script funziona esclusivamente sulla **pagina Dashboard/Home** del portale EVO.
    * Legge le timbrature dalla card "Timbrature di giornata" presente in home.
    * Visualizza l'orario di uscita in una **card dedicata** con lo stesso stile delle altre card della pagina.
* **Gestione Timbrature Flessibile:** 
    * Identifica automaticamente le timbrature di entrata e uscita dalla tabella `clockings-table`.
    * Supporta la lettura di timbrature da entrambe le colonne della tabella (4 celle per riga).
* **Gestione Pausa Pranzo Intelligente:** 
    * Calcola automaticamente la durata della pausa pranzo rilevando l'**ultima Uscita seguita dalla prima Entrata**.
    * Se la pausa rilevata è **inferiore a 10 minuti**, usa 10 minuti come minimo.
    * Se la pausa rilevata è **superiore a 3 ore** (180 minuti), la considera non valida e usa 10 minuti predefiniti.
    * Se non viene rilevata alcuna pausa Uscita-Entrata, aggiunge automaticamente **10 minuti predefiniti**.
* **Visualizzazione Orario di Uscita:** 
    * L'orario di uscita calcolato viene visualizzato in una **box dedicata e compatta** con etichetta `"Uscita: HH:mm"`.
    * La box ha uno sfondo grigio chiaro e include un tooltip con tutti i dettagli del calcolo (fascia, entrata, minuti lavorativi, pausa).
* **Design Integrato:** 
    * L'interfaccia dello script è completamente integrata con il design della pagina EVO.
    * Card con sfondo bianco, shadow sottile e stile identico alle altre card della dashboard.
    * Titolo "Ora del Giorno" coerente con lo stile degli altri elementi della pagina.
* **Posizionamento Intuitivo:** 
    * La card viene posizionata **sopra** la card "Timbrature di giornata".
    * Il selettore della fascia oraria, lo switch per la modalità di calcolo e la box dell'orario di uscita sono organizzati in modo chiaro e compatto.
* **Apparizione Condizionale:** 
    * Gli elementi UI dello script appaiono **esclusivamente sulla pagina Dashboard/Home** del portale, dove è presente la card "Timbrature di giornata".
* **Miglioramento Estetico:** 
    * Il font **"Open Sans"** è applicato in modo uniforme a tutti gli elementi UI generati dallo script per una migliore estetica e coerenza visiva.

## Installazione e Aggiornamenti Automatici

Per installare lo script e assicurarti che si aggiorni automaticamente dal repository GitHub, segui i passaggi per il tuo browser:

### 1. Installare l'estensione Tampermonkey

Se non l'hai già fatto, installa l'estensione Tampermonkey nel tuo browser:

* **[Tampermonkey per Chrome](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)**
* **[Tampermonkey per Edge](https://microsoftedge.microsoft.com/addons/detail/tampermonkey/iikmkjmpbldmmepgdkmfapfmccmocdkf)**
* **[Tampermonkey per Firefox](https://addons.mozilla.org/it/firefox/addon/tampermonkey/)** (o Greasemonkey se preferisci)

### 2. **DISABILITA/ELIMINA EVENTUALE VECCHIO SCRIPT (IMPORTANTE!)**

Prima di installare questa versione 2.0, è **FONDAMENTALE** che tu disabiliti o elimini qualsiasi versione precedente di "EVO Exit Time Calculator (HOME)" (incluse le versioni 1.x) che potrebbero essere ancora presenti nella tua dashboard di Tampermonkey. Lasciarli attivi potrebbe causare conflitti.

### 3. Configurazione del Browser (Importante per l'esecuzione)

Per consentire l'esecuzione corretta dello script, potrebbero essere necessari alcuni passaggi di configurazione nel tuo browser:

#### Per Google Chrome:

1.  Apri Chrome e digita `chrome://extensions/` nella barra degli indirizzi, poi premi Invio.
2.  In alto a destra, attiva la **"Modalità sviluppatore"** (interruttore).
3.  Individua Tampermonkey nell'elenco delle estensioni.
4.  Clicca su **"Dettagli"** sotto Tampermonkey.
5.  Assicurati che l'opzione **"Consenti script utente"** sia attiva.
6.  Assicurati che l'opzione **"Consenti l'accesso agli URL del file"** sia attiva.

#### Per Microsoft Edge:

1.  Apri Edge e digita `edge://extensions/` nella barra degli indirizzi, poi premi Invio.
2.  In alto a destra, attiva la **"Modalità sviluppatore"** (interruttore). Potrebbe comparire un avviso di sicurezza nella parte superiore del browser; è normale quando si usa questa modalità.
3.  Individua Tampermonkey nell'elenco delle estensioni.
4.  Clicca su **"Dettagli"** sotto Tampermonkey.
5.  Assicurati che l'opzione **"Consenti estensioni da altri archivi"** sia attiva.
6.  **Assicurati che l'opzione "Consenti l'accesso agli URL del file" sia attiva.**

### 4. Installazione dello Script per Aggiornamenti Automatici

Ora che il tuo browser è configurato e i vecchi script sono stati disabilitati, puoi installare lo script:

[**Clicca qui per installare/aggiornare EVO Exit Time Calculator (HOME)**](https://github.com/stefano-salvatore7/evo-exit-time-calc-home/raw/refs/heads/main/evo-exit-time-calculator-home.user.js)

* Dopo aver cliccato, Tampermonkey (o Greasemonkey) ti mostrerà il codice dello script e ti chiederà di **"Installa"** (se è la prima volta) o **"Aggiorna"** (se stai aggiornando una versione precedente). Conferma l'azione.

### 5. Verifica Aggiornamenti Automatici (Tampermonkey)

Una volta installato tramite il link RAW, Tampermonkey dovrebbe gestire automaticamente gli aggiornamenti. Puoi verificare le impostazioni:

* Clicca sull'icona di Tampermonkey nel tuo browser e seleziona **"Dashboard"**.
* Trova "EVO Exit Time Calculator (HOME)" nell'elenco.
* Verifica che la casella "Controlla aggiornamenti" sia spuntata. L'URL di aggiornamento dovrebbe essere corretto (quello RAW che hai usato per l'installazione).
* Tampermonkey controllerà periodicamente il repository per nuove versioni e ti notificherà se è disponibile un aggiornamento. Puoi anche forzare un controllo cliccando sull'icona delle frecce circolari (Aggiorna) accanto al nome dello script.

## Utilizzo

Una volta installato, lo script si attiverà automaticamente quando visiterai la pagina Dashboard/Home di EVO su `https://personale-unibo.hrgpi.it/*`.

1.  Naviga alla **pagina Dashboard/Home** (quella con la card "Timbrature di giornata").
2.  Vedrai apparire una nuova card **"Ora del Giorno"** posizionata sopra la card "Timbrature di giornata".
3.  Nella card troverai:
    * Un **selettore a discesa** per la "Linea oraria"
    * Uno **switch toggle** ("7:12" / "6:01") per la modalità di calcolo
    * Una **box con l'orario di uscita** calcolato
4.  **Seleziona la fascia oraria** desiderata dal selettore e la **modalità di calcolo** desiderata (7:12 o 6:01) tramite lo switch.
5.  L'orario di uscita apparirà automaticamente nella box dedicata con formato **"Uscita: HH:mm"**.
6.  Passa il mouse sulla box per vedere il **tooltip** con tutti i dettagli del calcolo.

## Novità Versione 2.0

La versione 2.0 introduce importanti miglioramenti estetici:

* ✅ **Design completamente rinnovato** con stile identico alle card native della dashboard
* ✅ **Card con sfondo bianco** e shadow sottile per integrazione perfetta
* ✅ **Titolo "Ora del Giorno"** coerente con gli altri elementi della pagina
* ✅ **Layout migliorato** con wrapper interno per organizzazione ottimale dei controlli
* ✅ **Gestione pausa intelligente** che rileva automaticamente la pausa Uscita-Entrata
* ✅ **Tooltip informativo** con tutti i dettagli del calcolo

## Contributi

Se desideri contribuire a migliorare questo script, sentiti libero di aprire una "Issue" o proporre una "Pull Request" sul repository GitHub.

## Log delle Versioni

### Versione 2.1 (Gennaio 2026)
* Redesign completo dell'interfaccia con stile card nativo
* Aggiunto titolo "Ora del Giorno" alla card principale
* Migliorato il layout con wrapper interno per i controlli
* Ottimizzata l'integrazione visiva con la dashboard

### Versione 1.0 (Gennaio 2026)
* Release iniziale
* Calcolo orario di uscita con modalità 7:12 e 6:01
* Selettore fascia oraria con salvataggio automatico
* Gestione pausa pranzo automatica
* Visualizzazione orario in box compatta

---

**Nota:** Questo script è specifico per la pagina HOME/Dashboard. Per la pagina "Cartellino" esiste uno script separato con funzionalità dedicate.
