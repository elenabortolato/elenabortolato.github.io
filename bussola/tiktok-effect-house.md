# Bussola Politica Lampo — scheda per Effect House

Versione ridotta della Bussola Politica Italiana da ricostruire come effetto TikTok con **Effect House**.
La stessa logica è già funzionante nella pagina `tiktok.html`: usala come riferimento visivo.

## Flusso dell'effetto

1. Schermata iniziale: "Che partito sei? 8 domande, sì o no." → tocco per iniziare.
2. Per ogni domanda: testo sopra la testa, due pulsanti **NO** (sinistra) e **SÌ** (destra).
   In alternativa al tocco: inclinare la testa a sinistra = NO, a destra = SÌ (Head Tilt).
3. Dopo l'ottava risposta: nome del partito più vicino, grande, nel colore del partito.

## Le 8 domande

Ogni risposta aggiunge un valore a uno dei tre contatori **X**, **Y**, **Z** (partono da 0).

| # | Domanda | Contatore | SÌ | NO |
|---|---|---|---|---|
| 1 | Le pensioni vanno calcolate sui contributi versati? | X | +1 | −1 |
| 2 | Il Superbonus è stato un buon investimento? | X | −1 | +1 |
| 3 | Più soldi pubblici alla sanità? | X | −1 | +1 |
| 4 | Ci vuole una difesa comune europea? | Y | +1 | −1 |
| 5 | Basta inviare armi all'Ucraina? | Y | −1 | +1 |
| 6 | Ridurre anche l'immigrazione regolare? | Y | −1 | +1 |
| 7 | I partiti al governo da 20 anni sanno fare le riforme? | Z | −1 | +1 |
| 8 | Abolire le misure che una valutazione indipendente boccia? | Z | +1 | −1 |

Alla fine: X e Y valgono −3, −1, 1 o 3; Z vale −2, 0 o 2.

- X: Stato (−) ↔ Mercato (+)
- Y: Sovranismo (−) ↔ Europeismo (+)
- Z: Vecchia politica (−) ↔ Discontinuità (+)

## Tabella dei risultati

Cerca la riga con i valori finali di X, Y e Z e mostra il partito indicato.
È calcolata con le stesse coordinate dei partiti e la stessa distanza usate nel sito.

| X | Y | Z | Partito più vicino | Affinità |
|---|---|---|---|---|
| -3 | -3 | -2 | Movimento 5 Stelle | 68% |
| -3 | -3 | 0 | Movimento 5 Stelle | 74% |
| -3 | -3 | 2 | Futuro Nazionale | 61% |
| -3 | -1 | -2 | Movimento 5 Stelle | 74% |
| -3 | -1 | 0 | Movimento 5 Stelle | 81% |
| -3 | -1 | 2 | Futuro Nazionale | 60% |
| -3 | 1 | -2 | Alleanza Verdi e Sinistra | 79% |
| -3 | 1 | 0 | Alleanza Verdi e Sinistra | 83% |
| -3 | 1 | 2 | ORA! | 59% |
| -3 | 3 | -2 | Partito Democratico | 74% |
| -3 | 3 | 0 | Alleanza Verdi e Sinistra | 74% |
| -3 | 3 | 2 | ORA! | 59% |
| -1 | -3 | -2 | Lega | 77% |
| -1 | -3 | 0 | Futuro Nazionale | 79% |
| -1 | -3 | 2 | Futuro Nazionale | 70% |
| -1 | -1 | -2 | Lega | 78% |
| -1 | -1 | 0 | Movimento 5 Stelle | 88% |
| -1 | -1 | 2 | Futuro Nazionale | 68% |
| -1 | 1 | -2 | Partito Democratico | 86% |
| -1 | 1 | 0 | Alleanza Verdi e Sinistra | 84% |
| -1 | 1 | 2 | ORA! | 70% |
| -1 | 3 | -2 | Partito Democratico | 82% |
| -1 | 3 | 0 | Partito Democratico | 78% |
| -1 | 3 | 2 | ORA! | 71% |
| 1 | -3 | -2 | Lega | 79% |
| 1 | -3 | 0 | Futuro Nazionale | 85% |
| 1 | -3 | 2 | Futuro Nazionale | 73% |
| 1 | -1 | -2 | Lega | 81% |
| 1 | -1 | 0 | Futuro Nazionale | 82% |
| 1 | -1 | 2 | Futuro Nazionale | 72% |
| 1 | 1 | -2 | Forza Italia | 89% |
| 1 | 1 | 0 | Partito Liberaldemocratico | 95% |
| 1 | 1 | 2 | ORA! | 90% |
| 1 | 3 | -2 | +Europa | 82% |
| 1 | 3 | 0 | Partito Liberaldemocratico | 91% |
| 1 | 3 | 2 | ORA! | 90% |
| 3 | -3 | -2 | Lega | 69% |
| 3 | -3 | 0 | Futuro Nazionale | 73% |
| 3 | -3 | 2 | Futuro Nazionale | 65% |
| 3 | -1 | -2 | Lega | 70% |
| 3 | -1 | 0 | Futuro Nazionale | 72% |
| 3 | -1 | 2 | Futuro Nazionale | 64% |
| 3 | 1 | -2 | Forza Italia | 80% |
| 3 | 1 | 0 | Partito Liberaldemocratico | 88% |
| 3 | 1 | 2 | ORA! | 81% |
| 3 | 3 | -2 | +Europa | 75% |
| 3 | 3 | 0 | Partito Liberaldemocratico | 85% |
| 3 | 3 | 2 | ORA! | 81% |

## Colori dei partiti

| Partito | Colore |
|---|---|
| ORA! | #ea580c |
| Partito Liberaldemocratico | #0ea5e9 |
| +Europa | #c026d3 |
| Forza Italia | #2563eb |
| Partito Democratico | #dc2626 |
| Lega | #16a34a |
| Futuro Nazionale | #a16207 |
| Movimento 5 Stelle | #ca8a04 |
| Alleanza Verdi e Sinistra | #65a30d |

## Come montarlo in Effect House (Visual Scripting)

1. Crea un progetto con **Face Tracking** e un **2D Text** agganciato sopra la testa per la domanda.
2. Aggiungi due **Screen Tap** (o due rilevatori **Head Tilt**) per NO e SÌ.
3. Crea quattro variabili numeriche: `step`, `X`, `Y`, `Z`.
4. A ogni risposta: aggiungi al contatore della domanda corrente il valore della tabella, poi `step + 1` e cambia il testo.
5. Quando `step = 8`: usa una catena di **If** sulle combinazioni di X, Y, Z (o un nodo **Switch**) per scegliere il testo e il colore del partito.

## Nota

Prima della pubblicazione TikTok revisiona ogni effetto. Un effetto che nomina partiti politici può essere respinto:
in quel caso registra la pagina `tiktok.html` con la registrazione schermo del telefono e pubblica il video.
