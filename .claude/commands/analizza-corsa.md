---
description: Analizza e commenta una o più corse usando il DB locale e la base scientifica
argument-hint: "[ultima | YYYY-MM-DD | activity_id | ultime N | non-analizzate]"
---

Analizza le corse dell'atleta. Rispondi in italiano, tono da coach, breve e concreto. Nessun consiglio medico.

Argomento: $ARGUMENTS (default: `ultima`)

## Passi
1. **Leggi prima**: `analysis-science.md` (soglie e regole di commento), `athlete-profile.md` (VC 4:33, zone, LTHR), `training-plan.md` (seduta prevista), `decisions-log.md`, `progress-log.md`.
2. **Sync**: leggi `data/runs/index.json`. Se manca o l'ultima corsa è più vecchia di quella su Intervals, esegui prima la procedura di `.claude/commands/sync-corse.md`.
3. **Seleziona corse** dal DB:
   - `ultima` = più recente; data / id = quella; `ultime N` = ultime N; `non-analizzate` = `analyzed: false`.
4. **Per ogni corsa** carica `data/runs/<file>.json`, poi:
   - Classifica il tipo (facile, lungo, ripetute, soglia, fartlek, progressivo, gara) da nome + piano.
   - Se serve il pacing/decoupling e `streams_derived` è null: `get_activity_streams` con `stream_types: "time,heartrate,velocity_smooth,distance,altitude"`. Calcola (script Python nello scratchpad, non a mano): split per km, half-ratio, CV ritmo, decoupling Pa:HR (2ª metà vs 1ª, escludendo i primi 10 min), FC media per metà. **Decoupling solo su sforzi continui ≥40 min a ritmo stabile e poco dislivello**; altrimenti scrivi "non applicabile".
   - Per lavori a intervalli: usa `intervals` (ritmo/FC per rep, calo tra prima e ultima rep, aderenza al target in % VC).
   - Confronta con le ultime 3–4 corse dello stesso tipo nel DB (EF, ritmo a FC simile, decoupling, RPE).
   - Facoltativo: `get_wellness_data` ±2 giorni (HRV, FC riposo, sonno) per contestualizzare RPE/Feel.
5. **Scrivi output** per corsa (max ~15 righe):
   - **Seduta**: previsto vs eseguito (ritmo, durata, zona in % VC).
   - **Intensità**: FC vs LTHR 182, distribuzione zone, coerenza con lo scopo (facile davvero facile?).
   - **Efficienza/resistenza**: EF, decoupling (con soglie e validità), trend.
   - **Pacing**: split, regolarità.
   - **Soggettivo**: RPE/Feel vs dati.
   - **Verdetto** (una frase) + **1–2 azioni** per le prossime sedute.
   - **Dati mancanti / affidabilità**.
   Se più corse: aggiungi in fondo un riepilogo di trend e carico settimanale (km, sRPE, rampa vs settimana precedente; ACWR solo come segnale, mai come predittore di infortunio).
6. **Persisti**: nel file JSON della corsa scrivi `streams_derived` (se calcolato) e `analysis` = `{date, verdict, actions, key_metrics}`; in `index.json` metti `analyzed: true`.
7. Non modificare Intervals.icu. Non cambiare il piano: se emerge un motivo per farlo, **proponilo** all'atleta; se accolto aggiorna `decisions-log.md`. Esiti di sedute chiave (test, gare) → anche `progress-log.md` dopo conferma.

## Regole
- Un dato singolo non è un trend: dichiara l'incertezza.
- Non usare ritmi assoluti inventati: calcola da velocità (min/km = 1000 / m/s / 60).
- Scala `Feel` di Intervals: verifica con l'atleta se 1 = ottimo o pessimo prima di trarre conclusioni.
- Se FC a riposo alta, HRV bassa, RPE alto con dati normali, oppure dolore segnalato: suggerisci riposo/consulto di un professionista.
