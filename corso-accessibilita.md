# Corso di Accessibilità Web

## Dispensa per Editor e Sviluppatori

---

## Capitolo 1: Introduzione Teorica

### Fondamenti legali e obiettivi dell'accessibilità

### 1.1 Quadro Normativo

L'Italia adotta un sistema normativo gerarchico per l'accessibilità digitale, allineato alle direttive europee. I tre pilastri principali sono:

**1. Legge Stanca (Legge 4/2004)**
- Prima normativa italiana sull'accessibilità digitale
- Ambito: Siti web, applicazioni e documenti digitali della Pubblica Amministrazione
- Testo ufficiale: https://www.gazzettaufficiale.it/eli/id/2004/01/17/004G0005/sg

**2. Direttiva UE 2016/2102**
- Estende gli obblighi a tutti i siti e app mobile della PA in Europa
- Recepimento in Italia: D.Lgs. 106/2018
- Testo UE: https://eur-lex.europa.eu/legal-content/IT/TXT/?uri=CELEX:32016L2102

**3. Linee Guida AgID**
- Standard tecnico per l'Italia, basato su WCAG 2.1 (livello AA)
- Versione attuale (2023): https://docs.italia.it/agid/documenti-in-consultazione/lg-accessibilita-docs/it/stabile/

#### Fonti Aggiuntive

**European Accessibility Act (EAA – Direttiva UE 2019/882)**
- Dal 2025 rende obbligatoria l'accessibilità anche per prodotti e servizi privati (es. e-commerce, bancomat)
- Testo UE: https://eur-lex.europa.eu/legal-content/IT/TXT/?uri=CELEX:32019L0882

**Decreto "Siti Web PA" (D.Lgs. 179/2016)**
- Normativa su usabilità e qualità dei siti pubblici, collegata all'accessibilità
- Testo ufficiale: https://www.gazzettaufficiale.it/eli/id/2016/09/16/16G00198/sg

### 1.2 Standard Obbligatori

**WCAG 2.2 Livello AA (aggiornamento 2024)**
- Standard obbligatorio per la PA italiana, come definito dalle Linee Guida AgID v2.2
- Novità vs 2.1: Maggiore attenzione a disabilità cognitive, mobile e drag-and-drop
- Testo ufficiale W3C: https://www.w3.org/TR/WCAG22/

**Principi POUR**
- **P**ercepibile, **U**tilizzabile, **C**omprensibile, **R**obusto
- Guida W3C ai principi: https://www.w3.org/WAI/fundamentals/accessibility-principles/

**Inclusione Universale**
- Convenzione ONU sui diritti delle persone con disabilità: https://www.un.org/development/desa/disabilities/convention-on-the-rights-of-persons-with-disabilities.html
- Dati ISTAT 2023: 3,1 milioni di persone con disabilità in Italia (https://www.istat.it/it/archivio/278703)

### 1.3 Sintesi degli Obblighi per le Amministrazioni

**1. Valutazione Tecnica (Audit Obbligatorio)**
- **Cosa**: Verifica di conformità ai WCAG 2.2 Livello AA tramite:
  - Autovalutazione (per siti semplici)
  - Audit esterno (per piattaforme complesse, es. portali con oltre 50 pagine)
- **Frequenza**: Ogni 2 anni (o dopo modifiche sostanziali)
- **Fonte**: Art. 9, D.Lgs. 106/2018 (scadenze) · Linee Guida AgID, Allegato 2 (metodologia)

**2. Dichiarazione di Accessibilità**
- **Cosa**: Documento pubblico che attesta:
  - Lo stato di conformità (es. "Parzialmente conforme" se ci sono eccezioni)
  - I contatti per segnalazioni
  - I contenuti non accessibili (con motivazione e piano di risoluzione)
- **Scadenza**: 23 settembre di ogni anno (termine per aggiornamento)
- Modello ufficiale AgID: https://form.agid.gov.it/view/d7b8a8a0-1b2d-4f1a-9b5a-7c9d1e2f3a4b
- **Fonte**: Art. 8, D.Lgs. 106/2018

**3. Meccanismo di Feedback**
- **Cosa**: Canale dedicato per segnalare barriere digitali (es. form online, email, telefono)
- **Requisiti**:
  - Risposta entro 20 giorni (7 giorni per segnalazioni urgenti, es. servizi sanitari)
  - Procedura di escalation: Se la PA non risponde, l'utente può rivolgersi al Difensore Civico per il Digitale (https://www.defensorecivico-digitale.it)
- **Fonte**: Art. 7, D.Lgs. 106/2018

---

## Capitolo 2: Markup e Semantica

### Dare significato alla struttura del documento

### 2.1 Gerarchia dei Titoli

La struttura semantica è fondamentale per chi utilizza Screen Reader. I titoli devono seguire un ordine logico e nidificato:

- `<h1>`: Titolo dell'Articolo (unico per pagina)
- `<h2>`: Macro-sezioni (es. Metodologia, Risultati)
- `<h3>`: Sotto-sezioni (es. Campionamento, Analisi Dati)

```html
<!-- ✅ Corretto: struttura logica -->
<h1>Analisi del comportamento migratorio degli uccelli</h1>
  <h2>Metodologia</h2>
    <h3>Campionamento</h3>
    <h3>Strumenti di rilevazione</h3>
  <h2>Risultati</h2>
    <h3>Dati quantitativi</h3>
    <h3>Osservazioni qualitative</h3>

<!-- ❌ Errato: salto di livello -->
<h1>Titolo articolo</h1>
  <h4>Sottosezione</h4>  <!-- Salta h2 e h3! -->
```

> **Nota bene**: Non saltare mai i livelli (non passare da un H2 a un H4) solo per motivi estetici.

### 2.2 Enfasi semantica: `<strong>` e `<em>`

```html
<!-- ✅ Semantico: trasmette significato -->
<p>È <strong>obbligatorio</strong> compilare tutti i campi.</p>
<p>Il termine <em>accessibilità</em> deriva dal latino.</p>

<!-- ❌ Presentazionale: solo aspetto visivo -->
<p>È <b>obbligatorio</b> compilare tutti i campi.</p>
<p>Il termine <i>accessibilità</i> deriva dal latino.</p>
```

**Perché preferire `<strong>` e `<em>`?**
- Gli screen reader cambiano tono/enfasi vocale
- `<b>` e `<i>` sono solo stilistici, non comunicano importanza
- Migliore SEO: i motori di ricerca pesano il contenuto in `<strong>`

### 2.3 Liste semantiche

Usare i tag appropriati per gli elenchi, mai simularli con trattini o numeri manuali.

```html
<!-- ✅ Lista non ordinata (punti elenco) -->
<ul>
  <li>Primo elemento</li>
  <li>Secondo elemento</li>
</ul>

<!-- ✅ Lista ordinata (sequenza numerata) -->
<ol>
  <li>Prima fase del processo</li>
  <li>Seconda fase del processo</li>
</ol>

<!-- ✅ Lista di definizioni (glossario, FAQ) -->
<dl>
  <dt>Accessibilità</dt>
  <dd>Caratteristica di un sistema che lo rende fruibile da tutti gli utenti.</dd>
  <dt>WCAG</dt>
  <dd>Web Content Accessibility Guidelines, standard internazionale.</dd>
</dl>

<!-- ❌ Errato: lista finta con trattini -->
<p>
  - Primo elemento<br>
  - Secondo elemento<br>
</p>
```

**Perché usare le liste semantiche?**
- Gli screen reader annunciano "lista di 5 elementi" e permettono di navigare tra gli item
- Con i trattini manuali, l'utente sente solo "trattino primo elemento trattino secondo elemento..." senza contesto

### 2.4 Citazioni

Distinguere tra citazioni in blocco e citazioni inline.

```html
<!-- ✅ Citazione in blocco (paragrafo citato) -->
<blockquote cite="https://www.w3.org/WAI/">
  <p>Il potere del Web sta nella sua universalità. 
  L'accesso da parte di tutti, indipendentemente dalla disabilità, 
  è un aspetto essenziale.</p>
  <footer>— Tim Berners-Lee</footer>
</blockquote>

<!-- ✅ Citazione inline (breve, nel testo) -->
<p>Come disse Tim Berners-Lee, <q>il potere del Web sta nella sua universalità</q>.</p>

<!-- ✅ Riferimento a un'opera -->
<p>Il concetto è approfondito nel documento <cite>WCAG 2.2</cite>.</p>

<!-- ❌ Errato: citazione con virgolette e corsivo manuale -->
<p><i>"Il potere del Web sta nella sua universalità"</i></p>
```

**Differenze:**
- `<blockquote>`: citazioni lunghe, in blocco separato
- `<q>`: citazioni brevi inline (il browser aggiunge le virgolette automaticamente)
- `<cite>`: titolo di un'opera (libro, documento, articolo)

---

## Capitolo 3: CSS e Layout

### Gestione estetica accessibile del tema

### 3.1 Specificità dei CSS

Nella personalizzazione dei temi, è importante capire come i browser applicano gli stili. Quando più regole si applicano allo stesso elemento, vince quella con specificità maggiore.

| Selettore | Peso | Note |
|-----------|------|------|
| `!important` | Massimo assoluto | Ultima risorsa, sovrascrive tutto |
| Stili Inline | Molto alto | Evitare se possibile |
| ID (`#`) | Alto | Un solo elemento per pagina |
| Classi (`.`) | Medio | Metodo consigliato |
| Tag | Minimo | Stili di base |

> **Nota**: `!important` va usato solo come ultima risorsa quando non si riesce a sovrascrivere uno stile per via gerarchica. L'abuso di `!important` rende il CSS difficile da mantenere.

```html
<!-- HTML di partenza -->
<body>
  <div class="content">
    <p class="intro" id="hero-text" style="color: red;">
      Questo è il testo di esempio.
    </p>
  </div>
</body>
```

```css
/* Esempio progressivo sullo stesso elemento */

/* 1. Selettore tag - specificità minima (0,0,1) */
p {
  color: black;
}

/* 2. Selettore classe - sovrascrive il tag (0,1,0) */
.intro {
  color: blue;      /* Vince su p */
}

/* 3. Selettore ID - sovrascrive la classe (1,0,0) */
#hero-text {
  color: green;     /* Vince su .intro */
}

/* 4. Lo style="color: red" nell'HTML sovrascrive l'ID */
/* Il testo sarà rosso */

/* 5. !important - sovrascrive tutto, anche l'inline */
.intro {
  color: purple !important;   /* Vince su tutto */
}
```

**Risultato della cascata:**
1. `p` → testo nero
2. `.intro` → testo blu (sovrascrive tag)
3. `#hero-text` → testo verde (sovrascrive classe)
4. `style="color: red"` → testo rosso (sovrascrive ID)
5. `!important` → testo viola (sovrascrive inline)

**Consiglio pratico**: Prima di usare `!important`, provare ad aumentare la specificità combinando selettori:

```css
/* Invece di !important, aumentare specificità */
body .content .intro {
  color: blue;      /* Specificità (0,3,1) - più alta di .intro */
}
```

### 3.2 Selettori e Contesto

Spesso lo stesso elemento (es. un titolo) appare in contesti diversi con la stessa classe. Come applicare uno stile solo in un contesto specifico?

```html
<!-- Contesto 1: Elenco articoli nel sommario del fascicolo -->
<div class="obj_article_summary">
  <h3 class="title">
    <a href="...">Editorial</a>
  </h3>
  ...
</div>

<!-- Contesto 2: Dettaglio singolo articolo -->
<article class="obj_article_details">
  <h1 class="title">
    Editorial
  </h1>
  ...
</article>
```

**Problema**: Se scrivo `.title { color: red; }` cambio il colore in entrambi i contesti.

**Soluzione**: Usare il selettore contestuale, specificando l'elemento padre.

```css
/* ❌ Troppo generico: colpisce TUTTI i .title */
.title {
  color: red;
}

/* ✅ Solo il titolo nel dettaglio articolo */
article.obj_article_details .title {
  color: red;
}

/* ✅ Solo il titolo nell'elenco sommario */
.obj_article_summary .title {
  color: blue;
}
```

**Vantaggi del selettore contestuale:**
- Specificità maggiore senza usare `!important`
- Stili isolati per contesto, nessun conflitto
- Codice più leggibile e manutenibile

### 3.3 Colori e Contrasti

Il contrasto tra testo e sfondo deve essere netto per permettere la lettura a ipovedenti o in condizioni di forte luce solare.

**Rapporti di contrasto minimi richiesti (WCAG 2.2):**

| Tipo di testo | Rapporto minimo |
|---------------|-----------------|
| Testo normale | 4.5:1 |
| Testo grande (≥18pt o ≥14pt bold) | 3:1 |
| Elementi UI e grafici | 3:1 |

**Evitare sfondi immagine sotto il testo**: Il testo sovrapposto a immagini di sfondo è quasi sempre problematico per il contrasto. Se possibile, usare sfondi a tinta unita.

#### Tool per verificare il contrasto

**WebAIM Contrast Checker**
- Inserisci i codici colore esadecimali e verifica il rapporto
- https://webaim.org/resources/contrastchecker/

**Colour Contrast Analyser (CCA)**
- Applicazione desktop con contagocce per prelevare i colori direttamente dallo schermo
- https://www.tpgi.com/color-contrast-checker/

**Firefox Developer Tools**
- Integrato nel browser: Ispeziona elemento → tab "Accessibilità" → mostra il rapporto di contrasto
- Segnala automaticamente i problemi di contrasto

### 3.4 Tipografia e Spazi

La leggibilità dipende da scelte tipografiche oculate:

- **Utilizzare unità di misura relative (`rem` o `em`)**: I pixel sono unità fisse e ignorano le preferenze dell'utente. Se un utente ingrandisce la dimensione del testo nelle impostazioni del browser, i valori in `px` rimangono invariati. Le unità relative invece si adattano.
  - `rem` = relativo al font-size del root (`<html>`), solitamente 16px
  - `em` = relativo al font-size dell'elemento padre

```css
/* ❌ Pixel: ignora le preferenze utente */
body {
  font-size: 16px;
}
h1 {
  font-size: 32px;
  margin-bottom: 24px;
}

/* ✅ Rem: si adatta alle impostazioni del browser */
body {
  font-size: 1rem;      /* = 16px di default, ma scala con le preferenze */
}
h1 {
  font-size: 2rem;      /* = 32px di default, scala proporzionalmente */
  margin-bottom: 1.5rem; /* = 24px di default */
}
```

  **Conversione rapida** (base 16px): 12px = 0.75rem · 14px = 0.875rem · 16px = 1rem · 18px = 1.125rem · 24px = 1.5rem · 32px = 2rem

- **Impostare un'altezza interlinea (`line-height`) di almeno 1.5 o 1.6** per facilitare la lettura

- **Evitare il testo giustificato**, che crea spazi irregolari difficoltosi per utenti dislessici

```css
/* ✅ Testo leggibile */
p {
  line-height: 1.6;
  text-align: left;   /* Mai justify */
}
```

---

## Capitolo 4: Contenuti e Asset

### Immagini, Link e File

### 4.1 Gestione Immagini

Ogni immagine deve avere un attributo `alt` (testo alternativo) che descriva il contenuto. Se l'immagine è puramente decorativa, l'attributo va lasciato vuoto (`alt=""`).

```html
<!-- ✅ Immagine informativa: descrivere il contenuto -->
<img src="grafico-vendite-2024.png" 
     alt="Grafico a barre delle vendite 2024: Q1 120k, Q2 145k, Q3 132k, Q4 168k">

<!-- ✅ Foto con soggetto rilevante -->
<img src="team-ricerca.jpg" 
     alt="Il team di ricerca del Dipartimento di Fisica durante la conferenza di Berlino">

<!-- ✅ Immagine decorativa: alt vuoto (non assente!) -->
<img src="decorazione-floreale.png" alt="">

<!-- ❌ Errato: alt assente (lo screen reader legge il nome file) -->
<img src="IMG_20240601_143052.jpg">

<!-- ❌ Errato: alt inutile -->
<img src="grafico.png" alt="immagine">
<img src="foto.jpg" alt="foto">
```

**Regole per un buon testo alternativo:**
- Descrivere il *contenuto* e lo *scopo* dell'immagine, non l'aspetto
- Essere concisi ma completi (idealmente sotto i 125 caratteri)
- Non iniziare con "Immagine di..." (lo screen reader già annuncia che è un'immagine)
- Per grafici e tabelle, descrivere i dati chiave o fornire una tabella accessibile

**Ottimizzazione delle immagini:**
- Usare risoluzioni adatte al web (72-96 DPI), non risoluzioni da stampa (300 DPI)
- Comprimere le immagini per ridurre il peso (idealmente sotto i 200KB)
- Evitare di caricare foto direttamente dalla fotocamera senza ottimizzazione

<!-- TODO: Aggiungere screenshot del backend per mostrare dove inserire il testo alternativo -->

### 4.2 Gestione Link

Il testo dei collegamenti deve essere auto-esplicativo: l'utente deve capire la destinazione senza leggere il contesto circostante.

| ❌ Evitare | ✅ Preferire |
|-----------|-------------|
| "clicca qui" | "Scarica il PDF della ricerca" |
| "leggi tutto" | "Consulta la bibliografia completa" |
| "maggiori informazioni" | "Informazioni sul bando 2025" |

```html
<!-- ✅ Link auto-esplicativo -->
<a href="report-2024.pdf">Scarica il report annuale 2024 (PDF, 2.3MB)</a>

<!-- ✅ Con indicazione del formato e peso -->
<a href="linee-guida.pdf">Linee guida per gli autori (PDF, 450KB)</a>

<!-- ❌ Errato: non descrive la destinazione -->
<p>Per scaricare il report <a href="report-2024.pdf">clicca qui</a></p>
```

**Attributo `title`**: È opzionale e sconsigliato come unica fonte di informazione. Non viene letto di default da molti screen reader e non è accessibile su dispositivi touch (non c'è hover). Se usato, deve essere *supplementare*, mai sostitutivo del testo del link.

**Apertura in nuova scheda (`target="_blank"`)**: Usare con cautela. Aprire link in nuova scheda senza avvisare l'utente è un problema di accessibilità (disorientante per utenti screen reader). Best practice:
- Preferire l'apertura nella stessa scheda (l'utente può sempre scegliere di aprire in nuova scheda con tasto destro)
- Se necessario usare `target="_blank"`, avvisare esplicitamente nel testo e aggiungere `rel="noopener"` per sicurezza

```html
<!-- ✅ Se proprio serve nuova scheda: avvisare e proteggere -->
<a href="https://example.com" target="_blank" rel="noopener">
  Sito esterno Example (si apre in una nuova scheda)
</a>
```

### 4.3 Gestione File

I file caricati (PDF, documenti, allegati) devono essere ottimizzati per il web.

**PDF ottimizzati:**
- Usare l'opzione "Salva per Web" o "Ottimizza PDF" del proprio editor
- Evitare PDF con risoluzione da stampa (300 DPI): usare 72-150 DPI per il web
- Comprimere le immagini all'interno del PDF
- Peso consigliato: sotto i 5MB per documenti standard, sotto i 10MB per pubblicazioni complesse

**Indicare sempre peso e formato:**
- Nel testo del link, specificare formato e dimensione: "Scarica il bando (PDF, 1.2MB)"
- Permette all'utente di decidere se scaricare (utile per connessioni lente o dati mobili)

**Accessibilità dei PDF:**
- I PDF devono essere "tagged" (strutturati) per essere leggibili dagli screen reader
- Evitare PDF da scansione (immagini di testo): se necessario, applicare OCR

---

## Capitolo 5: User Experience

### Semplicità e chiarezza dei contenuti

### 5.1 UX e Semplicità Espositiva

L'accessibilità non riguarda solo il codice, ma anche come scriviamo. Una buona UX riduce il carico cognitivo:

**Esempio Negativo**: Muri di testo compatti, paragrafi infiniti e linguaggio inutilmente burocratico.

**Esempio Positivo**: Frasi brevi, paragrafi ben distanziati, uso di liste puntate e grassetti per evidenziare i concetti chiave.

> **Il consiglio dell'esperto**: Applica la tecnica della "Piramide Rovesciata", inserendo le conclusioni o le informazioni più importanti all'inizio di ogni capitolo.

---

## Capitolo 6: Tool di Controllo

### Verificare il lavoro svolto

### 6.1 Strumenti di Audit

Per verificare l'accessibilità si possono usare:

**Lighthouse (integrato in Chrome)**

Strumento gratuito integrato in Google Chrome per un'analisi tecnica veloce.

Come usarlo:
1. Aprire la pagina da analizzare in Chrome
2. Tasto destro → "Ispeziona" (oppure F12)
3. Tab "Lighthouse" nella barra degli strumenti sviluppatore
4. Selezionare "Accessibility" tra le categorie
5. Cliccare "Analyze page load"

Il report mostra un punteggio da 0 a 100 e un elenco di problemi con suggerimenti per risolverli.

<!-- TODO: Aggiungere screenshot -->

**Mauve++ (validatore AgID)**

Validatore specifico per le linee guida italiane, sviluppato dal CNR. Produce report formali utilizzabili per la dichiarazione di accessibilità.

- Link: https://mauve.isti.cnr.it/

Come usarlo:
1. Accedere al sito e inserire l'URL da verificare
2. Avviare la scansione
3. Consultare il report che elenca le violazioni per criterio WCAG
4. Esportare il report in formato PDF o CSV per documentazione

<!-- TODO: Aggiungere screenshot -->

---

## Capitolo 7: Fonti e Riferimenti

### Approfondimenti e manuali ufficiali

**Standard internazionali**
- W3C WCAG 2.2: https://www.w3.org/TR/WCAG22/
- W3C WAI (Web Accessibility Initiative): https://www.w3.org/WAI/
- Principi POUR: https://www.w3.org/WAI/fundamentals/accessibility-principles/

**Normativa italiana**
- AgID - Linee Guida Accessibilità: https://docs.italia.it/agid/documenti-in-consultazione/lg-accessibilita-docs/it/stabile/
- Dichiarazione di Accessibilità (form AgID): https://form.agid.gov.it/
- Difensore Civico per il Digitale: https://www.defensorecivico-digitale.it

**Documentazione tecnica**
- MDN Web Docs (HTML semantico e CSS): https://developer.mozilla.org/
- Guida CSS di base per neofiti (HTML.it): https://www.html.it/guide/guida-css-di-base/
- PKP Documentation (accessibilità OJS/OMP): https://docs.pkp.sfu.ca/

**Tool di verifica**
- Mauve++ (CNR): https://mauve.isti.cnr.it/
- WebAIM Contrast Checker: https://webaim.org/resources/contrastchecker/
- Colour Contrast Analyser: https://www.tpgi.com/color-contrast-checker/

---

## Note di Lavoro

*Sezione per appunti e modifiche da integrare*

- [ ] Aggiungere esempi pratici con screenshot
- [ ] Integrare sezione su ARIA roles
- [ ] Valutare se aggiungere capitolo su PDF accessibili
