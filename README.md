# Occhio

Bollo, revisione, documenti, abbonamenti: le scadenze, prima che scadano.

Occhio è una web app installabile (PWA) per tenere sotto controllo le scadenze ricorrenti di tutti i giorni. Niente account, niente collegamento alla banca, niente cloud: i dati restano sul tuo dispositivo.

## Funzioni

- **"Occhio, oggi ti tocca"**: all'apertura, un riquadro con le scadenze entro il preavviso o già superate
- **Aggiungi auto**: dalle date del libretto calcola revisione (4 anni, poi ogni 2), bollo e assicurazione
- **Leggi una lettera**: fotografi una lettera di Comune, Agenzia delle Entrate, INPS…; Claude la spiega in parole semplici e propone le scadenze da aggiungere (serve una chiave API Anthropic tua, vedi sotto)
- Conto alla rovescia per ogni scadenza, divise in: scadute, entro 7 giorni, entro 30 giorni, più avanti
- Modelli rapidi: bollo, revisione, assicurazione, carta d'identità, passaporto, patente, abbonamenti, caldaia, TARI…
- "Fatto, rinnova": porta la scadenza al giro successivo (mensile, annuale, ogni 2/5/10 anni…)
- Riepilogo: scadenze superate, spese dei prossimi 30 giorni, spese ricorrenti annue
- Simulatore abbonamenti: quanto risparmi disdicendo quelli che non usi
- Esportazione in calendario (`.ics`) con promemoria, per avere le notifiche sul telefono
- Backup e ripristino dei dati in JSON
- Funziona offline e si installa sulla schermata home
- Tema chiaro e scuro automatico

## Usarla

È un sito statico, non serve nessuna build. Pubblicata con GitHub Pages, si apre dal browser del telefono e si aggiunge alla schermata home:

- **iPhone (Safari):** Condividi → Aggiungi alla schermata Home
- **Android (Chrome):** menu ⋮ → Installa app

In locale:

```bash
python3 -m http.server 8000
```

poi apri <http://localhost:8000>.

## File

| File | Cosa fa |
| --- | --- |
| `index.html` | L'app completa (HTML, CSS e JavaScript) |
| `manifest.webmanifest` | Nome, colori e icona per l'installazione |
| `sw.js` | Service worker per il funzionamento offline |
| `icon.svg` | Icona |

## Leggi una lettera (AI)

La funzione usa l'API di Anthropic direttamente dal browser, senza un server intermedio:

- serve una chiave API personale, da creare su <https://console.anthropic.com/settings/keys>;
- la chiave viene salvata solo nel `localStorage` del dispositivo e si può rimuovere dall'app;
- ogni lettera costa pochi centesimi, addebitati sull'account Anthropic. Conviene impostare un limite di spesa nella Console;
- la foto o il PDF della lettera vengono inviati ad Anthropic per l'analisi;
- le date proposte vanno sempre controllate sulla lettera prima di aggiungerle.

## Privacy

I dati sono salvati nel `localStorage` del browser e non vengono inviati da nessuna parte. Fa eccezione la funzione "Leggi una lettera", che invia ad Anthropic solo il documento che scegli tu. Se cancelli i dati del browser li perdi: usa "Copia backup" ogni tanto.
