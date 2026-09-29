# Decisions log

Storico cronologico delle discussioni e delle modifiche al piano. Da aggiornare a ogni cambio.

## 2026-09-29 – Costruzione del piano
- Richiesta iniziale: pianificare la preparazione a una mezza maratona il 20/12/2026 con obiettivo 1:35. Tre corse a settimana (martedì, venerdì, domenica) + bici il giovedì. Mezza tranquilla il 13/12. Ripresa progressiva nelle prime due settimane.
- Intervals.icu non conteneva dati (nessuna attività, wellness o evento). Il piano è stato costruito su soglie fornite a mano (VC 4:33, D' 160 m, zone in `athlete-profile.md`).
- Nota sul calendario: il 13/12/2026 è una **domenica**, non un sabato (errore iniziale corretto). La mezza tranquilla sostituisce il lungo di quella settimana.
- Realismo dell'obiettivo: 1:35 richiede circa 101% della VC; tempo realistico oggi 1:38–1:40, serve un miglioramento della VC di circa il 3%.

## Modifiche successive (in ordine)
1. **Più spinta nelle prime settimane:** l'atleta ha detto di non essere fermo. Volume iniziale più alto (26 km alla settimana 1, lungo fino a 20 km alla settimana 8) e ripetute già dalla settimana 2.
2. **Alternative al venerdì easy run:** proposti progressivo, fartlek, fondo medio, easy con esercizi. Scelta: primo mese progressivo, secondo mese fartlek, poi easy run.
3. **Bilanciamento intensità:** nelle settimane con lungo di qualità la domenica, il venerdì è easy run. Restano con qualità solo il venerdì delle settimane 1 (progressivo) e 6 (fartlek, scarico).
4. **Feedback esterno sul piano:** sono stati incollati commenti (regola 80/20, recuperi più lunghi nei lavori chiave, più soglia e meno VO2max, il test 3×3 km non è un test pulito). Applicati: test → gara di 10 km; sostituiti tutti i lavori a 4:20 con ripetute a 4:30–4:33. Non applicati (non richiesti): domeniche alternate a fondo puro, recuperi a 3' su tutti i lavori lunghi.
5. **Settimana 9:** il test è ora una gara di 10 km domenica 29/11; il martedì ha ripetute più leggere (4×1 km a 4:33), venerdì ridotto a 6 km.
6. **Forza + Zwift:** aggiunti da lunedì 5/10 (forza + pliometria) e giovedì 8/10 (Zwift). Nessun FTP disponibile, quindi la bici è a FC 120–150.
7. **Caricamento su Intervals.icu:** 55 eventi (corsa, bici, forza). Vedi `intervals-integration.md` per i problemi incontrati.

## 2026-09-29 – Alimentazione e integrazione
- Richiesta: aggiungere alimentazione e integrazione al piano. Dati forniti: maschio, 26 anni, 168 cm, 73 kg; obiettivo mantenere o perdere 1–2 kg; dieta vegetariana con pesce; poco tempo per cucinare (usa il freezer); esami nella norma; integratori attuali: creatina, omega 3, vitamina D, zinco, magnesio.
- Creato `nutrition-plan.md`: target kcal e macro per tipo di giornata, schema pasti con kit pre e post allenamento, fueling nei lunghi, strategia per il 10 km (29/11) e la mezza (13/12 e 20/12), integrazione, controllo del peso.
- Nessun cambio al piano di allenamento. Nessuna scrittura su Intervals.icu.

## 2026-09-29 – Spesa e menu freezer
- Creato `shopping-and-menus.md`: menu settimanale giorno per giorno, ricette da surgelare (ragù di lenticchie, curry di ceci, zuppa di ceci), lista della spesa settimanale, scorta freezer, gel e sessione di cucina tipo.
- Modificato il sabato in `nutrition-plan.md`: cena con 100 g di pasta o riso al posto delle patate.

## 2026-09-29 – Sito consultabile
- Creata la cartella `site/` con `plan.json` (allenamento, forza, gare, alimentazione, menu, ricette, spesa) e `index.html` (pagina statica che legge il JSON), più `vercel.json` con header noindex. Da deployare su Vercel con root `site`.
- Il JSON è una copia dei file `.md`: aggiornarlo a ogni modifica. Nel JSON non sono inclusi età, altezza, peso ed esami del sangue. Restano note generali su integrazione (creatina, vitamina D, ecc.) e sul controllo del peso.

## Punti aperti / da decidere
- Alimentazione: decidere se continuare la creatina (peso +1–2 kg) o sospenderla nelle ultime 4–6 settimane.
- Alimentazione: scegliere prodotti per i gel (marca, con o senza caffeina) e provarli nei lunghi.
- Decidere se applicare le proposte esterne non ancora accolte (domeniche alternate a fondo puro, recuperi più lunghi).
- Valutare dopo il 10 km del 29/11 se confermare 1:35 o abbassare l'obiettivo (tabella in `training-plan.md`).
- Eventuale test dell'FTP in bici (ramp test in scarico, 5/11) — non necessario per le uscite facili.
- Nome della settimana 1 nel calendario: dopo alcuni cambi (S1 → S! → S1) è tornato a "S1".
