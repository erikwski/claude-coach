---
description: Sincronizza le nuove corse da Intervals.icu nel DB locale (data/runs)
argument-hint: "[--from YYYY-MM-DD] [--force]"
---

Sincronizza le corse **non ancora presenti** nel DB locale. Sola lettura su Intervals.icu: non scrivere mai lì.

Argomenti: $ARGUMENTS

## DB locale
- `data/runs/index.json`: stato sync + riepilogo di ogni corsa.
- `data/runs/<YYYY-MM-DD>_<activity_id>.json`: dati completi della singola corsa.

Formato `index.json`:
```json
{
  "athlete_id": "i731779",
  "last_sync": "2026-09-29T21:00:00",
  "runs": [
    {"id": "i191620669", "date": "2026-09-29", "name": "...", "file": "2026-09-29_i191620669.json",
     "distance_m": 8181, "moving_time_s": 2823, "avg_hr": 147, "avg_pace_min_km": "5:45", "analyzed": false}
  ]
}
```

## Procedura
1. Leggi `data/runs/index.json`. Se manca, crealo con `runs: []` (prima sync = backfill dal 2026-01-01 o da `--from`).
2. Data di partenza = `--from` se dato, altrimenti la data dell'ultima corsa nell'indice meno 2 giorni (margine per attività caricate in ritardo). Fine = oggi.
3. `get_activities` (server `intervals-icu`) con `start_date`, `end_date`, `limit` alto (200), `include_unnamed: true`.
4. Tieni solo `Type` = `Run` (o `VirtualRun`, `TrailRun`). Scarta il resto.
5. Confronta gli `id` con l'indice. Nuove = non presenti. Con `--force` riscarica anche le esistenti (sovrascrivi il file, conserva `analysis` e `analyzed`).
6. Per ogni nuova corsa:
   - `get_activity_details` → metriche complete.
   - `get_activity_intervals` → intervalli/lap (se errore, salva `intervals: null`).
   - **Non** scaricare gli streams in sync (troppo pesanti). Li scarica `/analizza-corsa` solo se serve.
   - Scrivi il file `data/runs/<data>_<id>.json` con la struttura sotto.
   - Aggiungi la riga a `index.json` con `analyzed: false`.
7. Riordina `runs` per data crescente, aggiorna `last_sync`, salva.
8. Se il piano prevedeva una seduta quel giorno (`plan-events.json` / `training-plan.md`), scrivi in `planned` il nome/tipo previsto (non serve chiamare `get_events` per tutte: solo se ne trovi una corrispondente per data nel file).
9. Report finale breve in italiano: quante nuove, elenco (data, nome, km, ritmo, FC media), eventuali errori. Suggerisci `/analizza-corsa` per le non analizzate.

## Struttura file singola corsa
```json
{
  "id": "i191620669",
  "date": "2026-09-29",
  "start_local": "2026-09-29T17:26:51",
  "name": "...",
  "type": "Run",
  "planned": {"event_name": "S1 Mar - Facile + 5 allunghi", "kind": "facile"},
  "summary": {
    "distance_m": 8181, "duration_s": 2915, "moving_time_s": 2823,
    "avg_speed_ms": 2.894, "avg_pace_min_km": "5:45", "max_speed_ms": 4.74,
    "elevation_gain_m": 38.6, "avg_hr": 147, "max_hr": 179, "lthr": 182, "resting_hr": 55,
    "cadence": 81.06, "avg_stride_m": 1.07, "calories": 562, "weight_kg": 73
  },
  "load": {"training_load": 49, "hr_load": 37, "pace_load": 49, "trimp": 64.6,
           "intensity": 79.0, "polarization_index": 0.0, "efficiency_factor": null, "decoupling": null},
  "subjective": {"rpe": 1, "session_rpe": 47, "feel": 1},
  "intervals": [],
  "streams_derived": null,
  "analysis": null,
  "synced_at": "2026-09-29T21:00:00"
}
```
- Ritmo min/km = 1000 / velocità_ms / 60 → formatta `m:ss`. Calcolalo tu, non stimarlo a occhio.
- Campi `None` dell'API → `null`. Non inventare valori.
- Nessuna credenziale nei file.
