# Bussola Politica Lampo — scheda per Effect House

Versione ridotta della Bussola Politica Italiana da ricostruire come effetto TikTok con **Effect House**.
La stessa logica è già funzionante nella pagina `tiktok.html`: usala come riferimento visivo.

## Flusso dell'effetto

1. Schermata iniziale: "Che partito sei? 12 domande, sì o no." → tocco per iniziare.
2. Per ogni domanda: testo sopra la testa, due pulsanti **NO** (sinistra) e **SÌ** (destra).
   In alternativa al tocco: inclinare la testa a sinistra = NO, a destra = SÌ (Head Tilt).
3. Dopo la dodicesima risposta: nome del partito più vicino, grande, nel colore del partito.

## Le 12 domande

Ogni risposta aggiunge un valore a uno dei tre contatori **X**, **Y**, **Z** (partono da 0).

| # | Domanda | Contatore | SÌ | NO |
|---|---|---|---|---|
| 1 | Le pensioni vanno calcolate sui contributi versati? | X | +1 | −1 |
| 2 | Il Superbonus è stato uno spreco di soldi pubblici? | X | +1 | −1 |
| 3 | Più soldi pubblici alla sanità? | X | −1 | +1 |
| 4 | Lo Stato deve salvare le grandi aziende in crisi, come l'ex Ilva? | X | −1 | +1 |
| 5 | Ci vuole una difesa comune europea? | Y | +1 | −1 |
| 6 | Basta inviare armi all'Ucraina? | Y | −1 | +1 |
| 7 | Ridurre anche l'immigrazione regolare? | Y | −1 | +1 |
| 8 | L'Italia deve riconoscere lo Stato di Palestina? | Y | +1 | −1 |
| 9 | I partiti al governo da 20 anni sanno fare le riforme? | Z | −1 | +1 |
| 10 | Ogni processo deve avere una durata massima fissata per legge? | Z | +1 | −1 |
| 11 | Stessa scuola per tutti fino a 16 anni? | Z | +1 | −1 |
| 12 | L'ISEE basta per decidere chi riceve aiuti pubblici? | Z | −1 | +1 |

Alla fine X, Y e Z valgono ciascuno −4, −2, 0, 2 o 4 (125 combinazioni).

- X: Stato (−) ↔ Mercato (+)
- Y: Sovranismo (−) ↔ Europeismo (+)
- Z: Vecchia politica (−) ↔ Discontinuità (+)

## Tabella dei risultati

Cerca la riga con i valori finali di X, Y e Z e mostra il partito indicato.
È calcolata con le stesse coordinate dei partiti e la stessa distanza usate nel sito.

| X | Y | Z | Partito più vicino | Affinità |
|---|---|---|---|---|
| -4 | -4 | -4 | Movimento 5 Stelle | 68% |
| -4 | -4 | -2 | Movimento 5 Stelle | 73% |
| -4 | -4 | 0 | Movimento 5 Stelle | 74% |
| -4 | -4 | 2 | Futuro Nazionale | 65% |
| -4 | -4 | 4 | Futuro Nazionale | 61% |
| -4 | -2 | -4 | Movimento 5 Stelle | 73% |
| -4 | -2 | -2 | Movimento 5 Stelle | 78% |
| -4 | -2 | 0 | Movimento 5 Stelle | 79% |
| -4 | -2 | 2 | Movimento 5 Stelle | 65% |
| -4 | -2 | 4 | Futuro Nazionale | 60% |
| -4 | 0 | -4 | Alleanza Verdi e Sinistra | 80% |
| -4 | 0 | -2 | Alleanza Verdi e Sinistra | 86% |
| -4 | 0 | 0 | Alleanza Verdi e Sinistra | 85% |
| -4 | 0 | 2 | Alleanza Verdi e Sinistra | 66% |
| -4 | 0 | 4 | Movimento 5 Stelle | 59% |
| -4 | 2 | -4 | Alleanza Verdi e Sinistra | 77% |
| -4 | 2 | -2 | Alleanza Verdi e Sinistra | 83% |
| -4 | 2 | 0 | Alleanza Verdi e Sinistra | 81% |
| -4 | 2 | 2 | Alleanza Verdi e Sinistra | 65% |
| -4 | 2 | 4 | ORA! | 59% |
| -4 | 4 | -4 | Partito Democratico | 74% |
| -4 | 4 | -2 | Partito Democratico | 77% |
| -4 | 4 | 0 | Alleanza Verdi e Sinistra | 74% |
| -4 | 4 | 2 | Alleanza Verdi e Sinistra | 61% |
| -4 | 4 | 4 | ORA! | 59% |
| -2 | -4 | -4 | Lega | 74% |
| -2 | -4 | -2 | Lega | 76% |
| -2 | -4 | 0 | Movimento 5 Stelle | 77% |
| -2 | -4 | 2 | Futuro Nazionale | 72% |
| -2 | -4 | 4 | Futuro Nazionale | 67% |
| -2 | -2 | -4 | Movimento 5 Stelle | 76% |
| -2 | -2 | -2 | Movimento 5 Stelle | 82% |
| -2 | -2 | 0 | Movimento 5 Stelle | 84% |
| -2 | -2 | 2 | Futuro Nazionale | 72% |
| -2 | -2 | 4 | Futuro Nazionale | 67% |
| -2 | 0 | -4 | Alleanza Verdi e Sinistra | 81% |
| -2 | 0 | -2 | Alleanza Verdi e Sinistra | 89% |
| -2 | 0 | 0 | Movimento 5 Stelle | 86% |
| -2 | 0 | 2 | Movimento 5 Stelle | 69% |
| -2 | 0 | 4 | Movimento 5 Stelle | 61% |
| -2 | 2 | -4 | Partito Democratico | 83% |
| -2 | 2 | -2 | Partito Democratico | 87% |
| -2 | 2 | 0 | Alleanza Verdi e Sinistra | 82% |
| -2 | 2 | 2 | ORA! | 68% |
| -2 | 2 | 4 | ORA! | 67% |
| -2 | 4 | -4 | Partito Democratico | 80% |
| -2 | 4 | -2 | Partito Democratico | 83% |
| -2 | 4 | 0 | Partito Democratico | 76% |
| -2 | 4 | 2 | ORA! | 67% |
| -2 | 4 | 4 | ORA! | 67% |
| 0 | -4 | -4 | Lega | 85% |
| 0 | -4 | -2 | Lega | 91% |
| 0 | -4 | 0 | Futuro Nazionale | 93% |
| 0 | -4 | 2 | Futuro Nazionale | 85% |
| 0 | -4 | 4 | Futuro Nazionale | 77% |
| 0 | -2 | -4 | Lega | 88% |
| 0 | -2 | -2 | Lega | 97% |
| 0 | -2 | 0 | Futuro Nazionale | 91% |
| 0 | -2 | 2 | Futuro Nazionale | 84% |
| 0 | -2 | 4 | Futuro Nazionale | 76% |
| 0 | 0 | -4 | Noi Moderati | 87% |
| 0 | 0 | -2 | Noi Moderati | 91% |
| 0 | 0 | 0 | Fratelli d'Italia | 85% |
| 0 | 0 | 2 | ORA! | 74% |
| 0 | 0 | 4 | ORA! | 74% |
| 0 | 2 | -4 | Partito Democratico | 85% |
| 0 | 2 | -2 | Italia Viva | 91% |
| 0 | 2 | 0 | Azione | 87% |
| 0 | 2 | 2 | ORA! | 88% |
| 0 | 2 | 4 | ORA! | 87% |
| 0 | 4 | -4 | Italia Viva | 82% |
| 0 | 4 | -2 | Italia Viva | 87% |
| 0 | 4 | 0 | +Europa | 83% |
| 0 | 4 | 2 | ORA! | 87% |
| 0 | 4 | 4 | ORA! | 86% |
| 2 | -4 | -4 | Lega | 76% |
| 2 | -4 | -2 | Lega | 79% |
| 2 | -4 | 0 | Futuro Nazionale | 81% |
| 2 | -4 | 2 | Futuro Nazionale | 77% |
| 2 | -4 | 4 | Futuro Nazionale | 71% |
| 2 | -2 | -4 | Lega | 78% |
| 2 | -2 | -2 | Lega | 81% |
| 2 | -2 | 0 | Futuro Nazionale | 81% |
| 2 | -2 | 2 | Futuro Nazionale | 76% |
| 2 | -2 | 4 | Futuro Nazionale | 70% |
| 2 | 0 | -4 | Forza Italia | 82% |
| 2 | 0 | -2 | Forza Italia | 84% |
| 2 | 0 | 0 | Partito Liberaldemocratico | 79% |
| 2 | 0 | 2 | ORA! | 75% |
| 2 | 0 | 4 | ORA! | 75% |
| 2 | 2 | -4 | Forza Italia | 86% |
| 2 | 2 | -2 | Forza Italia | 88% |
| 2 | 2 | 0 | Partito Liberaldemocratico | 96% |
| 2 | 2 | 2 | ORA! | 90% |
| 2 | 2 | 4 | ORA! | 89% |
| 2 | 4 | -4 | +Europa | 80% |
| 2 | 4 | -2 | +Europa | 87% |
| 2 | 4 | 0 | Partito Liberaldemocratico | 90% |
| 2 | 4 | 2 | ORA! | 89% |
| 2 | 4 | 4 | ORA! | 88% |
| 4 | -4 | -4 | Lega | 69% |
| 4 | -4 | -2 | Lega | 71% |
| 4 | -4 | 0 | Futuro Nazionale | 73% |
| 4 | -4 | 2 | Futuro Nazionale | 70% |
| 4 | -4 | 4 | Futuro Nazionale | 65% |
| 4 | -2 | -4 | Lega | 70% |
| 4 | -2 | -2 | Lega | 72% |
| 4 | -2 | 0 | Futuro Nazionale | 73% |
| 4 | -2 | 2 | Futuro Nazionale | 70% |
| 4 | -2 | 4 | Futuro Nazionale | 65% |
| 4 | 0 | -4 | Forza Italia | 77% |
| 4 | 0 | -2 | Forza Italia | 78% |
| 4 | 0 | 0 | Partito Liberaldemocratico | 77% |
| 4 | 0 | 2 | ORA! | 71% |
| 4 | 0 | 4 | ORA! | 71% |
| 4 | 2 | -4 | Forza Italia | 79% |
| 4 | 2 | -2 | Forza Italia | 81% |
| 4 | 2 | 0 | Partito Liberaldemocratico | 88% |
| 4 | 2 | 2 | ORA! | 82% |
| 4 | 2 | 4 | ORA! | 82% |
| 4 | 4 | -4 | +Europa | 75% |
| 4 | 4 | -2 | +Europa | 80% |
| 4 | 4 | 0 | Partito Liberaldemocratico | 85% |
| 4 | 4 | 2 | ORA! | 82% |
| 4 | 4 | 4 | ORA! | 81% |

## Colori dei partiti

| Partito | Colore |
|---|---|
| ORA! | #ea580c |
| Partito Liberaldemocratico | #0ea5e9 |
| +Europa | #c026d3 |
| Azione | #3b82f6 |
| Italia Viva | #db2777 |
| Forza Italia | #2563eb |
| Noi Moderati | #0891b2 |
| Partito Democratico | #dc2626 |
| Fratelli d'Italia | #3b5bdb |
| Lega | #16a34a |
| Futuro Nazionale | #a16207 |
| Movimento 5 Stelle | #ca8a04 |
| Alleanza Verdi e Sinistra | #65a30d |

## Come montarlo in Effect House (Visual Scripting)

1. Crea un progetto con **Face Tracking** e un **2D Text** agganciato sopra la testa per la domanda.
2. Aggiungi due **Screen Tap** (o due rilevatori **Head Tilt**) per NO e SÌ.
3. Crea quattro variabili numeriche: `step`, `X`, `Y`, `Z`.
4. A ogni risposta: aggiungi al contatore della domanda corrente il valore della tabella, poi `step + 1` e cambia il testo.
5. Quando `step = 12`: usa una catena di **If** sulle combinazioni di X, Y, Z (o un nodo **Switch**) per scegliere il testo e il colore del partito.

## Nota

Prima della pubblicazione TikTok revisiona ogni effetto. Un effetto che nomina partiti politici può essere respinto:
in quel caso registra la pagina `tiktok.html` con la registrazione schermo del telefono e pubblica il video.
