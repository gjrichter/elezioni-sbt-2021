# Elezioni Comunali San Benedetto del Tronto 2021

Mappe interattive dei risultati delle elezioni comunali del 3–4 ottobre 2021.

**Dati**: AMMINISTRATIVE 2021 – DATI VALIDATI ALL'UFFICIO CENTRALE  
**Fonte**: [elezioni.comunesbt.it](https://elezioni.comunesbt.it) (cdele=3, macro=S3, path=storico)  
**Sezioni**: 43 · **Votanti**: 24.070 / 40.211 iscritti (59,8%)

## Risultati

| # | Candidato | Voti | % |
|---|-----------|------|---|
| 4 | **Piunti Pasqualino** 🥇 | 9.706 | 41,5% |
| 1 | Spazzafumo Antonio | 4.452 | 19,0% |
| 3 | Canducci Paolo | 3.794 | 16,2% |
| 2 | Bottiglieri Aurora | 3.679 | 15,7% |
| 5 | Angelini Serafino | 1.724 | 7,4% |

Piunti non raggiunge il 50%+1 → ballottaggio con Spazzafumo (17–18 ottobre 2021).

## Mappe

- `map_sezioni.html` — 43 sezioni per collegio (5 collegi, colori distinti)
- `map_vincente.html` — candidato vincente per sezione
- `map_percentuali.html` — percentuali dei 5 candidati aggregati per sede
- `map_voti.html` — voti assoluti per candidato e sede

## Struttura dati

```
data/
  meta.json                        ← riepilogo fetch
  totale_raggrup.json              ← voti totali con anagrafica candidati
  totale_liste.json                ← voti per lista
  totale_candidati.json            ← voti preferenze
  sezioni_con_sede.geojson         ← 43 sezioni (geometria = posizione sede)
  sedi_sezioni_elettorali.geojson  ← 10 sedi elettorali (con range sezioni)
  sezioni/
    001/ raggrup.json, liste.json, candidati.json
    002/ ...
    043/ ...
```

## Aggiornamento dati

```bash
node fetch-scrutinio.js
```

Scarica i dati storicizzati (cdele=3) da Eleweb e sovrascrive i file in `data/`.

## Note tecniche

Le mappe usano [ixMaps](https://github.com/gjrichter/ixmaps-flat) con pattern FEATURE+overlay:
il layer base carica la geometria dei punti (sedi), l'overlay join calcola
voti/percentuali on-the-fly nel browser tramite `Promise.all(fetch(...))` su 43 file JSON.
