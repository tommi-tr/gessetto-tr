# Gessetto

Lavagna digitale essenziale per la scuola, in **un solo file HTML**: funziona da chiavetta USB anche senza internet, oppure come sito (Vercel).

## Uso rapido

- **Da chiavetta USB**: copia `index.html` sulla chiavetta e aprilo con il browser della lavagna (o del PC collegato).
- **Online**: apri l'indirizzo Vercel del progetto (vedi sotto).

Tutto si salva da solo nel browser in uso (pagine, impostazioni, lavagne salvate). Per portare le lavagne salvate su un altro computer usa *Lavagne salvate → Esporta* e poi *Importa*.

## Funzioni

| Dove | Pulsanti |
|---|---|
| In basso al centro | mano (sposta; con due dita zoom libero), zoom (cursore a comparsa), penna stilografica, evidenziatore, gomma, gomma del tratto, annulla, ripeti (a coppie, separate da uno spazio) |
| Palmo | con il palmo appoggiato si cancella una fascia larga come il palmo (cerchio di 5 cm di raggio). Si disattiva nelle impostazioni; lì si indica anche la diagonale dello schermo, così i 5 cm sono corretti. Richiede che il browser comunichi la dimensione del contatto |
| In basso a sinistra | inverti lati dei pulsanti, lavagne salvate, salva un'area, forme |
| In basso a destra | pagina precedente, numero pagina, pagina successiva, aggiungi pagina |
| Colonna laterale | colori (bianco, nero, blu, verde, giallo, arancione, rosso, personalizzato da spettro visibile o esadecimale) e spessore a 10 livelli |
| In alto a sinistra | impostazioni, guida, extra (calcolatrice, scientifica, collega telefono) |
| In alto a destra | nascondi pulsanti, schermo intero, orologio |

Forme: rettangolo, quadrato, parallelogramma, ellisse, circonferenza (dal centro), retta (con tratteggi sfumati), retta dei numeri reali, vettore, piano cartesiano (dall'origine verso un angolo, tacche allineate ai quadretti, etichette *x* e *y* cancellabili).

Scorciatoie: Ctrl+Z / Ctrl+Y, Pag↑ / Pag↓, Esc, rotellina per scorrere, Ctrl+rotellina per lo zoom.

## Pubblicare su Vercel

1. Su [vercel.com](https://vercel.com) → *Add New… → Project* → importa `tommi-tr/gessetto-tr`.
2. Framework: **Other**, nessun comando di build, cartella di output: la radice.
3. Pubblica. Se l'indirizzo assegnato **non** è `https://gessetto-tr.vercel.app/`, aggiorna la costante `SITE_URL` all'inizio dello script in `index.html`: è l'indirizzo che il QR code mostra al telefono quando la lavagna gira da chiavetta.

## Collegare il telefono

*Extra → Collega telefono* mostra un QR code. Il telefono apre la pagina del sito e:

- **foto** → compaiono sulla lavagna, da posizionare e ridimensionare;
- **PDF** → ogni pagina diventa una pagina della lavagna (la conversione avviene sul telefono con pdf.js);
- **altri file** → si aprono dalla lista «Ricevuti».

Dalla lavagna si possono inviare al telefono le lavagne salvate, come **immagine PNG** o **PDF**.

Come funziona: i due dispositivi si «presentano» con brevi messaggi su [ntfy.sh](https://ntfy.sh) (serve internet), poi i file viaggiano **direttamente sulla rete locale** con WebRTC. Se la rete della scuola blocca il collegamento diretto (es. isolamento dei client sul wifi), dopo circa 15 secondi i file passano come allegati temporanei di ntfy.sh, su un canale con nome casuale.

## Requisiti tecnici rispettati

- Un unico file, nessuna libreria, font o richiesta di rete per la lavagna (solo il collegamento col telefono usa la rete).
- JavaScript ES5, flexbox con prefissi, niente CSS grid né `gap`; eventi pointer con ripiego touch/mouse.
- Scala in `em` (1em = 1% dell'altezza dello schermo, adattato a 16:9 e 4:3).
- Tratto fluido: `getCoalescedEvents`, curve di Bézier sui punti medi, un solo puntatore alla volta, gomma con `destination-out`.
- Salvataggio in IndexedDB (con ripiego su localStorage, sempre protetto da `try/catch`).

## Versione

1.0.0
