# Brief per gli agenti coach

Bozza dei requisiti per gli agenti che dovranno commentare le attività e tenere traccia dei progressi e dei cambi di allenamento. Da rifinire prima di implementare.

## Fonte dei dati
- Intervals.icu (athlete `i731779`): attività svolte, wellness, eventi pianificati (`get_activities`, `get_activity_details`, `get_wellness_data`, `get_events`).
- Contesto stabile nei file di questa cartella: `athlete-profile.md`, `training-plan.md`, `decisions-log.md`, `progress-log.md`.

## Agenti proposti

### 1. Coach delle sedute (post-attività)
- **Quando:** dopo ogni attività sincronizzata.
- **Input:** attività eseguita, seduta pianificata nello stesso giorno, zone di ritmo/FC.
- **Output:** commento breve (rispetto dei ritmi, ripetute, FC, carico rispetto al previsto), semaforo (in linea / da monitorare / da correggere), eventuale nota nel `progress-log.md`.
- **Regole:** confrontare con i ritmi del piano (facile 5:50, sub-soglia 4:56, VC 4:33, gara 4:30). Segnalare se le sedute facili sono troppo veloci o se le ripetute a VC sono troppo dure per il recupero previsto.

### 2. Analista dei progressi (settimanale)
- **Quando:** domenica sera o lunedì.
- **Output:** riepilogo settimanale (km, carico, sedute saltate), andamento della VC/ritmi a parità di sforzo, confronto con la tabella del piano, stato della forma per il 1:35.
- **Regole:** aggiornare `progress-log.md`; usare il 10 km del 29/11 come checkpoint per la decisione sull'obiettivo.

### 3. Gestore del piano (aggiustamenti)
- **Quando:** su richiesta o quando l'analista segnala scostamenti.
- **Output:** proposta di modifica al piano (motivo, sedute coinvolte, impatto su volume e intensità), approvata dall'atleta prima di scrivere su Intervals.icu.
- **Regole:** non modificare eventi passati; registrare ogni cambio in `decisions-log.md`; rispettare i vincoli (3 corse: mar/ven/dom; giovedì bici; lunedì forza; riposo dopo le gare).

### 4. Guardiano di recupero (opzionale)
- **Input:** wellness (sonno, HRV, FC a riposo), carico degli ultimi 7–14 giorni.
- **Output:** avviso se il carico sale troppo (oltre circa +10% a settimana) o se i segnali di recupero peggiorano, con suggerimento di alleggerire.

## Vincoli di sicurezza
- Non scrivere su Intervals.icu senza conferma dell'atleta.
- Non salvare credenziali (API key) nei file del progetto.
- Commenti sportivi e di carico, non consigli medici: in caso di dolore o infortunio, invitare a consultare un professionista.

## Note tecniche utili (dettagli in `intervals-integration.md`)
- Soglia di ritmo Corsa in Intervals.icu: 4:33/km (3,67 m/s). Gli step usano `%pace`.
- Usare `plan-events.json` per mappare data → ID evento.
- Le descrizioni degli eventi sono nella sintassi del workout builder di Intervals.icu.
