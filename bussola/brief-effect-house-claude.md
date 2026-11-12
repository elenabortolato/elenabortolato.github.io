# Brief per Claude: filtro TikTok "Bussola Politica Lampo" in Effect House

## Cosa voglio fare

Voglio costruire in **Effect House** un effetto TikTok a quiz, usando il **Visual Scripting** (non JavaScript).
È la versione ridotta di un test politico web già funzionante (`tiktok.html`): la persona si inquadra con la
fotocamera frontale, compaiono **12 domande sì/no** una alla volta sopra la testa, risponde **toccando la metà
destra dello schermo (SÌ) o la metà sinistra (NO)**, e alla fine compare il **partito politico italiano più vicino**.

Ti chiedo di aiutarmi a completare il grafo: dirmi quali nodi aggiungere e come collegarli, controllare quello che
ho già fatto e, se puoi agire direttamente sul progetto, costruire le parti mancanti seguendo questa specifica.

## Logica in breve

- Tre contatori numerici: **X** (Stato − ↔ Mercato +), **Y** (Sovranismo − ↔ Europeismo +), **Z** (Vecchia politica − ↔ Discontinuità +).
- Ogni risposta vale **risposta = +1 (SÌ) o −1 (NO)** e viene **sommata o sottratta** a uno dei tre contatori, secondo la tabella sotto.
- Dopo 12 risposte X, Y e Z valgono ciascuno −4, −2, 0, 2 o 4 (125 combinazioni).
- Il risultato si sceglie con un **albero di 31 nodi If** (sezione 5), equivalente alla tabella completa delle 125 combinazioni.

## 1. Oggetti nella scena (già creati)

| Oggetto | Tipo | Stato iniziale |
|---|---|---|
| `Domanda` | 2D Text | visibile, testo = domanda 1 |
| `Etichette` | 2D Text (`NO          SÌ`) | visibile |
| `Risultato` | 2D Text | nascosto (ora lo uso temporaneamente per vedere i valori delle variabili) |

## 2. Variabili (Number, valore iniziale 0)

`step` (domanda corrente, 0–11), `X`, `Y`, `Z`, `risposta`.

## 3. Cosa ho già costruito e funziona

```
[Screen Tap] Next ▶ → [If]  Condition = (Position.x > 0.5)
                         True  ▶ → [Set risposta = 1]  ─┐
                         False ▶ → [Set risposta = -1] ─┴─▶ [Sequence] (uscite: Procedure 1, 2, 3)
Procedure 1 ▶ → [If step == 0] True ▶ → [Set X = X + risposta] ▶ → [Set Text Domanda = domanda 2]
Procedure 3 ▶ → [Set step = step + 1]
```

- Per cambiare un testo uso: `Get Scene Object` → `Get Component by Type (Text)` → ingresso **Source** di `Set Text`.
- Il nodo **Sequence** ha uscite chiamate **Procedure 1, 2, 3…**, eseguite in ordine.
- Sto verificando che `step` salga di 1 a ogni tocco, mostrandolo nel testo `Risultato`.

## 4. Cosa manca: i 12 rami

Ogni ramo ha la stessa forma:

```
Procedure N ▶ → [If step == N-1] True ▶ → [Set ASSE = ASSE ± risposta] ▶ → [Set Text Domanda = prossima domanda]
```

Servono **13 uscite** di Sequence (12 rami + l'aumento di `step`, che deve essere **sempre l'ultima**).
Se Sequence non permette di aggiungere uscite, si mettono più Sequence in fila (ultima uscita → nuova Sequence).

| Ramo | step == | Asse | Operazione | Testo da mostrare dopo (prossima domanda) |
|---|---|---|---|---|
| 1 | 0 | X | X = X **+** risposta | Il Superbonus è stato uno spreco di soldi pubblici? |
| 2 | 1 | X | X = X **+** risposta | Più soldi pubblici alla sanità? |
| 3 | 2 | X | X = X **−** risposta | Lo Stato deve salvare le grandi aziende in crisi, come l'ex Ilva? |
| 4 | 3 | X | X = X **−** risposta | Ci vuole una difesa comune europea? |
| 5 | 4 | Y | Y = Y **+** risposta | Basta inviare armi all'Ucraina? |
| 6 | 5 | Y | Y = Y **−** risposta | Ridurre anche l'immigrazione regolare? |
| 7 | 6 | Y | Y = Y **−** risposta | L'Italia deve riconoscere lo Stato di Palestina? |
| 8 | 7 | Y | Y = Y **+** risposta | I partiti al governo da 20 anni sanno fare le riforme? |
| 9 | 8 | Z | Z = Z **−** risposta | Ogni processo deve avere una durata massima fissata per legge? |
| 10 | 9 | Z | Z = Z **+** risposta | Stessa scuola per tutti fino a 16 anni? |
| 11 | 10 | Z | Z = Z **+** risposta | L'ISEE basta per decidere chi riceve aiuti pubblici? |
| 12 | 11 | Z | Z = Z **−** risposta | *(nessuna: nascondi `Domanda` ed `Etichette`, mostra `Risultato`, esegui l'albero della sezione 5)* |

La prima domanda (mostrata all'avvio, collegando `Start` a un `Set Text`) è:
**"Le pensioni vanno calcolate sui contributi versati?"**

## 5. Albero del risultato (31 nodi If)

Ogni `SE … :` è un If con condizione **≥** (Greater or Equal). Uscita vera → blocco rientrato sotto; uscita falsa → `ALTRIMENTI`.
Ogni `→ Partito` è un `Set Text` su `Risultato` con quel nome.

```
SE X ≥ -2:
   SE X ≥ 0:
      SE Y ≥ 0:
         SE Z ≥ 0:
            SE Z ≥ 2:
               → ORA!
            ALTRIMENTI:
               SE X ≥ 2:
                  → Partito Liberaldemocratico
               ALTRIMENTI:
                  SE Y ≥ 2:
                     SE Y ≥ 4:
                        → +Europa
                     ALTRIMENTI:
                        → Azione
                  ALTRIMENTI:
                     → Fratelli d'Italia
         ALTRIMENTI:
            SE X ≥ 2:
               SE Y ≥ 4:
                  → +Europa
               ALTRIMENTI:
                  → Forza Italia
            ALTRIMENTI:
               SE Y ≥ 2:
                  SE Y ≥ 4:
                     → Italia Viva
                  ALTRIMENTI:
                     SE Z ≥ -2:
                        → Italia Viva
                     ALTRIMENTI:
                        → Partito Democratico
               ALTRIMENTI:
                  → Noi Moderati
      ALTRIMENTI:
         SE Z ≥ 0:
            → Futuro Nazionale
         ALTRIMENTI:
            → Lega
   ALTRIMENTI:
      SE Y ≥ 0:
         SE Y ≥ 2:
            SE Z ≥ 0:
               SE Z ≥ 2:
                  → ORA!
               ALTRIMENTI:
                  SE Y ≥ 4:
                     → Partito Democratico
                  ALTRIMENTI:
                     → Alleanza Verdi e Sinistra
            ALTRIMENTI:
               → Partito Democratico
         ALTRIMENTI:
            SE Z ≥ 0:
               → Movimento 5 Stelle
            ALTRIMENTI:
               → Alleanza Verdi e Sinistra
      ALTRIMENTI:
         SE Z ≥ 0:
            SE Z ≥ 2:
               → Futuro Nazionale
            ALTRIMENTI:
               → Movimento 5 Stelle
         ALTRIMENTI:
            SE Y ≥ -2:
               → Movimento 5 Stelle
            ALTRIMENTI:
               → Lega
ALTRIMENTI:
   SE Y ≥ -2:
      SE Y ≥ 0:
         SE Z ≥ 0:
            SE Z ≥ 4:
               SE Y ≥ 2:
                  → ORA!
               ALTRIMENTI:
                  → Movimento 5 Stelle
            ALTRIMENTI:
               → Alleanza Verdi e Sinistra
         ALTRIMENTI:
            SE Y ≥ 4:
               → Partito Democratico
            ALTRIMENTI:
               → Alleanza Verdi e Sinistra
      ALTRIMENTI:
         SE Z ≥ 4:
            → Futuro Nazionale
         ALTRIMENTI:
            → Movimento 5 Stelle
   ALTRIMENTI:
      SE Z ≥ 2:
         → Futuro Nazionale
      ALTRIMENTI:
         → Movimento 5 Stelle
```

## 6. Prove di verifica

| 12 risposte in ordine | X | Y | Z | Risultato atteso |
|---|---|---|---|---|
| SÌ SÌ SÌ NO · SÌ NO NO SÌ · NO SÌ SÌ NO | 2 | 4 | 4 | ORA! |
| tutti SÌ | 0 | 0 | 0 | Fratelli d'Italia |
| tutti NO | 0 | 0 | 0 | Fratelli d'Italia |
| NO NO SÌ SÌ · NO SÌ SÌ NO · SÌ NO NO SÌ | −4 | −4 | −4 | Movimento 5 Stelle |

## 7. Colori dei partiti (testo di `Risultato`)

ORA! #ea580c · Partito Liberaldemocratico #0ea5e9 · +Europa #c026d3 · Azione #3b82f6 · Italia Viva #db2777 ·
Forza Italia #2563eb · Noi Moderati #0891b2 · Partito Democratico #dc2626 · Fratelli d'Italia #3b5bdb · Lega #16a34a ·
Futuro Nazionale #a16207 · Movimento 5 Stelle #ca8a04 · Alleanza Verdi e Sinistra #65a30d

## Come vorrei procedere

1. Verifica il grafo esistente (sezione 3), in particolare che `step` aumenti di 1 a ogni tocco.
2. Completa i rami 2–12 (sezione 4) e prova che le domande scorrano tutte.
3. Costruisci l'albero del risultato (sezione 5).
4. Fai le prove della sezione 6.
5. Spiegami ogni passo in italiano, in modo semplice: non sono esperta di Effect House.
