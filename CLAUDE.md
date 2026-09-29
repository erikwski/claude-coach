# Running Coach – Mezza maratona 20/12/2026

Progetto di coaching per una mezza maratona con obiettivo **1:35:00 (4:30/km)** domenica **20/12/2026**. Questa cartella contiene contesto, piano e decisioni; gli agenti coach useranno questi file più i dati di Intervals.icu.

## Lingua e stile
- Rispondere in **italiano**.
- Commenti tecnici brevi e concreti. Nessun consiglio medico: in caso di dolore o infortunio, suggerire di consultare un professionista.

## File di riferimento (leggere prima di agire)
- `athlete-profile.md`: obiettivi, soglie, zone di ritmo, vincoli.
- `training-plan.md`: piano settimana per settimana (29/9 – 20/12/2026).
- `decisions-log.md`: storico delle modifiche e punti aperti. **Aggiornarlo a ogni cambio di piano.**
- `progress-log.md`: esiti di sedute chiave, test, gare, infortuni.
- `nutrition-plan.md`: alimentazione, fueling e integrazione (atleta 168 cm, 73 kg, vegetariano con pesce).
- `shopping-and-menus.md`: menu settimanale, ricette freezer e lista della spesa.
- `site/plan.json` + `site/index.html`: versione consultabile del piano (sito statico per Vercel). `plan.json` è una copia dei file `.md`: va aggiornato a ogni cambio di piano, alimentazione o menu.
- `intervals-integration.md`: sintassi dei workout, problemi noti e soluzioni.
- `agents-brief.md`: requisiti degli agenti coach.
- `plan-events.json`: mappa data → ID evento su Intervals.icu.

## Dati base dell'atleta
- Velocità Critica (VC): 3,67 m/s = **4:33/km**, D' 160 m.
- Zone (min/km): recupero 6:30 (70%), facile 5:50 (78%), medio 5:21 (85%), sub-soglia 4:56 (92%), VC 4:33 (100%), VO2max 4:20 (105%), allunghi 4:04 (112%). Ritmo gara 4:30 (~101%).
- Bici: nessun FTP. Sedute facili a **FC 120–150 bpm**.
- Realismo dell'obiettivo: con la VC attuale il tempo realistico è 1:38–1:40; per 1:35 la VC deve salire a circa 4:22–4:25.

## Struttura settimanale
- Lunedì: forza per runner + pliometria (dal 5/10; riposo dopo le gare).
- Martedì: corsa di qualità (ripetute/soglia).
- Mercoledì: riposo.
- Giovedì: bici sui rulli con Zwift, facile, FC 120–150 (dal 8/10).
- Venerdì: easy run (progressivo alla sett. 1, fartlek alla sett. 6).
- Sabato: riposo.
- Domenica: lungo, spesso con finale a ritmo.

## Date chiave
- **Domenica 29/11/2026:** gara 10 km, test per decidere l'obiettivo (≤44:45 → 1:35; 44:45–46:00 → 1:37; >46:00 → 1:38–1:40).
- **Domenica 13/12/2026:** mezza maratona tranquilla a 5:10–5:20/km (senza spingere). Lunedì 14/12 riposo.
- **Domenica 20/12/2026:** gara obiettivo. Primi 5 km a 4:33, poi 4:30; accelerare dopo il 15° km se si sta bene.
- Settimane di scarico/attenzione: sett. 6 (2–8/11) scarico; sett. 8 ha il lungo da 20 km (22/11), accorciabile a 18 km.

## Intervals.icu
- Athlete ID: `i731779`. Il piano è caricato come eventi WORKOUT (Run, VirtualRide, WeightTraining).
- MCP locale: `C:\Users\EFerrari\tools\intervals-mcp-server` (server `intervals-icu`).
- Soglia di ritmo Corsa nel profilo: 3,67 m/s (4:33/km). Gli step usano `%pace`.
- Sintassi descrizione: `Warmup` / `4x` / `Cooldown`, una riga per passo `- 1km 92% Pace ...`. Vedere `intervals-integration.md`.

## Regole di lavoro
- **Non scrivere su Intervals.icu senza conferma** dell'atleta.
- **Non salvare credenziali** (API key) in nessun file del progetto.
- Prima di modificare un evento, verificare ID e data con `get_events` (in passato due eventi sono stati confusi).
- Nelle descrizioni usare `1.5km` e non `1500m`: `m` significa minuti.
- Il 13/12/2026 è una **domenica**: la mezza tranquilla sostituisce il lungo di quella settimana.
- Quando cambia il piano: aggiornare `training-plan.md`, `decisions-log.md` e, se serve, `plan-events.json`.
- Non applicare modifiche non richieste. Proposte esterne non ancora accolte: domeniche alternate a fondo puro e recuperi più lunghi nei lavori chiave (vedi `decisions-log.md`).
- Rispettare i vincoli: tre corse (mar/ven/dom), giovedì bici, lunedì forza, mercoledì e sabato riposo. Il venerdì è easy run nelle settimane con lungo di qualità.
