# Bussola Politica Lampo — come costruirla in Effect House

Guida operativa per ricostruire la versione TikTok (`tiktok.html`) come effetto in **Effect House**, con il Visual Scripting.
Il risultato è identico alla pagina web: 12 domande sì/no, tre contatori, 125 combinazioni possibili, 13 partiti.

> I nomi dei nodi sono quelli della documentazione di Effect House (Screen Tap, If, Sequence, Get/Set delle variabili, nodi Math, Set Visibility).
> Se nella tua versione un nome è leggermente diverso, cerca nel menu dei nodi la parola chiave indicata tra parentesi.

---

## 1. Oggetti nella scena

Nel pannello **Hierarchy** crea:

| Nome oggetto | Tipo | A cosa serve |
|---|---|---|
| `Domanda` | 2D Text | mostra la domanda corrente |
| `Risultato` | 2D Text | mostra il partito alla fine (all'inizio **nascosto**) |
| `Etichette` | 2D Text con scritto `NO          SÌ` | ricorda di toccare a sinistra o a destra |

## 2. Variabili

Nel pannello **Variables** crea 4 variabili di tipo **Number**, tutte con valore iniziale **0**:

| Variabile | Significato |
|---|---|
| `step` | numero della domanda corrente, da 0 a 11 |
| `X` | Stato (−) ↔ Mercato (+) |
| `Y` | Sovranismo (−) ↔ Europeismo (+) |
| `Z` | Vecchia politica (−) ↔ Discontinuità (+) |

Più una quinta variabile **Number** `risposta` (vale +1 per SÌ, −1 per NO).

## 3. Grafo "Avvio"

```
[Start]  →  [Set Text]  Domanda = "Le pensioni vanno calcolate sui contributi versati?"
```

- **Start** (cerca: *start*): parte quando si apre l'effetto.
- **Set Text** (cerca: *text*): trascina l'oggetto `Domanda` nel grafo e usa il suo setter del testo.

## 4. Grafo "Risposta" (uno solo per tutte le domande)

```
[Screen Tap]
    │
    ▼
[If]  condizione: posizione X del tocco > 0.5        (Math → Greater / Compare)
    ├─ vero  → [Set Variable] risposta = 1           (tocco a destra = SÌ)
    └─ falso → [Set Variable] risposta = -1          (tocco a sinistra = NO)
    │
    ▼
[Sequence]   (Control → Sequence) con 13 uscite, eseguite in ordine:
    uscita 1…12 → i 12 rami della tabella qui sotto
    uscita 13   → [Set Variable] step = step + 1     (Math → Add)
```

> **Posizione del tocco.** Screen Tap restituisce la posizione del dito. Se è normalizzata (da 0 a 1) confronta con **0.5**;
> se è in pixel confronta con **metà della larghezza dello schermo**.

### I 12 rami

Ogni ramo è fatto sempre allo stesso modo:

```
[If]  step == N                                     (Math/Logic → Equal)
  └─ vero → [Set Variable] ASSE = ASSE ± risposta    (Add oppure Subtract)
          → [Set Text] Domanda = TESTO DELLA PROSSIMA DOMANDA
```

Copia e incolla il primo ramo 12 volte e cambia solo i valori della tabella:

| Ramo | `step ==` | Variabile da aggiornare | Operazione | Testo della prossima domanda |
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
| 12 | 11 | Z | Z = Z **−** risposta | *(nessuna: vai al grafo "Risultato")* |

Il ramo 12, invece di cambiare il testo, fa:
`[Set Visibility] Domanda = nascosto` → `[Set Visibility] Risultato = visibile` → **grafo "Risultato"**.

## 5. Grafo "Risultato" — 31 nodi If

Alla fine X, Y e Z valgono ciascuno −4, −2, 0, 2 o 4. Invece di 125 condizioni basta questo albero di **31 nodi If**,
che dà esattamente lo stesso risultato della tabella completa (verificato su tutte le 125 combinazioni).

Ogni riga `SE … :` è un nodo **If** con condizione **Greater or Equal** (cerca: *greater*, *compare*).
L'uscita **vero** va al blocco rientrato subito sotto, l'uscita **falso** al blocco `ALTRIMENTI`.
Ogni `→ Partito` è un nodo **Set Text** sull'oggetto `Risultato` con quel nome.

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

### Come costruirlo senza perdersi

1. Costruisci prima solo il primo livello (`SE X ≥ -2`) con due nodi Set Text provvisori "A" e "B" e provalo.
2. Poi sostituisci "A" con il sotto-albero `SE X ≥ 0 …` e "B" con `SE Y ≥ -2 …`, e così via un livello alla volta.
3. Usa i **commenti/gruppi** del Visual Scripting per incorniciare ogni sotto-albero con il suo nome (es. "X ≥ 0 / Y ≥ 0").

## 6. Scorciatoia, se Effect House ha le liste di testo

Se nel pannello Variables esiste un tipo **lista di stringhe** (cerca: *array*, *list*), puoi sostituire tutto l'albero con 3 nodi:

1. calcola `indice = (X + 4) / 2 × 25 + (Y + 4) / 2 × 5 + (Z + 4) / 2` (nodi Add, Divide, Multiply): esce un numero da 0 a 124;
2. leggi l'elemento `indice` della lista (cerca: *get item*, *element*);
3. Set Text su `Risultato`.

La lista, nell'ordine dell'indice:

```
  0  Movimento 5 Stelle
  1  Movimento 5 Stelle
  2  Movimento 5 Stelle
  3  Futuro Nazionale
  4  Futuro Nazionale
  5  Movimento 5 Stelle
  6  Movimento 5 Stelle
  7  Movimento 5 Stelle
  8  Movimento 5 Stelle
  9  Futuro Nazionale
 10  Alleanza Verdi e Sinistra
 11  Alleanza Verdi e Sinistra
 12  Alleanza Verdi e Sinistra
 13  Alleanza Verdi e Sinistra
 14  Movimento 5 Stelle
 15  Alleanza Verdi e Sinistra
 16  Alleanza Verdi e Sinistra
 17  Alleanza Verdi e Sinistra
 18  Alleanza Verdi e Sinistra
 19  ORA!
 20  Partito Democratico
 21  Partito Democratico
 22  Alleanza Verdi e Sinistra
 23  Alleanza Verdi e Sinistra
 24  ORA!
 25  Lega
 26  Lega
 27  Movimento 5 Stelle
 28  Futuro Nazionale
 29  Futuro Nazionale
 30  Movimento 5 Stelle
 31  Movimento 5 Stelle
 32  Movimento 5 Stelle
 33  Futuro Nazionale
 34  Futuro Nazionale
 35  Alleanza Verdi e Sinistra
 36  Alleanza Verdi e Sinistra
 37  Movimento 5 Stelle
 38  Movimento 5 Stelle
 39  Movimento 5 Stelle
 40  Partito Democratico
 41  Partito Democratico
 42  Alleanza Verdi e Sinistra
 43  ORA!
 44  ORA!
 45  Partito Democratico
 46  Partito Democratico
 47  Partito Democratico
 48  ORA!
 49  ORA!
 50  Lega
 51  Lega
 52  Futuro Nazionale
 53  Futuro Nazionale
 54  Futuro Nazionale
 55  Lega
 56  Lega
 57  Futuro Nazionale
 58  Futuro Nazionale
 59  Futuro Nazionale
 60  Noi Moderati
 61  Noi Moderati
 62  Fratelli d'Italia
 63  ORA!
 64  ORA!
 65  Partito Democratico
 66  Italia Viva
 67  Azione
 68  ORA!
 69  ORA!
 70  Italia Viva
 71  Italia Viva
 72  +Europa
 73  ORA!
 74  ORA!
 75  Lega
 76  Lega
 77  Futuro Nazionale
 78  Futuro Nazionale
 79  Futuro Nazionale
 80  Lega
 81  Lega
 82  Futuro Nazionale
 83  Futuro Nazionale
 84  Futuro Nazionale
 85  Forza Italia
 86  Forza Italia
 87  Partito Liberaldemocratico
 88  ORA!
 89  ORA!
 90  Forza Italia
 91  Forza Italia
 92  Partito Liberaldemocratico
 93  ORA!
 94  ORA!
 95  +Europa
 96  +Europa
 97  Partito Liberaldemocratico
 98  ORA!
 99  ORA!
100  Lega
101  Lega
102  Futuro Nazionale
103  Futuro Nazionale
104  Futuro Nazionale
105  Lega
106  Lega
107  Futuro Nazionale
108  Futuro Nazionale
109  Futuro Nazionale
110  Forza Italia
111  Forza Italia
112  Partito Liberaldemocratico
113  ORA!
114  ORA!
115  Forza Italia
116  Forza Italia
117  Partito Liberaldemocratico
118  ORA!
119  ORA!
120  +Europa
121  +Europa
122  Partito Liberaldemocratico
123  ORA!
124  ORA!
```

## 7. Prove da fare in anteprima

| Risposte (in ordine, 12 tocchi) | X | Y | Z | Risultato atteso |
|---|---|---|---|---|
| SÌ SÌ SÌ NO · SÌ NO NO SÌ · NO SÌ SÌ NO (come ORA!) | 2 | 4 | 4 | ORA! |
| tutti SÌ | 0 | 0 | 0 | Fratelli d'Italia |
| tutti NO | 0 | 0 | 0 | Fratelli d'Italia |
| NO NO SÌ SÌ · NO SÌ SÌ NO · SÌ NO NO SÌ | −4 | −4 | −4 | Movimento 5 Stelle |

Se un risultato non torna, controlla prima la colonna **Operazione** della tabella dei 12 rami (un + al posto di un −).

## 8. Colori dei partiti (per il testo del risultato)

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

## Nota

Prima della pubblicazione TikTok revisiona ogni effetto. Un effetto che nomina partiti politici può essere respinto:
in quel caso registra la pagina `tiktok.html` con la registrazione schermo del telefono e pubblica il video.
