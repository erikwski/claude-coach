# Base scientifica per commentare le corse

Riferimento usato dal comando `/analizza-corsa`. Ricerca del 29/9/2026. Le soglie sono **indicative**, non diagnostiche: valgono per un singolo atleta solo se lette nel trend, non sul singolo dato.

## 1. Disaccoppiamento aerobico (Pa:HR / cardiac drift)
- Confronta il rapporto ritmo/FC della prima metà con la seconda metà di uno sforzo **continuo e a ritmo costante**. 5% = a FC costante si va il 5% più lenti nella seconda metà (o FC +5% a ritmo costante).
- Soglie usate comunemente: **<5%** buona resistenza aerobica a quell'intensità; **5–10%** limite moderato o fatica; **>10%** intensità sopra soglia aerobica o resistenza insufficiente.
- Validità: solo su corse facili/lunghe ≥ 40–60 min, terreno piatto, ritmo stabile. **Non calcolare** su ripetute, fartlek, progressivi, corse con molto dislivello.
- Confondenti: caldo/disidratazione (aumenta il drift), dislivello, sonno, caffeina, stress. Il drift cardiaco è legato a calo della gittata sistolica dopo 5–10 min di lavoro costante.
- Uso nel piano: sui lunghi e sulle easy run, se il decoupling scende a <5% a parità di ritmo nelle settimane → base aerobica in crescita.
- Fonti: [TrainingPeaks – Aerobic decoupling](https://www.trainingpeaks.com/coach-blog/aerobic-endurance-and-decoupling/), [Marathon Handbook](https://marathonhandbook.com/aerobic-decoupling/), [Uphill Athlete](https://uphillathlete.com/aerobic-training/heart-rate-drift/), [arXiv: HR efficiency in amateur runners](https://arxiv.org/pdf/2509.05961), [PMC: drift correction](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11070768/).

## 2. Efficiency Factor (EF) e trend ritmo/FC
- EF = velocità (m/s) / FC media. Confrontabile **solo** tra corse simili (stessa intensità, stesso tipo, condizioni simili).
- EF in crescita a parità di FC = miglior economia/forma. Un singolo valore non dice nulla.
- Alternativa robusta: ritmo medio alla FC target (es. ritmo a 145 bpm) nel tempo.

## 3. Distribuzione dell'intensità (polarizzato / 80-20)
- Atleti di resistenza ben allenati: circa **75–80% delle sedute (≈90% del tempo) a bassa intensità** (sotto la prima soglia), **~5% a soglia**, **15–20% ad alta intensità**; poco tempo nella zona media ("zona grigia"). Seiler la chiama "population optimum", non una legge.
- Nel programma: martedì (qualità) e lunghi con finale a ritmo sono i giorni duri; venerdì e giovedì (bici) devono restare davvero facili. Se le easy run escono a FC/ritmo troppo alti → segnalarlo.
- Metrica Intervals: `Polarization Index` (solo con dati di zona validi), tempo per zona.
- Fonti: [Seiler 2010, IJSPP](https://umh1617.umh.es/files/2016/05/02-IJSPP_2010_Seiler_0009.pdf), [Sanders/Seiler review, PMC4621419](https://pmc.ncbi.nlm.nih.gov/articles/PMC4621419/), [8020 Endurance](https://www.8020endurance.com/allaboutintensitybalance/), [Fast Talk Labs](https://www.fasttalklabs.com/pathways/polarized-training/).

## 4. Pacing: regolarità, negative split
- Negative split operativo: seconda metà **~1–3% più veloce** della prima. Le gare ben eseguite hanno pacing quasi costante.
- Indicatori: half-ratio (ritmo/velocità 2ª metà su 1ª), coefficiente di variazione del ritmo. Cluster "pacing regolare": half-ratio ≈ 0,95 ± 0,03 e CV ritmo ≈ 3,7 ± 1,8%; forte positive split: ≈ 0,82 e CV ≈ 12%. (Dati da maratone, applicare con cautela su altre distanze.)
- Per la mezza del 20/12: piano = primi 5 km a 4:33, poi 4:30, accelerazione dopo il 15° km. Valutare split a 5 km, deriva di ritmo e FC.
- Fonti: [PMC12307312 negative splits](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12307312/), [PMC13379030 pacing patterns](https://pmc.ncbi.nlm.nih.gov/articles/PMC13379030/), [Systematic review pacing marathon](https://www.sciencedirect.com/science/article/pii/S2405844024127910).

## 5. Velocità Critica (VC) e D'
- VC = massima intensità sostenibile in stato quasi stazionario; D' = capacità di lavoro sopra VC (m). Atleta: VC 3,67 m/s (4:33/km), D' 160 m.
- Lettura ripetute: ritmo > VC consuma D' e serve recupero per ricostituirlo; sotto VC è sostenibile. Ripetute alla VC/sub-soglia con recuperi brevi: valutare se il ritmo tiene fino all'ultima rep (calo <2–3% = buon controllo).
- Stima VC aggiornata: usare test/gare (3–20 min) o best effort; ricalcolare dopo la 10 km del 29/11. Obiettivo: VC ~4:22–4:25.
- Predittore: la velocità a soglia spiega gran parte della varianza di prestazione in maratona/mezza (più del VO2max).

## 6. Carico e rischio infortuni
- Carico esterno (ritmo/distanza, `Pace Load`) e interno (FC, `HR Load`, TRIMP, sRPE = RPE × durata) misurano cose diverse. Guardare entrambi.
- ACWR (carico acuto 7 gg / cronico 28 gg): fascia "sicura" citata 0,8–1,3; >1,5 rischio alto. **Evidenza debole e contestata**: non usarlo come predittore di infortuni; usarlo solo come segnale di picchi improvvisi (rampa carico > ~10–15%/sett.).
- Nessun consiglio medico: dolore o infortunio → professionista.
- Fonti: [PMC12487117 ACWR](https://pmc.ncbi.nlm.nih.gov/articles/PMC12487117/), [PubMed 32158285](https://pubmed.ncbi.nlm.nih.gov/32158285/), [PMC10765439 acuto vs cronico](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10765439/), [Science for Sport](https://www.scienceforsport.com/acutechronic-workload-ratio/).

## 7. Percezione soggettiva (RPE, Feel)
- RPE e sRPE (RPE × minuti) sono metodo valido per carico interno. Incoerenza dati/percezione: FC bassa con RPE alto (o viceversa) = fatica, sonno, stress, malattia, caldo.
- In Intervals: `RPE` 1–10, `Feel` 1–5 (1 = ottimo, 5 = pessimo, **verificare** la scala nel profilo dell'atleta prima di interpretare).
- Correlare con wellness (`get_wellness_data`: HRV, FC a riposo, sonno).

## 8. Cadenza e falcata
- Cadenza media in Intervals per la corsa è spesso in "rpm" per gamba (es. 81 = ~162 spm). Confrontare a parità di ritmo, non in assoluto. Non c'è cadenza ideale universale: segnalare solo variazioni sistematiche.

## 9. Regole di commento (sintesi operativa)
1. Prima contesto: tipo seduta prevista dal piano (`training-plan.md`) vs eseguita.
2. Aderenza: ritmo, durata, recuperi, intensità vs target in % VC.
3. Interno vs esterno: FC, EF, decoupling (se valido), RPE/Feel.
4. Trend: confronto con ultime 3–4 corse dello stesso tipo dal DB locale.
5. Un solo giudizio chiaro + al massimo 1–2 azioni. Niente sovra-interpretazione di un dato singolo.
6. Dichiarare i dati mancanti (FC, streams, dislivello) e la loro incidenza sull'affidabilità.
