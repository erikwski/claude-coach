# Integrazione con Intervals.icu

## Stato
- Athlete ID: `i731779`. Il piano è caricato nel calendario come eventi di categoria WORKOUT (tipo Run, VirtualRide, WeightTraining).
- L'MCP usato è locale: `C:\Users\EFerrari\tools\intervals-mcp-server` (server Python, configurato in `~/.claude.json`, server `intervals-icu`). Le credenziali (API key) sono in quella configurazione: **non copiarle nei file del progetto**.
- Sincronizzazione dei workout con Garmin: attiva nell'account (`icu_garmin_upload_workouts: true`). I workout arrivano sull'orologio solo per i giorni più vicini.

## Eventi
`plan-events.json` contiene ID, data, nome e tipo di ogni evento creato. Serve per aggiornarli senza creare doppioni.

## Problemi incontrati e soluzioni
1. **"Type: Other" in `get_events`:** è solo un limite della funzione di formattazione dell'MCP (controlla un campo che l'API non restituisce per la lista). I dati reali sono corretti: categoria `WORKOUT`, tipo `Run`.
2. **Grafico dei passi assente:** la causa era la soglia di ritmo non impostata nel profilo Corsa. Gli step usano `%pace` (percentuale della soglia) e senza soglia non si possono calcolare. Soluzione: impostata la soglia di ritmo Corsa a **3,67 m/s (4:33/km)** tramite `PUT /athlete/{id}/sport-settings/{id}`.
3. **Ritmi assoluti (es. `4:56`) non funzionano** come passi con l'MCP: vengono salvati come numero senza unità. Usare la percentuale della VC: 78% = 5:50, 85% = 5:21, 92% = 4:56, 100% = 4:33, 101% ≈ 4:30, 112% = 4:04, 70% = 6:30.
4. **`1500m` viene letto come 1500 minuti** dalla sintassi testuale di Intervals.icu (`m` = minuti). Usare `1.5km` per le distanze in metri sotto il km, oppure `mtr`.
5. **Aggiornamento di un evento con l'MCP:** `add_or_update_event` sovrascrive tutto il contenuto. Attenzione agli ID: in una occasione sono stati confusi gli ID di due eventi e uno è stato sovrascritto per errore (poi ripristinato). Verificare sempre ID e data con `get_events` prima di modificare.
6. **Scrittura diretta via API:** più veloce dell'MCP per aggiornare molti eventi in serie (`PUT /athlete/{id}/events/{event_id}` con il solo campo `description`). Richiede l'header `User-Agent` (senza, l'API risponde 403) e autenticazione Basic con utente `API_KEY`.

## Sintassi delle descrizioni (workout builder di Intervals.icu)
Una riga per passo, durata/distanza per prima, poi il target:

```
Warmup
- 2km 78% Pace Riscaldamento

4x
- 1km 92% Pace 1 km sub-soglia
- 90s 70% Pace Recupero

Cooldown
- 1km 78% Pace Defaticamento
```

- Bici a FC: `- 20m 120-150bpm 90rpm`.
- Il server ricostruisce `workout_doc` (passi, durata e carico) dalla descrizione.

## Tipi di evento usati
| Attività | Tipo |
|---|---|
| Corsa | `Run` |
| Bici sui rulli (Zwift) | `VirtualRide` |
| Forza + pliometria | `WeightTraining` (solo testo, senza passi) |
