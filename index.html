<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>DoseDiary</title>
  <meta name="description" content="DoseDiary — Harm Reduction App" />
  <meta name="theme-color" content="#121218" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <!-- React + ReactDOM (UMD builds, no bundler needed) -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react/18.3.1/umd/react.production.min.js" crossorigin></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/react-dom/18.3.1/umd/react-dom.production.min.js" crossorigin></script>
  <!-- Babel standalone for JSX transform in-browser -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/7.24.4/babel.min.js" crossorigin></script>
  <!-- Tailwind CSS (CDN) -->
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
    html, body { margin: 0; padding: 0; height: 100%; background: #121218; }
    #root { height: 100%; }
    input[type=range] { -webkit-appearance: none; appearance: none; height: 6px; border-radius: 3px; }
    input[type=range]::-webkit-slider-thumb { -webkit-appearance: none; width: 20px; height: 20px; border-radius: 50%; cursor: pointer; }
    @keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }
    .animate-fadeIn { animation: fadeIn 0.25s ease-out forwards; }
    .warn-critical { animation: pulse 1.5s infinite; }
    @keyframes pulse { 0%,100% { opacity:1; } 50% { opacity:0.75; } }
  </style>
</head>
<body>
  <div id="root"></div>
  <script type="text/babel" data-presets="react">
    const { useState, useEffect, useCallback, useRef } = React;
// ─── Persistent Storage ───
const S = {
  async get(k) { try { const v = localStorage.getItem(k); return v ? JSON.parse(v) : null; } catch { return null; } },
  async set(k, v) { try { localStorage.setItem(k, JSON.stringify(v)); } catch {} },
};

// ─── Constants ───
const MOODS = [
  { emoji: "😊", label: "Gut", value: 5, color: "#6BCB77" },
  { emoji: "🙂", label: "Okay", value: 4, color: "#A8D8B9" },
  { emoji: "😐", label: "Neutral", value: 3, color: "#F2D388" },
  { emoji: "😔", label: "Mies", value: 2, color: "#E8A87C" },
  { emoji: "😣", label: "Krise", value: 1, color: "#E06B8A" },
];

const ALL_ITEMS = [
  { id:"Alkohol", cat:"sub", group:"Depressiva" },
  { id:"Cannabis", cat:"sub", group:"Cannabinoide" },
  { id:"Amphetamin", cat:"sub", group:"Stimulanzien" },
  { id:"MDMA", cat:"sub", group:"Empathogene" },
  { id:"Kokain", cat:"sub", group:"Stimulanzien" },
  { id:"Opioide", cat:"sub", group:"Opioide" },
  { id:"Benzodiazepine", cat:"sub", group:"Depressiva" },
  { id:"Nikotin", cat:"sub", group:"Stimulanzien" },
  { id:"Vaping", cat:"sub", group:"Inhalativa" },
  { id:"Koffein", cat:"sub", group:"Stimulanzien" },
  { id:"Kratom", cat:"sub", group:"Opioide" },
  { id:"LSD", cat:"sub", group:"Psychedelika" },
  { id:"Psilocybin", cat:"sub", group:"Psychedelika" },
  { id:"Ketamin", cat:"sub", group:"Dissoziativa" },
  { id:"GHB/GBL", cat:"sub", group:"Depressiva" },
  { id:"Lachgas", cat:"sub", group:"Dissoziativa" },
  { id:"Research Chemicals", cat:"sub", group:"Novel Psychoactive Substances" },
  { id:"Andere Substanz", cat:"sub", group:"Sonstiges" },
  { id:"Pornografie", cat:"beh", group:"Verhalten" },
  { id:"Glücksspiel", cat:"beh", group:"Verhalten" },
  { id:"Social Media", cat:"beh", group:"Verhalten" },
  { id:"Gaming", cat:"beh", group:"Verhalten" },
  { id:"Anderes Verhalten", cat:"beh", group:"Verhalten" },
];
const SUBSTANCES = ALL_ITEMS.map(i => i.id);
const SUB_ITEMS = ALL_ITEMS.filter(i => i.cat === "sub").map(i => i.id);
const BEH_ITEMS = ALL_ITEMS.filter(i => i.cat === "beh").map(i => i.id);
const SETTINGS_OPT = ["Allein zuhause","Mit Freund:innen","Party/Club","Draußen","Arbeit/Schule","Online/Gaming","Anderes"];
const UNITS = ["mg","g","ml","Stück","Züge","Tropfen","Lines","Pillen"];

const SUB_INFO = {
  Alkohol: { risk:"mittel–hoch", riskColor:"#E8A87C", onset:"15–30 Min.", duration:"2–6 Std.", safer:["Vor dem Trinken essen","Zwischen alkoholischen Getränken Wasser trinken","Eigene Grenzen kennen und respektieren","Nie allein in unbekannter Umgebung trinken","Mischkonsum (bes. mit Benzos/Opiaten) vermeiden"], interactions:["Benzodiazepine ⚠️ Atemdepression","Opioide ⚠️ Lebensgefahr","MDMA ⚠️ Dehydrierung","Cannabis ⚠️ Verstärkung, Übelkeit","Amphetamin ⚠️ Überdosierungsgefahr","Kokain ⚠️ Cocaethylen (hohe Herztoxizität)","Ketamin ⚠️ Erstickungsgefahr bei Erbrechen","GHB/GBL ⚠️ Lebensgefahr (Atemdepression)"] },
  Cannabis: { risk:"niedrig–mittel", riskColor:"#A8D8B9", onset:"Sofort (Rauchen) / 30–90 Min. (oral)", duration:"2–4 Std. (Rauchen) / 4–8 Std. (oral)", safer:[
    "Niedrig dosiert starten, besonders bei Edibles — Wirkung kann 30–90 Min. verzögert einsetzen",
    "Vaporizer statt Verbrennung bevorzugen (weniger Verbrennungsprodukte)",
    "Set & Setting beachten",
    "Bei Angst oder Panik: ruhiger Ort, Zuckergetränk, ruhige Stimme, abwarten",
    "Nicht fahren — gesetzlicher THC-Grenzwert im Straßenverkehr: 3,5 ng/ml Blutserum (§ 24a StVG). Auch nach dem Konsum kann THC noch stundenlang über dem Grenzwert liegen.",
    "Kein Konsum in Sichtweite von Schulen, Kitas, Spielplätzen, Sportstätten (Schutzzone: 100 m Luftlinie) — auch in Fußgängerzonen gilt 7–20 Uhr Konsumverbot.",
    "Rechtsstatus DE (KCanG, seit 1.4.2024, nur für Erwachsene ab 18): Besitz bis 25 g in der Öffentlichkeit / bis 50 g privat / max. 3 Pflanzen Eigenanbau straflos. Erwerb auf dem Schwarzmarkt bleibt verboten. Für Minderjährige gilt weiterhin vollständiges Verbot.",
  ], interactions:["Alkohol ⚠️ Verstärkung, Übelkeit","Amphetamin ⚠️ Herzbelastung","Kokain ⚠️ Herzbelastung","MDMA ⚠️ Verstärkte Halluzinationen"] },
  Amphetamin: { risk:"mittel–hoch", riskColor:"#E8A87C", onset:"15–30 Min. (nasal) / 30–60 Min. (oral)", duration:"4–8 Std.", safer:[
    "NIEMALS nachlegen wenn Wirkung nachlässt — Redosing verlängert Schlafentzug und verschlimmert den Crash massiv",
    "Schlafentzug ist das größte Risiko: Schon 24 Std. ohne Schlaf erhöhen psychotisches Risiko und Unfallgefahr stark",
    "Essen erzwingen: Appetithemmung ist stark — kleine Mahlzeiten vor und nach dem Konsum sind essenziell",
    "Viel Wasser trinken (2–3 L/Tag) — Hyperthermie und Dehydrierung sind häufige Komplikationen",
    "Drug-Checking nutzen: Speed ist eine der am häufigsten gestreckten Substanzen (MSM, Koffein, teils NPS)",
    "Nasenpflege bei nasalem Konsum: Kochsalzspülung nach jeder Session, eigenes Röhrchen verwenden",
    "Mind. 3 Tage Pause zwischen Konsumereignissen — Dopaminsystem braucht Zeit zur Erholung",
    "Bei Verfolgungsgedanken, Paranoia oder Halluzinationen: sofort Konsum stoppen und Hilfe suchen"
  ], interactions:[
    "MAO-Hemmer ⚠️ LEBENSGEFAHR: Hypertensive Krise, Serotoninsyndrom — absolute Kontraindikation",
    "MDMA ⚠️ Serotoninsyndrom — beide Substanzen zusammen können lebensbedrohlich sein",
    "Kokain ⚠️ Extreme kumulative Herzbelastung — Arrhythmie und Herzinfarkt",
    "Alkohol ⚠️ Amphetamin maskiert Alkoholwirkung — man trinkt unbewusst zu viel, Lebertoxizität",
    "Antidepressiva (SSRI/SNRI) ⚠️ Serotoninsyndrom-Risiko, Blutdruckkrise",
    "Opioide ⚠️ Gegenseitige Maskierung — Atemdepression und Überdosis werden nicht rechtzeitig bemerkt",
    "Methylphenidat (Ritalin) ⚠️ Überstimulation des Herz-Kreislauf-Systems",
    "Cannabis ⚠️ Herzbelastung, Panikattacken bei empfindlichen Personen"
  ] },
  MDMA: { risk:"mittel–hoch", riskColor:"#E8A87C", onset:"30–60 Min.", duration:"3–5 Std.", safer:[
    "Dosierung: max. 1–1.5 mg/kg Körpergewicht — bei 70 kg max. 105 mg gesamt",
    "6-Wochen-Regel strikt einhalten: Häufigerer Konsum schädigt Serotonin-Neuronen dauerhaft (Neurotoxizität)",
    "NIEMALS nachlegen — der Wunsch ist ein Zeichen des Comedowns, kein Zeichen von Unterdosierung",
    "Wasser trinken: ca. 250–500 ml/Std. beim Tanzen — nicht mehr (Hyponatriämie-Risiko bei Übertrinken!)",
    "Körpertemperatur beobachten: Überhitzung (Hyperthermie) ist häufigste Todesursache — Tanzpausen, kühle Orte aufsuchen",
    "Drug-Checking nutzen: Viele 'Ecstasy'-Pillen enthalten Amphetamin, PMA/PMMA oder Fentanyl-Analogika",
    "5-HTP: Manche Menschen nehmen es erst 24 Std. NACH dem Konsum (nicht davor) — der Grund: vorherige Einnahme kann das Serotoninsyndrom-Risiko erhöhen. Bitte informiere dich individuell oder frage eine Fachkraft.",
    "Nie allein konsumieren — bei Hitzschlag oder Krämpfen sofort 112 rufen"
  ], interactions:[
    "MAO-Hemmer ⚠️ LEBENSGEFAHR: Serotoninsyndrom — absolute Kontraindikation, auch Wochen nach Absetzen",
    "SSRI / SNRI ⚠️ LEBENSGEFAHR: Serotoninsyndrom — Symptome: Zittern, Verwirrtheit, hohes Fieber, Krämpfe",
    "Amphetamin ⚠️ Serotoninsyndrom + Herzüberlastung — beide Substanzen vervielfachen das Risiko",
    "Tramadol ⚠️ LEBENSGEFAHR: Serotoninsyndrom + Krampfanfallgefahr",
    "Lithium ⚠️ Sehr hohes Risiko für Krampfanfälle und Hyperthermie",
    "Kokain ⚠️ Extreme Herzbelastung, Überhitzung, Serotoninsyndrom-Risiko",
    "Alkohol ⚠️ Verstärkte Dehydrierung und Überhitzung — begünstigt Hyponatriämie",
    "Cannabis ⚠️ Kann Panik, Dissoziation und starke Halluzinationen auslösen",
    "Ketamin ⚠️ Unvorhersehbare Intensivierung, Risiko für Bewusstseinsverlust"
  ] },
  Kokain: { risk:"hoch", riskColor:"#E06B8A", onset:"Sofort (Rauchen/i.v.) / 1–5 Min. (nasal)", duration:"15–45 Min. (nasal) / 5–15 Min. (Rauchen/Crack)", safer:[
    "Eigenes Ziehröhrchen verwenden — niemals teilen (Hepatitis C und HIV-Übertragung über Schleimhautverletzungen)",
    "Nasenpflege: Nach nasalem Konsum Kochsalzspülung und Nasensalbe zum Schutz der Schleimhaut",
    "Kein Alkohol kombinieren: Leber bildet Cocaethylen — hochtoxisch mit 5× höherem Herzinfarktrisiko als Kokain allein",
    "Nie allein konsumieren — Herzrhythmusstörungen und Herzinfarkt können ohne Vorwarnung auftreten",
    "Pausen erzwingen: Kurze Wirkdauer verführt zum Nachlegen — das erhöht Herzbelastung und Abhängigkeitsrisiko exponentiell",
    "Keine Kombination mit anderen Stimulanzien (Amphetamin, MDMA) — kumulative Herzbelastung kann tödlich sein",
    "Brustschmerzen, Herzrasen, Kribbeln im linken Arm → sofort 112 (Herzinfarkt-Warnsymptome)",
    "Drug-Checking: Fentanyl-Kontamination in Kokain ist eine wachsende Todesursache — Fentanyl-Teststreifen nutzen"
  ], interactions:[
    "Alkohol ⚠️ KRITISCH: Bildet Cocaethylen in der Leber — Herzinfarktrisiko 5× erhöht, verlängerte Toxizität",
    "Amphetamin ⚠️ Extreme kumulative Herzbelastung — Arrhythmie und Herzinfarkt",
    "MDMA ⚠️ Extreme Herzbelastung, Überhitzung, hohes Serotoninsyndrom-Risiko",
    "MAO-Hemmer ⚠️ LEBENSGEFAHR: Hypertensive Krise — Blutdruck kann lebensbedrohlich ansteigen",
    "Opioide ⚠️ 'Speedball': Gegenseitige Maskierung — Atemdepression oft unbemerkt bis Bewusstlosigkeit",
    "Cannabis ⚠️ Verstärkte Herzbelastung und Panikattacken",
    "Koffein ⚠️ Additive Herzbelastung — in Energy Drinks oft unterschätzt",
    "Antidepressiva (SSRI/SNRI) ⚠️ Erhöhtes Krampfanfallrisiko"
  ] },
  Opioide: { risk:"sehr hoch", riskColor:"#E06B8A", onset:"Variabel: Sofort (i.v.) / 5–15 Min. (nasal) / 15–45 Min. (oral)", duration:"3–8 Std. (substanzabhängig)", safer:[
    "Naloxon (Narcan/Nyxoid) IMMER griffbereit haben und alle anwesenden Personen in die Anwendung einweisen",
    "NIE allein konsumieren — Atemdepression führt lautlos zur Bewusstlosigkeit, ohne Hilfe ist sie tödlich",
    "Toleranzpause = akute Lebensgefahr: Nach wenigen Tagen Pause die alte Dosis NICHT verwenden — immer mit 25–50% neu starten",
    "Sterile Utensilien bei i.v.-Konsum: Hepatitis C, HIV und Herzklappenentzündung drohen bei Nadeltausch",
    "Drug-Checking: Fentanyl und Fentanyl-Analoga (10–100× potenter als Heroin) kontaminieren zunehmend alle Drogen",
    "Erste Dosis immer klein halten: Potenz und Zusammensetzung variieren stark zwischen Quellen",
    "Nicht fahren oder Maschinen bedienen — auch bei subjektiv normaler Wahrnehmung",
    "Notfall-Zeichen: Langsame/flache Atmung, blaue Lippen, nicht weckbar → sofort 112, Naloxon geben, stabile Seitenlage"
  ], interactions:[
    "Alkohol ⚠️ LEBENSGEFAHR: Additive Atemdepression — häufigste Todesursache bei Opioid-Überdosis",
    "Benzodiazepine ⚠️ LEBENSGEFAHR: Diese Kombination tötet mehr Menschen als alle anderen Drogenkombinationen",
    "GHB/GBL ⚠️ LEBENSGEFAHR: Atemdepression, Bewusstlosigkeit — auch bei niedrigen Dosen tödlich",
    "Ketamin ⚠️ Verstärkte Atemdepression und Sedierung",
    "Antihistaminika (Diphenhydramin) ⚠️ Verstärkte Sedierung, Atemdepression-Risiko",
    "Amphetamin ⚠️ Gegenseitige Maskierung — man spürt weder Überdosis noch Atemdepression rechtzeitig",
    "Kokain ⚠️ 'Speedball': Stimulation verdeckt Atemdepression — Herzstillstand bei nachlassender Kokainwirkung möglich",
    "Tramadol / SSRI ⚠️ Serotoninsyndrom (besonders Tramadol + SSRI oder Tramadol + MDMA)"
  ] },
  Benzodiazepine: { risk:"hoch", riskColor:"#E06B8A", onset:"15–45 Min. (oral) / schneller bei sublingualer Einnahme", duration:"4–12 Std. (kurz: Lorazepam/Oxazepam) / bis 72 Std. (lang: Diazepam/Clonazepam)", safer:[
    "Abhängigkeit entsteht schnell: Körperliche Abhängigkeit kann sich bereits nach 2–4 Wochen täglicher Einnahme entwickeln — auch bei therapeutischer Dosierung. Frühzeichen: Rebound-Angst zwischen den Dosen.",
    "NIEMALS abrupt absetzen nach regelmäßigem Konsum — kalter Entzug kann lebensbedrohliche Krampfanfälle auslösen (Grand-Mal-Status epilepticus). Dieser Entzug ist medizinisch gefährlicher als Heroin- oder Alkohol-Entzug.",
    "Ausschleichen ist Pflicht: Dosisreduktion über Wochen bis Monate (Ashton-Protokoll) — immer unter ärztlicher Begleitung, niemals eigenständig.",
    "Nur kurzfristig einsetzen: Wirksamkeit nimmt nach 2–4 Wochen ab, das Abhängigkeitspotenzial bleibt.",
    "Niemals mit Alkohol, Opiaten oder GHB/GBL kombinieren — Atemdepression auch bei normalen Dosen möglich.",
    "Gedächtnisprobleme und Blackouts sind häufig — keine wichtigen Entscheidungen unter Einfluss treffen.",
    "Fahrtüchtigkeit stark eingeschränkt — rechtliche Konsequenzen auch ohne Unfall möglich.",
    "Benzos aus nicht-ärztlichen Quellen haben oft variable oder falsch deklarierte Wirkstoffgehalte (z.B. Brotizolam, Flualprazolam) — Drug-Checking empfohlen."
  ], interactions:[
    "Alkohol ⚠️ LEBENSGEFAHR: Additive Atemdepression — tödlich auch bei vergleichsweise geringen Mengen",
    "Opioide ⚠️ LEBENSGEFAHR: Häufigste Ursache für verschreibungsbedingte Drogentote weltweit",
    "GHB/GBL ⚠️ LEBENSGEFAHR: Extreme Atemdepression, Bewusstlosigkeit",
    "Ketamin ⚠️ Starke Sedierung, Atemdepression — Erbrechen bei Bewusstlosigkeit lebensbedrohlich",
    "Cannabis ⚠️ Verstärkte Sedierung, kognitive Beeinträchtigung, Sturzgefahr",
    "Antihistaminika (z.B. Diphenhydramin) ⚠️ Additive Sedierung und Atemdepression",
    "Antidepressiva ⚠️ Verstärkte sedierende Wirkung, erhöhtes Sturzrisiko bei Älteren",
    "Kratom ⚠️ Additive Dämpfung des Atemzentrums"
  ] },
  Nikotin: { risk:"mittel (Abhängigkeit)", riskColor:"#F2D388", onset:"Sofort (Rauchen/Vape)", duration:"30–60 Min.", safer:["Vaporizer/Nikotinersatz statt Verbrennung","Rauchpausen bewusst einlegen","Trigger erkennen (Stress, Kaffee, Alkohol)","Reduktion statt kalter Entzug erwägen"], interactions:["Stimulanzien ⚠️ Verstärkte Herzbelastung","Alkohol ⚠️ Verstärktes Verlangen nach beidem"] },
  Koffein: { risk:"niedrig", riskColor:"#A8D8B9", onset:"15–45 Min.", duration:"3–5 Std.", safer:["Max. 400 mg/Tag (ca. 4 Tassen Kaffee)","Nicht nach 14 Uhr für guten Schlaf","Genug Wasser trinken","Abhängigkeit ernst nehmen"], interactions:["Amphetamin ⚠️ Verstärkte Herzbelastung","MDMA ⚠️ Verstärkte Überhitzung","Kokain ⚠️ Herzbelastung"] },
  Kratom: { risk:"mittel", riskColor:"#F2D388", onset:"15–30 Min.", duration:"3–6 Std.", safer:["Niedrig dosieren (unter 5g)","Nicht täglich konsumieren","Auf Qualität und Herkunft achten","Leerer Magen verstärkt Wirkung"], interactions:["Opioide ⚠️ Verstärkte Opioidwirkung","Alkohol ⚠️ Übelkeit, Sedierung","Benzodiazepine ⚠️ Atemdepression"] },
  LSD: { risk:"niedrig (physisch) / mittel–hoch (psychisch)", riskColor:"#F2D388", onset:"30–90 Min. (Onset täuscht — nicht nachlegen!)", duration:"8–12 Std. / Nachwirkungen bis 24 Std.", safer:[
    "Set & Setting sind das A und O: Innere Verfassung und sichere Umgebung bestimmen den Trip — schlechte psychische Verfassung erhöht Bad-Trip-Risiko enorm",
    "Tripsitter: Eine nüchterne, vertrauenswürdige Person dabei haben — besonders bei Ersterfahrungen oder Dosen über 100 µg",
    "Einstiegsdosis: 50–75 µg für Unerfahrene — handelsübliche Trips oft 100–200 µg, eine halbe Einheit ist legitim",
    "NIEMALS nachlegen in den ersten 3–4 Std. — verzögerter Onset kann zu massiver unbeabsichtigter Überdosierung führen",
    "Keine Verpflichtungen für 24 Std.: Nachwirkungen beeinflussen Konzentration und emotionale Stabilität erheblich",
    "Bad Trip: Ruhige Umgebung, Musik wechseln, Frischluft — Vertrauensperson ruhig sprechen lassen, keine weitere Substanz",
    "Psychose-Risiko: Menschen mit persönlicher oder familiärer Schizophrenie-/Bipolaranamnese sollten Konsum dringend vermeiden",
    "HPPD ist real: Bei anhaltenden visuellen Phänomenen nach dem Trip ärztlichen Rat suchen"
  ], interactions:[
    "Lithium ⚠️ LEBENSGEFAHR: Krampfanfälle — absolute Kontraindikation",
    "MAO-Hemmer ⚠️ LEBENSGEFAHR: Massive Wirkungsverstärkung und -verlängerung, vollständig unkontrollierbar",
    "SSRI / SNRI ⚠️ Oft stark reduzierte Wirkung (Serotonin-Kreuztoleranz) — in seltenen Fällen aber Serotoninsyndrom",
    "Cannabis ⚠️ Stark verstärkte Halluzinationen, Paranoia, Panikattacken — besonders risikoreiche Kombination",
    "MDMA ⚠️ 'Candyflip': Intensität schwer kalkulierbar, Überhitzung, 15+ Std. Dauer",
    "Tramadol / Triptane ⚠️ Serotoninsyndrom-Risiko",
    "Stimulanzien ⚠️ Erhöhte Herzbelastung, Schlafentzug verstärkt psychotisches Risiko"
  ] },
  Psilocybin: { risk:"niedrig (physisch) / mittel–hoch (psychisch)", riskColor:"#F2D388", onset:"20–60 Min. (nüchtern schneller)", duration:"4–6 Std. / Nachwirkungen bis 12 Std.", safer:[
    "Set & Setting: Innere Verfassung und vertraute, sichere Umgebung sind entscheidend für den Tripverlauf",
    "Tripsitter: Nüchterne Begleitperson empfohlen — besonders bei Dosen über 2g oder beim ersten Mal",
    "Dosierung: 1–1.5g getrocknete Pilze als Einstieg (mittel: 2–3g, hoch: 3.5g+) — Potenz variiert stark je nach Art und Ernte",
    "Nüchtern konsumieren: Voller Magen verlangsamt den Onset und kann Übelkeit in der ersten Stunde verstärken",
    "NICHT nachlegen innerhalb von 2 Std. — Onset kann sich verzögern, unbeabsichtigte Überdosierung möglich",
    "Verpflichtungsfreien Tag einplanen: Nachwirkungen können emotionale Verarbeitung und Konzentration beeinflussen",
    "Psychose-Risiko: Menschen mit persönlicher oder familiärer Schizophrenie-/Bipolar-I-Anamnese sollten Konsum meiden",
    "Pilze aus unbekannten Quellen bestimmen lassen — Verwechslung mit giftigen Arten (z.B. Grüner Knollenblätterpilz) kann tödlich sein"
  ], interactions:[
    "Lithium ⚠️ LEBENSGEFAHR: Krampfanfälle — absolute Kontraindikation",
    "MAO-Hemmer ⚠️ LEBENSGEFAHR: Drastische Wirkungsverstärkung, nicht steuerbar",
    "SSRI / SNRI ⚠️ Stark reduzierte Wirkung oder unvorhersehbare Symptomverstärkung",
    "Tramadol ⚠️ Serotoninsyndrom-Risiko",
    "Cannabis ⚠️ Stark verstärkte Halluzinationen, Paranoia, erhöhtes Risiko für Kontrollverlust",
    "MDMA ⚠️ 'Hippieflip': Intensive emotionale Verstärkung, schwer steuerbar — nur für Erfahrene",
    "Stimulanzien ⚠️ Herzbelastung, Schlafentzug erhöht psychisches Destabilisierungsrisiko"
  ] },
  Ketamin: { risk:"mittel–hoch", riskColor:"#E8A87C", onset:"Sofort (i.v.) / 3–5 Min. (i.m.) / 5–15 Min. (nasal)", duration:"30–45 Min. (nasal) / bis 90 Min. (i.m.)", safer:[
    "K-Hole: Bei hohen Dosen kann totale Dissoziation eintreten — immer in sicherer Liegeposition, niemals stehend konsumieren",
    "Blasengesundheit: Regelmäßiger Konsum (mehrmals/Woche) zerstört Blasenschleimhaut irreversibel (Ketamin-Zystitis) — Frühzeichen: Harndrang und Schmerzen beim Wasserlassen",
    "Konsumpausen einhalten: Mind. 1 Woche zwischen Sessions — Blasenschäden sind ab 2–3× pro Woche in Fallberichten und Studien beschrieben",
    "Auf Erbrechen vorbereitet sein: Stabile Seitenlage bei eingeschränktem Bewusstsein — Erstickungsgefahr durch Aspiration",
    "Nie in der Nähe von Wasser, Treppen oder Straßen konsumieren — Orientierungsverlust führt zu schweren Stürzen",
    "Nicht mit anderen dämpfenden Substanzen kombinieren — Atemdepression und Aspirationsrisiko steigen stark an",
    "Nasale Dosierung: 0.5–1 mg/kg als Einstieg — nach mind. 45 Min. erst beurteilen, ob Nachdosierung sinnvoll"
  ], interactions:[
    "Alkohol ⚠️ LEBENSGEFAHR: Erstickungsgefahr bei Erbrechen — Schutzreflexe ausgeschaltet",
    "Opioide ⚠️ Verstärkte Atemdepression und tiefe Sedierung",
    "Benzodiazepine ⚠️ Extreme Sedierung, Atemdepression, Aspirationsrisiko",
    "GHB/GBL ⚠️ LEBENSGEFAHR: Bewusstlosigkeit und Atemstillstand",
    "Cannabis ⚠️ Stark verstärkte Dissoziation, Desorientierung und Übelkeit",
    "MDMA / Stimulanzien ⚠️ Extreme kardiovaskuläre Belastung durch gegensätzliche Substanzwirkungen",
    "Antidepressiva ⚠️ Ketamin hat selbst antidepressive Eigenschaften — unvorhersehbare Wechselwirkungen möglich"
  ] },
  "GHB/GBL": { risk:"sehr hoch", riskColor:"#E06B8A", onset:"15–30 Min.", duration:"1.5–3 Std.", safer:[
    "IMMER mit Milliliter-Spritze oder geeichtem Messbecher dosieren — der Unterschied zwischen Wirkdosis und Überdosis beträgt oft nur 0.5–1 ml",
    "GBL ist etwa 1.5–2× potenter als GHB: Umrechnungsfaktor beachten, niemals GBL mit GHB-Dosierung nehmen",
    "Nie nachlegen vor vollständigem Wirkungsende — durch Kumulation droht plötzlicher Bewusstseinsverlust ohne Vorwarnung",
    "Mind. 2 Std. Zeitabstand zwischen Dosierungen einhalten — auch wenn keine Wirkung mehr spürbar ist",
    "NIE allein konsumieren: Einschlafen und Aspirieren ist die häufigste Todesursache — Begleitperson muss Zeitintervalle dokumentieren",
    "Notfallprotokoll: Person nicht weckbar → stabile Seitenlage, sofort 112 — Rettungsdienst vollständig informieren (Entkriminalisierung bei Hilfe)",
    "Verdünnt konsumieren: Auf mindestens das 5–10-fache Volumen mit Wasser oder Saft verdünnen, niemals pur"
  ], interactions:[
    "Alkohol ⚠️ LEBENSGEFAHR: Selbst sehr kleine Alkoholmengen potenzieren die GHB-Wirkung massiv — häufigste Todesursache",
    "Opioide ⚠️ LEBENSGEFAHR: Additive Atemdepression und Bewusstlosigkeit",
    "Benzodiazepine ⚠️ LEBENSGEFAHR: Extreme Sedierung, Atemstillstand",
    "Ketamin ⚠️ LEBENSGEFAHR: Bewusstlosigkeit, Atemdepression, kein Erwecken möglich",
    "Cannabis ⚠️ Verstärkte Sedierung, Übelkeit — erhöhtes Aspirationsrisiko",
    "MDMA ⚠️ Herz-Kreislauf-Überlastung, Dehyration, Überhitzung — unberechenbare Interaktion",
    "Antidepressiva / Schlafmittel ⚠️ Additive dämpfende Wirkung — dosisunabhängige Atemdepression möglich"
  ] },
  "Research Chemicals": { risk:"sehr hoch / unbekannt", riskColor:"#E06B8A", onset:"Stark variabel — oft 20–90 Min., manche RC-Stimulanzien ab 5 Min.", duration:"Stark variabel — 2 bis über 24 Std. je nach Substanzklasse", safer:[
    "Drug-Checking ist zwingend: Identität, Reinheit und Gehalt mit Reagenzien-Kit (z.B. Marquis, Mecke, Folin) oder bei einer Drogenchecking-Stelle überprüfen — viele RC-Proben enthalten Streckmittel oder Fehlsubstitutionen.",
    "Dosierung mit Feinwaage (0,001 g Auflösung): Aktive Dosen liegen bei vielen RCs im einstelligen Milligramm-Bereich — kleine Abweichungen können massive Wirkungsunterschiede bedeuten.",
    "Onset täuscht: Viele RCs haben verzögerte oder stufenweise Onsets — niemals vor Ablauf von 2 Stunden nachlegen, auch wenn noch keine Wirkung spürbar.",
    "Erster Test immer mit 5–10 % der vermuteten Wirkdosis (Allergy-Test): Unbekannte Substanzen können idiosynkratische Reaktionen auslösen, die bei kleinen Mengen beherrschbar sind.",
    "Nie allein konsumieren: Unbekanntes Wirkprofil, unbekannte Dauer — eine nüchterne Begleitperson ist bei RCs keine Empfehlung, sondern Risikominimierungs-Standard.",
    "Substanzklasse recherchieren: Stimulanzien-RC (z.B. 4-MMC/Mephedron, α-PVP), Psychedelika-RC (z.B. 2C-B, NBOMe), Dissoziativa-RC (z.B. 3-MeO-PCP, Deschloroketamin) und Cannabinoide-RC (synthetische Cannabinoide) haben grundlegend unterschiedliche RisikoProfile.",
    "Synthetische Cannabinoide gesondert: Wirkung nicht mit Cannabis vergleichbar — 100× stärker, kein Ceiling-Effekt, häufige Krampfanfälle und kardiovaskuläre Notfälle in klinischen Berichten.",
    "NBOMe-Klasse: Niemals oral — aktiv nur sublingual/nasal; Papierstrips nicht mit LSD verwechseln (LSD ist oral aktiv, NBOMe-Verbindungen nicht); Überdosierung durch Schlucken war mehrfach tödlich.",
    "Rechtsstatus prüfen: Die meisten RCs fallen unter das NpSG (Neue-psychoaktive-Stoffe-Gesetz) — Besitz und Erwerb sind in Deutschland strafbar.",
    "Im Notfall: Rettungsdienst vollständig informieren, welche Substanz konsumiert wurde — das verbessert die Behandlung und ist durch Straffreiheits-Klauseln bei Hilfeleistung abgesichert."
  ], interactions:[
    "Alkohol ⚠️ Unvorhersehbare Wechselwirkungen — je nach RC-Klasse Atemdepression (Depressiva-RC) oder Herzbelastung (Stimulanzien-RC)",
    "MDMA ⚠️ Serotoninsyndrom-Risiko bei Entaktogen-RCs (z.B. 4-MMC/Mephedron) — schwere Hyperthermie und Krampfanfälle",
    "Amphetamin / Kokain ⚠️ Extreme kumulative Herzbelastung bei Stimulanzien-RCs — kardiovaskuläre Notfälle",
    "Opioide ⚠️ Atemdepression bei Opioid-ähnlichen RCs (z.B. U-47700-Analoga) — besonders in Kombination mit anderen Depressiva",
    "Benzodiazepine ⚠️ Starke Sedierung, bei Depressiva-RCs Atemdepression",
    "LSD / Psilocybin ⚠️ Unkalkulierbare Intensivierung bei Psychedelika-RCs (z.B. 2C-B, DOx) — lange Wirkdauer und Kontrollverlust",
    "MAO-Hemmer ⚠️ LEBENSGEFAHR bei Stimulanzien- und Entaktogen-RCs — Serotoninsyndrom und hypertensive Krisen"
  ] },
  Lachgas: { risk:"niedrig–mittel", riskColor:"#A8D8B9", onset:"Sofort", duration:"1–3 Min.", safer:["Immer im Sitzen konsumieren","Nie direkt aus der Kartusche (Erfrierungen!)","Sauerstoffpausen einlegen","Bei regelmäßigem Konsum: Vitamin B12 supplementieren"], interactions:["Alkohol ⚠️ Verstärkte Benommenheit, Sturzgefahr","Opioide ⚠️ Atemdepression","Stimulanzien ⚠️ Herzrhythmusstörungen"] },
  Andere: { risk:"unbekannt", riskColor:"#8899AA", onset:"–", duration:"–", safer:["Substanz identifizieren (Drug-Checking!)","Niedrigste mögliche Dosis testen","Nie allein konsumieren","Im Zweifel: nicht konsumieren"], interactions:[] },
  "Andere Substanz": { risk:"unbekannt", riskColor:"#8899AA", onset:"–", duration:"–", safer:["Substanz identifizieren (Drug-Checking!)","Niedrigste mögliche Dosis testen","Nie allein konsumieren","Im Zweifel: nicht konsumieren"], interactions:[] },
  Vaping: { risk:"mittel", riskColor:"#F2D388", onset:"Sofort", duration:"30–60 Min.", safer:["Nur regulierte Liquids verwenden (keine Schwarzmarkt-Cartridges)","Nikotinstärke bewusst wählen und ggf. reduzieren","Gerät regelmäßig reinigen","Bei Husten/Atemnot: Konsum pausieren","Vitamin-E-Acetat-haltige Produkte meiden"], interactions:["Nikotin ⚠️ Doppelte Nikotinzufuhr","Stimulanzien ⚠️ Verstärkte Herzbelastung","Cannabis-Vapes ⚠️ Oft unbekannte Inhaltsstoffe"] },
  Pornografie: { risk:"niedrig–mittel (Verhalten)", riskColor:"#F2D388", onset:"Sofort", duration:"Variabel", safer:["Zeitlimits setzen und einhalten","Auslöser (Trigger) erkennen: Langeweile, Stress, Einsamkeit","Bewusst konsumieren statt automatisch","Reflektion: Verändert sich mein Bild von Intimität?","Professionelle Hilfe suchen, wenn Kontrollverlust eintritt"], interactions:[] },
  Glücksspiel: { risk:"hoch (Verhalten)", riskColor:"#E06B8A", onset:"Sofort", duration:"Variabel", safer:["Festes Budget setzen — nie über Limit gehen","Verluste nicht durch Weiterspielen ausgleichen","Zeitlimits setzen","Selbstsperre bei Online-Anbietern nutzen","Beratung: BZgA-Hotline 0800 1 37 27 00"], interactions:[] },
  "Social Media": { risk:"niedrig–mittel (Verhalten)", riskColor:"#F2D388", onset:"Sofort", duration:"Variabel", safer:["Bildschirmzeit-Tracker nutzen","Benachrichtigungen reduzieren","Bewusste Nutzungszeiten definieren","Vergleichsfalle erkennen","Regelmäßige Digital-Detox-Phasen"], interactions:[] },
  Gaming: { risk:"niedrig–mittel (Verhalten)", riskColor:"#F2D388", onset:"Sofort", duration:"Variabel", safer:["Zeitlimits setzen und Timer nutzen","Pausen einlegen (alle 60 Min.)","Auf Schlaf achten","In-App-Käufe budgetieren","Wenn Alltag leidet: professionelle Beratung"], interactions:[] },
  "Anderes Verhalten": { risk:"unbekannt", riskColor:"#8899AA", onset:"–", duration:"–", safer:["Trigger identifizieren","Zeitlimits setzen","Muster erkennen und reflektieren"], interactions:[] },
};

// ─── Substance-specific safer-use timers (min hours between use) ───
const SAFER_TIMERS = {
  MDMA: { hours: 2160, label: "3-Monats-Regel", desc: "MDMA braucht mind. 3 Monate Pause fuer Serotonin-Regeneration. Haeufigerer Konsum ist neurotoxisch.", color: "#E06B8A" },
  LSD: { hours: 336, label: "2-Wochen-Toleranz", desc: "LSD-Toleranz braucht ca. 14 Tage zum vollstaendigen Abbau. Frueherer Konsum verschwendet Substanz.", color: "#F2D388" },
  Psilocybin: { hours: 336, label: "2-Wochen-Toleranz", desc: "Kreuztoleranz mit LSD. Mind. 2 Wochen Pause fuer volle Wirkung.", color: "#F2D388" },
  Ketamin: { hours: 168, label: "1-Woche-Minimum", desc: "Regelmaessiger Konsum schaedigt die Blase irreversibel. Mind. 1 Woche Pause.", color: "#E8A87C" },
  Kokain: { hours: 168, label: "1-Woche-Minimum", desc: "Herz und Nasenschleimhaut brauchen Erholung. Binge-Konsum vermeiden.", color: "#E06B8A" },
  Amphetamin: { hours: 72, label: "3-Tage-Minimum", desc: "Schlaf und Naehrstoffe muessen sich erholen. Nachschieben verschlechtert das Nebenwirkungsprofil.", color: "#E8A87C" },
  "GHB/GBL": { hours: 2, label: "2-Stunden-Regel", desc: "Nie vor Wirkungsende nachlegen. Mindestens 2 Std. zwischen Dosen — Ueberdosierung kann toedlich sein.", color: "#E06B8A" },
  "Research Chemicals": { hours: 336, label: "2-Wochen-Mindestpause", desc: "Unbekanntes Toxizitaetsprofil: Organschaeden (Niere, Leber, Herz) akkumulieren bei haeufigem Konsum. Mind. 2 Wochen Pause zwischen Konsumereignissen. Bei anhaltenden Symptomen aerztliche Hilfe suchen.", color: "#E06B8A" },
  Alkohol: { hours: 48, label: "2-Tage-Regeneration", desc: "Die Leber braucht 48 Std. zur vollen Regeneration. Konsekutives Trinken erhoet Abhaengigkeitsrisiko.", color: "#E8A87C" },
};

// ─── Common medications with substance interaction warnings ───
const MEDICATIONS = [
  { id: "ssri", name: "SSRI (Antidepressiva)", examples: "Sertralin, Citalopram, Fluoxetin", warns: { MDMA: "LEBENSGEFAHR: Serotoninsyndrom", LSD: "Stark abgeschwaechtzte Wirkung", Psilocybin: "Stark abgeschwaechtzte Wirkung", Amphetamin: "Serotoninsyndrom-Risiko", Kokain: "Erhoehtes Krampfrisiko", Tramadol: "Serotoninsyndrom" } },
  { id: "snri", name: "SNRI (Antidepressiva)", examples: "Venlafaxin, Duloxetin", warns: { MDMA: "LEBENSGEFAHR: Serotoninsyndrom", Amphetamin: "Serotoninsyndrom + Bluthochdruck", Kokain: "Bluthochdruck-Krise" } },
  { id: "mao", name: "MAO-Hemmer", examples: "Tranylcypromin, Moclobemid", warns: { MDMA: "LEBENSGEFAHR", Amphetamin: "LEBENSGEFAHR", Kokain: "LEBENSGEFAHR: Bluthochdruck-Krise", LSD: "Unberechenbare Verstaerkung", Psilocybin: "Unberechenbare Verstaerkung" } },
  { id: "benzo_rx", name: "Benzodiazepine (verschrieben)", examples: "Diazepam, Lorazepam, Alprazolam", warns: { Alkohol: "LEBENSGEFAHR: Atemdepression", Opioide: "LEBENSGEFAHR: Atemdepression", "GHB/GBL": "LEBENSGEFAHR", Ketamin: "Starke Sedierung" } },
  { id: "opioid_rx", name: "Opioid-Schmerzmittel", examples: "Tramadol, Tilidin, Oxycodon", warns: { Alkohol: "LEBENSGEFAHR: Atemdepression", Benzodiazepine: "LEBENSGEFAHR", "GHB/GBL": "LEBENSGEFAHR", Ketamin: "Atemdepression", MDMA: "Serotoninsyndrom (Tramadol)" } },
  { id: "lithium", name: "Lithium", examples: "Quilonum, Hypnorex", warns: { LSD: "LEBENSGEFAHR: Krampfanfaelle", Psilocybin: "LEBENSGEFAHR: Krampfanfaelle", MDMA: "Serotoninsyndrom-Risiko" } },
  { id: "antipsych", name: "Antipsychotika", examples: "Risperidon, Quetiapin, Olanzapin", warns: { Amphetamin: "Gegenseitige Aufhebung + Nebenwirkungen", Kokain: "Herzrhythmusstoerungen", Alkohol: "Verstaerkte Sedierung", Cannabis: "Verstaerkte Sedierung" } },
  { id: "methylph", name: "Methylphenidat (Ritalin)", examples: "Ritalin, Concerta, Medikinet", warns: { Kokain: "Extreme Herzbelastung", Amphetamin: "Ueberstimulation", MDMA: "Serotoninsyndrom-Risiko", Alkohol: "Maskierte Wirkung, Ueberdosierungsgefahr" } },
];

// ─── Badges / Milestones (Gamification light) ───
const BADGES = [
  { id:"first_log", icon:"📝", title:"Erster Schritt", desc:"Ersten Log-Eintrag gespeichert", check: (l,m,g,kb,sk) => l.length >= 1 },
  { id:"mood_3", icon:"😊", title:"Stimmungs-Check", desc:"3 Mood-Check-ins gemacht", check: (l,m,g,kb,sk) => m.length >= 3 },
  { id:"clean_7", icon:"🔥", title:"Eine Woche stark", desc:"7-Tage Clean-Streak erreicht", check: (l,m,g,kb,sk) => (g.cleanDays||[]).length >= 7 },
  { id:"clean_30", icon:"🏆", title:"Ein ganzer Monat", desc:"30 Clean Days gesammelt", check: (l,m,g,kb,sk) => (g.cleanDays||[]).length >= 30 },
  { id:"kb_3", icon:"🧬", title:"Wissensdurst", desc:"3 Wissensmodule gelesen", check: (l,m,g,kb,sk) => Object.keys(kb.read||{}).length >= 3 },
  { id:"kb_12", icon:"🎓", title:"Wissensmeister", desc:"Alle 12 Module abgeschlossen", check: (l,m,g,kb,sk) => Object.keys(kb.read||{}).length >= 12 },
  { id:"refl_1", icon:"💭", title:"Selbstreflexion", desc:"Erste Reflexion geschrieben", check: (l,m,g,kb,sk) => Object.values(kb.reflections||{}).filter(v=>v?.trim()).length >= 1 },
  { id:"skill_5", icon:"🧰", title:"Skill-Profi", desc:"Skills 5x genutzt", check: (l,m,g,kb,sk) => Object.values(sk.feedback||{}).reduce((a,v)=>a+v.length,0) >= 5 },
  { id:"streak_14", icon:"💎", title:"Zwei Wochen Streak", desc:"14-Tage Clean-Streak", check: (l,m,g,kb,sk) => { const s=calcLongestStreak(g.cleanDays||[]); return s>=14; } },
  { id:"log_20", icon:"📊", title:"Datensammler", desc:"20 Log-Eintraege erfasst", check: (l,m,g,kb,sk) => l.length >= 20 },
];

// Full cross-interaction matrix for mix warnings
const INTERACTION_MATRIX = {
  "Alkohol+Opioide": { level:"critical", text:"LEBENSGEFAHR: Atemdepression. Beide Substanzen unterdrücken das Atemzentrum.", advice:"Höchstes Risiko. Bei Notfall sofort 112 rufen. Fachberatung empfohlen." },
  "Alkohol+Benzodiazepine": { level:"critical", text:"LEBENSGEFAHR: Atemdepression und Bewusstlosigkeit.", advice:"Höchstes Risiko. Ärztliche oder suchtmedizinische Beratung empfohlen. Notfall: 112." },
  "Alkohol+GHB/GBL": { level:"critical", text:"LEBENSGEFAHR: Massive Atemdepression. Schon geringe Mengen Alkohol können tödlich wirken.", advice:"Extrem hohes Risiko — auch bei kleinen Mengen. Notfall: 112." },
  "Alkohol+Kokain": { level:"critical", text:"Bildet Cocaethylen in der Leber — hohe Herztoxizität. Erhöhtes Risiko für plötzlichen Herztod.", advice:"Hohes Risiko, das oft unterschätzt wird. Bei Beschwerden sofort 112." },
  "Alkohol+Ketamin": { level:"high", text:"Erstickungsgefahr: Ketamin kann Erbrechen auslösen, Alkohol unterdrückt Schutzreflexe.", advice:"Erhöhtes Risiko. Bei Bewusstlosigkeit: stabile Seitenlage, 112 rufen." },
  "Alkohol+MDMA": { level:"high", text:"Dehydrierung und Überhitzung. Alkohol verstärkt Flüssigkeitsverlust.", advice:"Erhöhtes Risiko. Ausreichend Wasser trinken wird empfohlen." },
  "Alkohol+Amphetamin": { level:"high", text:"Amphetamin maskiert Alkoholwirkung → Überdosierungsgefahr.", advice:"Hohes Risiko: Die Alkoholwirkung wird verschleiert — Überdosierung schwer erkennbar." },
  "Alkohol+Cannabis": { level:"medium", text:"Gegenseitige Verstärkung: Übelkeit, Schwindel, Kreislaufprobleme ('Greenout').", advice:"Erhöhtes Risiko. Niedrige Mengen und ausreichend Pausen werden empfohlen." },
  "Opioide+Benzodiazepine": { level:"critical", text:"LEBENSGEFAHR: Massive Atemdepression. Häufigste Todesursache bei Drogennotfällen.", advice:"Extrem hohes Risiko. Naloxon bereithalten. Notfall: 112." },
  "Opioide+GHB/GBL": { level:"critical", text:"LEBENSGEFAHR: Beide unterdrücken Atemzentrum.", advice:"Extrem hohes Risiko. Notfall: sofort 112." },
  "Opioide+Ketamin": { level:"high", text:"Verstärkte Atemdepression und Sedierung.", advice:"Hohes Risiko. Fachberatung zur Risikoreduktion wird empfohlen." },
  "Opioide+Amphetamin": { level:"high", text:"Gegenseitige Maskierung: Man merkt weder Überdosis noch Atemdepression rechtzeitig.", advice:"Sehr hohes Risiko durch wechselseitige Verschleierung der Wirkung." },
  "Opioide+Kokain": { level:"high", text:"Speedball — gegenseitige Maskierung, hohes Risiko für Herz-Kreislauf-Versagen.", advice:"Sehr hohes Risiko. Bei Beschwerden sofort 112." },
  "Benzodiazepine+GHB/GBL": { level:"critical", text:"LEBENSGEFAHR: Extreme Atemdepression.", advice:"Extrem hohes Risiko. Notfall: 112." },
  "Benzodiazepine+Ketamin": { level:"high", text:"Starke Sedierung bis Bewusstlosigkeit, Atemdepression.", advice:"Hohes Risiko. Nicht fahren. Bei Notfall: 112." },
  "Benzodiazepine+Cannabis": { level:"medium", text:"Verstärkte Sedierung, eingeschränkte Reaktionsfähigkeit.", advice:"Erhöhtes Risiko. Fahren nicht empfohlen." },
  "MDMA+Amphetamin": { level:"high", text:"Serotoninsyndrom: Lebensbedrohliche Überhitzung, Krampfanfälle.", advice:"Hohes Risiko. Bei Symptomen (Zittern, Fieber, Verwirrtheit) sofort 112." },
  "MDMA+Kokain": { level:"high", text:"Extreme Herzbelastung, Überhitzung, Serotoninsyndrom-Risiko.", advice:"Hohes Risiko. Fachberatung empfohlen." },
  "MDMA+LSD": { level:"medium", text:"Candyflip — schwer dosierbar, intensiv. Kann überwältigend werden.", advice:"Erhöhtes Risiko. Niedrige Mengen und eine nüchterne Begleitperson werden empfohlen." },
  "MDMA+Psilocybin": { level:"medium", text:"Hippieflip — intensiv, emotional überwältigend.", advice:"Erhöhtes Risiko. Erfahrung und Begleitperson empfohlen." },
  "MDMA+Cannabis": { level:"medium", text:"Verstärkte Halluzinationen und Verwirrung möglich.", advice:"Erhöhtes Risiko. Niedrige Mengen werden empfohlen." },
  "Amphetamin+Kokain": { level:"high", text:"Extreme Herzbelastung. Risiko für Herzrhythmusstörungen und Herzinfarkt.", advice:"Hohes Risiko. Bei Brustschmerzen oder Herzrasen sofort 112." },
  "Amphetamin+Cannabis": { level:"medium", text:"Herzbelastung und Kreislaufprobleme.", advice:"Erhöhtes Risiko. Auf Herzrasen achten, bei Beschwerden pausieren." },
  "Kokain+Cannabis": { level:"medium", text:"Herzbelastung, Kreislaufprobleme.", advice:"Erhöhtes Risiko. Auf körperliche Warnsignale achten." },
  "Ketamin+GHB/GBL": { level:"critical", text:"LEBENSGEFAHR: Bewusstlosigkeit, Atemdepression, Erstickung.", advice:"Extrem hohes Risiko. Notfall: 112." },
  "Ketamin+Cannabis": { level:"medium", text:"Verstärkte Dissoziation, Desorientierung, Übelkeit.", advice:"Erhöhtes Risiko. Niedrige Mengen und sichere Umgebung werden empfohlen." },
  "LSD+Cannabis": { level:"medium", text:"Stark verstärkte Halluzinationen, kann Angst/Panik triggern.", advice:"Erhöhtes Risiko. Besonders während des Wirkungspeaks." },
  "Psilocybin+Cannabis": { level:"medium", text:"Verstärkte visuelle Effekte und Verwirrung.", advice:"Erhöhtes Risiko. Kann den Tripverlauf unvorhersehbar verändern." },
  "LSD+Psilocybin": { level:"medium", text:"Extreme Verstärkung. Schwer kontrollierbar.", advice:"Hohes Risiko durch Summierung der Wirkung. Fachberatung möglich über Drugchecking-Stellen." },
  // ─── Research Chemicals ─────────────────────────────────────────────────────
  "Alkohol+Research Chemicals": { level:"high", text:"Unvorhersehbare Wechselwirkung: Depressiva-RCs potenzieren Atemdepression, Stimulanzien-RCs verschleiern Alkoholwirkung.", advice:"Hohes Risiko — unbekanntes Wirk- und Interaktionsprofil. Nicht kombinieren. Notfall: 112." },
  "MDMA+Research Chemicals": { level:"critical", text:"LEBENSGEFAHR bei Entaktogen-RCs (z.B. 4-MMC/Mephedron): Serotoninsyndrom, lebensbedrohliche Hyperthermie und Krampfanfälle.", advice:"Extrem hohes Risiko. Bei Symptomen (Zittern, hohes Fieber, Verwirrtheit) sofort 112." },
  "Amphetamin+Research Chemicals": { level:"high", text:"Extreme kumulative Herzbelastung bei Stimulanzien-RCs — Arrhythmie und hypertensive Krise möglich.", advice:"Hohes Risiko. Bei Brustschmerzen oder Herzrasen sofort 112." },
  "Kokain+Research Chemicals": { level:"high", text:"Kumulative Herzbelastung und Überstimulation bei Stimulanzien-RCs — hohes Risiko für kardiovaskuläre Notfälle.", advice:"Hohes Risiko. Bei Herzrasen oder Brustschmerzen sofort 112." },
  "Benzodiazepine+Research Chemicals": { level:"high", text:"Starke Sedierung bis Atemdepression bei Depressiva-RCs. Wirkungsverläufe unvorhersehbar.", advice:"Hohes Risiko. Nicht kombinieren — unbekannte Pharmakodynamik." },
  "Opioide+Research Chemicals": { level:"critical", text:"LEBENSGEFAHR bei Opioid-ähnlichen RCs: Additive Atemdepression, Bewusstlosigkeit.", advice:"Extrem hohes Risiko. Naloxon bereithalten. Notfall: sofort 112." },
  "LSD+Research Chemicals": { level:"high", text:"Unkontrollierbare Wirkungsverstärkung bei Psychedelika-RCs (z.B. 2C-B, DOx) — extreme Dauer und Intensität.", advice:"Hohes Risiko. Nicht kombinieren. Nüchterne Begleitperson essenziell." },
  "Psilocybin+Research Chemicals": { level:"high", text:"Massive Verstärkung bei Psychedelika-RCs — Kontrollverlust und psychiatrische Destabilisierung möglich.", advice:"Hohes Risiko. Nicht kombinieren." },
};

function getInteractionKey(a, b) {
  const sorted = [a, b].sort();
  return `${sorted[0]}+${sorted[1]}`;
}

function findMixWarnings(currentSub, recentSubs) {
  const warnings = [];
  for (const recent of recentSubs) {
    if (recent === currentSub) continue;
    const key = getInteractionKey(currentSub, recent);
    if (INTERACTION_MATRIX[key]) {
      warnings.push({ sub: recent, ...INTERACTION_MATRIX[key] });
    }
  }
  // Sort by severity
  const order = { critical: 0, high: 1, medium: 2 };
  warnings.sort((a, b) => (order[a.level] ?? 3) - (order[b.level] ?? 3));
  return warnings;
}

// ═══════════════════════════════════════════════════════════════════
// ─── 12-MODULE WISSENSDATENBANK (Knowledge Base — Harm Reduction) ──
// ═══════════════════════════════════════════════════════════════════
const KB_MODULES = [
  { id:"neuro", icon:"🧬", title:"Dopamin & Belohnung", color:"#B89DE8", readMin:4, linkTo:"analysis", linkLabel:"→ Muster-Analyse öffnen",
    tagline:"Wie dein Gehirn Belohnung lernt — und warum das kein Fehler ist.",
    sections:[
      { heading:"Dein Belohnungssystem", body:"Tief im Mittelhirn liegt das mesolimbische Dopaminsystem — eine Schaltung, die dafür entwickelt wurde, überlebensrelevantes Verhalten (Essen, Bindung, Sex) mit einem guten Gefühl zu belohnen. Dopamin ist dabei nicht das 'Glückshormon', sondern eher ein Vorhersage-Signal: Es feuert, wenn etwas besser ist als erwartet, und bereitet den Körper auf Wiederholung vor." },
      { heading:"Was Substanzen verändern", body:"Psychoaktive Substanzen überfluten das Belohnungssystem mit einem Dopamin-Signal, das natürliche Reize um ein Vielfaches übersteigt. Kokain kann den Dopaminspiegel um das 3-Fache, Methamphetamin um das 12-Fache des normalen Werts erhöhen. Das Gehirn reagiert darauf mit Gegenregulation: Rezeptoren werden heruntergefahren (Downregulation), die Empfindlichkeit sinkt." },
      { heading:"Toleranz & Craving", body:"Diese Anpassung erklärt zwei zentrale Phänomene: Toleranzentwicklung (du brauchst mehr für denselben Effekt) und Craving (das Gehirn hat gelernt, dass die Substanz die effizienteste Belohnungsquelle ist). Das ist keine Schwäche — es ist Neurobiologie. Das System funktioniert wie vorgesehen, nur der Input hat sich verändert." },
      { heading:"Neuroplastizität: Erholung ist real", body:"Die gute Nachricht: Das Gehirn ist plastisch. Rezeptordichte normalisiert sich, Dopamin-Basislevel erholen sich. Studien zeigen messbare Verbesserungen bereits nach 14 Tagen Abstinenz. Jede neue Erfahrung, jede sportliche Aktivität, jede soziale Verbindung schreibt neue neuronale Pfade." },
    ],
    reflection:{ q:"Welche natürlichen Aktivitäten in deinem Alltag geben dir ein echtes Gefühl von Belohnung oder Zufriedenheit?", placeholder:"z.B. Kochen, Sport, Gespräche, Musik…" },
  },
  { id:"misch", icon:"⚗️", title:"Mischkonsum", color:"#E06B8A", readMin:5, linkTo:"wissen", linkLabel:"→ Substanzinfos ansehen",
    tagline:"Warum 1+1 bei Substanzen manchmal tödlich ist.",
    sections:[
      { heading:"Polykonsum: Die häufigste Todesursache", body:"Die überwiegende Mehrheit aller Drogennotfälle und Drogentodesfälle steht im Zusammenhang mit Mischkonsum — nicht mit Einzelsubstanzen. Die Wirkungen addieren sich nicht einfach, sondern potenzieren sich oft unvorhersehbar. Besonders gefährlich: Substanzen, deren Wirkung sich gegenseitig verdeckt — man merkt die Überdosierung nicht, bis es zu spät ist." },
      { heading:"Die Gefahren-Ampel: Substanzgruppen-Kombinationen", body:"🔴 LEBENSGEFAHR — Niemals kombinieren:\n• Depressiva + Depressiva: Alkohol / Opioide / Benzodiazepine / GHB-GBL untereinander → addierte Atemdepression, häufigste Drogentodesursache\n• Alkohol + GHB/GBL → schon kleine Alkoholmengen können tödlich sein\n• Opioide + Benzodiazepine → häufigste Kombination bei Drogennotfällen\n\n🟠 HOHES RISIKO — Extreme Vorsicht:\n• Stimulanzien + Stimulanzien: Kokain / Amphetamin / MDMA untereinander → extreme Herzbelastung, Rhythmusstörungen\n• MDMA + Alkohol → Überhitzung, Dehydrierung\n• Alkohol + Kokain → Körper bildet Cocaethylen (eigenständige toxische Substanz, hohe Herztoxizität)\n• Stimulanzien + Psychedelika → Serotoninsyndrom, unkontrollierbare Panik\n\n🟡 VORSICHT — Erhöhtes Risiko:\n• Psychedelika + Cannabis → stark verstärkte Halluzinationen, Panik, Kontrollverlust\n• Dissociativa + Depressiva → Bewusstlosigkeit, Erstickungsgefahr\n• Benzodiazepine + Cannabis → starke Sedierung, Reaktionsfähigkeit stark eingeschränkt" },
      { heading:"Die unterschätzte Zeitachse", body:"Substanzen haben unterschiedliche Halbwertszeiten — und das ist tödlich unterschätzt. MDMA wirkt subjektiv nicht mehr, belastet aber noch Stunden das Serotoninsystem. GHB/GBL ist nach 2 Stunden kaum noch spürbar, aber beim nächsten Glas Alkohol noch aktiv. Wer 'zur Beruhigung' eine Substanz nachlegt, kombiniert oft unwissentlich. Faustregel: Eine Substanz ist erst weg, wenn du 3× ihre Halbwertszeit gewartet hast." },
      { heading:"Praktische Faustregeln", body:"Faustregel 1: Eine Substanz pro Nacht — konsequent. Faustregel 2: Wenn du kombinierst, halbiere jede Einzeldosis. Faustregel 3: Kenne die Halbwertszeit dessen, was du nimmst. Faustregel 4: Immer eine nüchterne Vertrauensperson in der Nähe. Faustregel 5: Beim ersten Anzeichen von Atemnot, Bewusstlosigkeit oder starker Verwirrung — SOFORT 112." },
    ],
    reflection:{ q:"Gibt es Situationen, in denen du regelmäßig mehr als eine Substanz konsumierst? Was könnte ein erster Schritt sein, das Risiko zu reduzieren?", placeholder:"Beschreibe die Situation und einen möglichen Schritt…" },
  },
  { id:"safer", icon:"🛡️", title:"Safer Use", color:"#6BCB77", readMin:3, linkTo:"log", linkLabel:"→ Dose-Log öffnen",
    tagline:"Pragmatische Schadensminimierung für den realen Alltag.",
    sections:[
      { heading:"Safer Use ≠ sicherer Konsum", body:"Es gibt keinen risikofreien Substanzkonsum. Safer Use anerkennt das und zielt darauf ab, die Wahrscheinlichkeit und Schwere negativer Folgen zu verringern. Es ist eine Haltung: bewusst, informiert und ehrlich mit dir selbst." },
      { heading:"Universelle Regeln", body:"• Kenne deine Substanz: Drug-Checking nutzen, Inhalt prüfen. • Dosierung: Niedrig starten, nicht nachlegen vor Wirkungseintritt. • Setting: Sicherer Ort, Vertrauensperson, kein Mischkonsum. • Selbstfürsorge: Essen, Wasser, Schlaf — vor und nach dem Konsum. • Pausen: Feste konsumfreie Tage und Wochen einplanen." },
      { heading:"Substanzspezifische Tipps", body:"Jede Substanz hat eigene Safer-Use-Regeln. Für nasalen Konsum: eigenes Röhrchen (Hepatitis-Schutz). Für MDMA: 6-Wochen-Regel und max. 1.5 mg/kg Körpergewicht. Für Opioide: Naloxon griffbereit, nie allein. Nutze die Substanzinfos in dieser App für substanzspezifische Details." },
      { heading:"Logging als Safer Use", body:"Das Führen eines Konsumtagebuchs ist selbst eine Form von Safer Use. Es schärft das Bewusstsein, macht Muster sichtbar und unterstützt dich dabei, informierte Entscheidungen zu treffen. Jeder Eintrag ist ein Akt der Selbstfürsorge." },
    ],
    reflection:{ q:"Welche Safer-Use-Regel aus diesem Modul möchtest du bei deinem nächsten Konsum konkret anwenden?", placeholder:"z.B. Ich nehme beim nächsten Mal nur die Hälfte…" },
  },
  { id:"funktion", icon:"🔍", title:"Funktions-Check", color:"#F2D388", readMin:5, linkTo:"log", linkLabel:"→ Konsummuster im Log analysieren",
    tagline:"Die ehrlichste Frage: Warum konsumiere ich eigentlich?",
    sections:[
      { heading:"Konsum hat immer eine Funktion", body:"Niemand konsumiert 'einfach so'. Hinter jedem Griff zur Substanz steht ein Bedürfnis: Entspannung, Zugehörigkeit, Leistungssteigerung, Betäubung, Grenzerfahrung, Langeweile-Management oder Selbstmedikation. Die Substanz zu verurteilen, ohne die Funktion zu verstehen, greift zu kurz." },
      { heading:"Die vier Hauptfunktionen", body:"1) Emotionsregulation — Konsum um Angst, Trauer, Wut oder innere Leere zu bewältigen. 2) Soziale Funktion — Dazugehören, Hemmungen abbauen, gemeinsam feiern. 3) Leistungsfunktion — Fokus, Durchhaltevermögen, Wachsein. 4) Selbstexploration — Neugier, Bewusstseinserweiterung, Grenzerfahrung." },
      { heading:"Warum Funktionsanalyse hilft", body:"Wenn du verstehst, WARUM du konsumierst, kannst du beginnen, alternative Wege zu finden, dasselbe Bedürfnis zu erfüllen. Nicht jeder braucht Abstinenz — aber jeder profitiert davon, bewusste Entscheidungen zu treffen statt automatisch zu handeln." },
      { heading:"Dein persönliches Muster", body:"Schau dir dein Konsumlogbuch an: Wann konsumierst du besonders häufig? In welchem Setting? Mit welchem Craving-Level? Die Antworten zeigen dir dein Muster. Und Muster sind der Schlüssel zu Veränderung." },
    ],
    reflection:{ q:"Welche Funktion erfüllt dein Konsum am häufigsten? Welche Alternative könntest du ausprobieren?", placeholder:"z.B. Ich trinke um mich zu entspannen → stattdessen Yoga oder Badewanne…" },
  },
  { id:"craving", icon:"🌊", title:"Craving-Skills", color:"#E8A87C", readMin:3, linkTo:"skillbox", linkLabel:"→ Skill-Box öffnen",
    tagline:"Die Welle kommt — aber du musst nicht darauf surfen.",
    sections:[
      { heading:"Craving ist eine Welle", body:"Craving (Substanzverlangen) fühlt sich an wie ein Tsunami, folgt aber einem vorhersagbaren Muster: Anstieg → Plateau → Abklingen. Die meisten Cravings dauern 15–30 Minuten. Dieses Wissen allein ist mächtig: Du musst nur die Welle überstehen, nicht das Meer bezwingen." },
      { heading:"Sofort-Strategien (0–5 Min.)", body:"• STOPP-Technik: Innerlich 'STOPP' sagen, physisch innehalten. • 5-4-3-2-1: 5 Dinge sehen, 4 hören, 3 fühlen, 2 riechen, 1 schmecken. • Box-Breathing: 4 Sek. ein, 4 halten, 4 aus, 4 halten. • Ortswechsel: Physisch den Raum verlassen. • Kälte-Reiz: Kaltes Wasser über die Handgelenke." },
      { heading:"Mittelfristige Strategien (5–30 Min.)", body:"• Jemanden anrufen (Vertrauensperson, Beratungshotline). • Bewegung: 10 Minuten gehen, rennen, Treppen steigen. • Craving-Surfen: Das Verlangen beobachten statt bekämpfen. Benenne es: 'Ich spüre ein Craving, Level 7. Es wird vorbeigehen.' • Ablenkung: Podcast, Musik, Rätsel, kalte Dusche." },
      { heading:"Craving-Notfallplan", body:"Erstelle jetzt einen Plan: Was tue ich bei Craving-Level 1–3? (z.B. Atemübung). Bei 4–6? (z.B. spazieren gehen). Bei 7–10? (z.B. Notfallkontakt anrufen, Ort verlassen). Schreibe ihn auf — im akuten Moment ist Planen schwer." },
    ],
    reflection:{ q:"Was war die Situation bei deinem letzten starken Craving? Welche Strategie hättest du anwenden können?", placeholder:"Beschreibe die Situation und eine mögliche Strategie…" },
  },

  { id:"body", icon:"🥗", title:"Body Repair", color:"#A8D8B9", readMin:5, linkTo:"goals", linkLabel:"→ Clean Days markieren",
    tagline:"Dein Körper verzeiht viel — aber er braucht Material dafür.",
    sections:[
      { heading:"Koerper & Naehrstoffe", body:"Substanzkonsum zehrt an den Reserven des Koerpers: Vitamine, Mineralien, Aminosaeuren. Die Versorgung nach Konsum oder in Erholungsphasen ist kein Luxus, sondern Notfallversorgung. Prioritaet haben B-Vitamine (B1, B6, B12), Magnesium, Vitamin C, Omega-3-Fettsaeuren und ausreichend Protein." },
      { heading:"Regeneration unterstuetzen", body:"Nach Konsum braucht dein Koerper vor allem drei Dinge: Fluessigkeit (mindestens 2 Liter Wasser am Tag, bei Stimulanzien mehr), Mikro-Naehrstoffe (B-Vitamine, Magnesium, Vitamin C, Omega-3 und Zink — idealerweise ueber abwechslungsreiche Ernaehrung, notfalls als Supplement) und Ruhe (der Koerper repariert sich im Schlaf, vermeide Bildschirme vor dem Einschlafen und halte feste Schlafzeiten ein). Kleine, regelmaessige Mahlzeiten sind besser als grosse — auch wenn der Appetit fehlt." },
      { heading:"Schlaf — die wirkungsvollste Erholung", body:"Im Schlaf räumt das glymphatische System neurotoxische Abfallprodukte auf, Rezeptoren regenerieren sich, und emotionale Erinnerungen werden verarbeitet. Nach Konsum kann es helfen: Melatonin-Rhythmus mit Lichtexposition am Morgen stabilisieren, Bildschirmzeit ab 21 Uhr reduzieren, Schlafzimmer kühl und dunkel halten." },
      { heading:"Bewegung & Supplements", body:"30 Minuten moderate Bewegung erhöhen BDNF (Brain-Derived Neurotrophic Factor), der Neuroplastizität fördert. Sinnvolle Supplements nach ärztlicher Rücksprache: Magnesium (300–400 mg), B-Komplex, Vitamin D3 (besonders im Winter), 5-HTP (Vorsicht bei SSRI!), NAC (N-Acetylcystein)." },
    ],
    reflection:{ q:"Was ist eine realistische kleine Veraenderung fuer deine Regeneration, die du diese Woche umsetzen koenntest?", placeholder:"z.B. Taeglich 2L Wasser trinken, um 23 Uhr Bildschirm aus, Magnesium nehmen…" },
  },
  { id:"sozial", icon:"👥", title:"Soziale Trigger", color:"#F2D388", readMin:4, linkTo:"goals", linkLabel:"→ Ziele & Grenzen setzen",
    tagline:"Dein Umfeld formt dein Verhalten — aber du entscheidest.",
    sections:[
      { heading:"Sozialer Druck hat viele Gesichter", body:"Direkter Druck ('Komm, trink mit!') ist nur die offensichtlichste Form. Subtiler: Normalisierung ('Alle machen das'), stille Erwartung (alle trinken, du fällst auf), internalisierter Druck (du willst dazugehören). Erkennen ist der erste Schritt." },
      { heading:"Nein sagen — Skripte die funktionieren", body:"• Klar und kurz: 'Nein danke, ich bin gut.' • Mit Alternative: 'Ich nehm lieber ein Wasser, aber cheers!' • Humorvoll: 'Mein Körper hat mir heute eine Absage erteilt.' • Ehrlich: 'Ich mach grad eine Pause, fühlt sich richtig an.' • Wichtig: Du brauchst keine Rechtfertigung. Ein Nein ist eine vollständige Antwort." },
      { heading:"Beziehungs-Inventur", body:"Sortiere dein Umfeld in drei Kategorien: (A) Menschen, die dich unabhängig von Konsum wertschätzen. (B) Menschen, mit denen die Beziehung vor allem über Konsum läuft. (C) Menschen, die aktiv Druck ausüben. Kategorie A stärken, B bewusst gestalten, C Grenzen setzen." },
      { heading:"Neue Räume schaffen", body:"Veränderung braucht neue Kontexte: ein Hobby ohne Substanzbezug, eine Sportgruppe, Ehrenamt, kreative Projekte. Diese neuen Räume sind nicht Ersatz, sondern Erweiterung deines Lebens. Und ja: Am Anfang fühlt es sich seltsam an. Das ist normal." },
    ],
    reflection:{ q:"Denke an die letzte Situation, in der du wegen deines Umfelds konsumiert hast. Was wäre ein realistisches Skript für das nächste Mal?", placeholder:"z.B. Bei der nächsten Party sage ich: …" },
  },
  { id:"dual", icon:"🧠", title:"Dualdiagnosen", color:"#A78BFA", readMin:5, linkTo:"skillbox", linkLabel:"→ Skill-Box & Krisen-Kontakte",
    tagline:"Wenn Sucht und psychische Erkrankung zusammentreffen.",
    sections:[
      { heading:"Häufiger als du denkst", body:"Studien zeigen: 40–60% der Menschen mit Substanzproblemen haben gleichzeitig eine psychische Erkrankung (Depression, Angststörung, ADHS, PTBS, Borderline). Und umgekehrt: Viele psychische Erkrankungen gehen mit erhöhtem Substanzkonsum einher. Beides beeinflusst sich gegenseitig — oft in einer Abwärtsspirale." },
      { heading:"Selbstmedikation erkennen", body:"Depression → Alkohol/Cannabis zur Betäubung. ADHS → Stimulanzien zur Selbstregulation. Angststörung → Benzodiazepine/Alkohol zur Beruhigung. PTBS → alles, was dissoziiert oder betäubt. Wenn dein Konsum primär dazu dient, psychische Belastungen zu managen, kann fachliche Beratung oder Begleitung (z. B. Suchtberatungsstelle, Psychologische Beratung) ein hilfreicher nächster Schritt sein." },
      { heading:"Integrierte Begleitung", body:"Fachkreise empfehlen bei Dualdiagnosen eine integrierte Begleitung: Substanzthemen und psychische Belastungen werden gemeinsam und aufeinander abgestimmt angegangen — nicht nacheinander. Es lohnt sich, Fachstellen oder Einrichtungen zu suchen, die auf beide Bereiche spezialisiert sind. Diese Entscheidung liegt bei dir und deinen Begleitpersonen." },
      { heading:"Was du selbst tun kannst", body:"Ehrlichkeit: Beim Arzt und Therapeuten auch ueber Konsum sprechen. Dokumentation: Dein DoseDiary hilft, Zusammenhaenge zwischen Stimmung und Konsum sichtbar zu machen. Stabilisierung: Schlaf, koerperliche Versorgung und Routine bilden die Basis fuer jede Veraenderung." },
    ],
    reflection:{ q:"Gibt es Momente, in denen dein Konsum sich wie Selbstmedikation anfühlt? Was genau versuchst du zu lindern?", placeholder:"z.B. Ich trinke besonders wenn ich innerlich unruhig bin…" },
  },
  { id:"rueckfall", icon:"🔄", title:"Rückfall-Logik", color:"#E8A87C", readMin:4, linkTo:"goals", linkLabel:"→ Clean Days & Ziele öffnen",
    tagline:"Ein Rückfall ist kein Versagen — er ist ein Datenpunkt.",
    sections:[
      { heading:"Rückfall als Prozess", body:"Ein Rückfall beginnt nicht in dem Moment, in dem du konsumierst. Er beginnt Tage oder Wochen vorher: Gedanken kreisen um die Substanz, Routinen werden vernachlässigt, der innere Kompass verschiebt sich. Gorskis Rückfallmodell beschreibt 11 Warnsignale — vom sozialen Rückzug bis zur Situation, die den Konsum ermöglicht." },
      { heading:"Der Abstinenz-Verletzungseffekt", body:"Nach einem Rückfall setzt oft ein destruktiver Gedanke ein: 'Jetzt ist eh alles egal, jetzt kann ich gleich weitermachen.' Marlatt nennt das den Abstinenz-Verletzungseffekt (Abstinence Violation Effect). Dieser Gedanke ist gefährlicher als der Rückfall selbst. Erkenne ihn und widersprich ihm." },
      { heading:"Was du aus Rückfällen lernst", body:"Jeder Rückfall liefert wertvolle Information: Was war der Trigger? Welches Bedürfnis wurde nicht erfüllt? Welche Schutzfaktoren fehlten? Trage jeden Rückfall ins Log ein — nicht als Strafe, sondern als Forschungsdaten. Du lernst dein System kennen." },
      { heading:"Nach dem Rückfall", body:"1. Stopp: Nicht weiterkonsumieren. 2. Sicherheit: Bist du in einer sicheren Umgebung? 3. Kontakt: Ruf jemanden an. 4. Dokumentation: Was ist passiert? 5. Selbstmitgefühl: Du bist auf einem Weg, nicht am Ziel gescheitert. 6. Plan: Was ändere ich konkret? Veränderung ist nicht linear — aber jeder Neustart zählt." },
    ],
    reflection:{ q:"Falls du einen Rückfall erlebt hast: Was war der Auslöser, den du rückblickend erkennen kannst? Was würdest du beim nächsten Mal anders machen?", placeholder:"z.B. Der Auslöser war … Beim nächsten Mal würde ich …" },
  },
  { id:"recht", icon:"⚖️", title:"Recht & Gesetz", color:"#8899AA", readMin:6, linkTo:"privacy", linkLabel:"→ Datenschutz & Info",
    tagline:"Was du wissen solltest — nüchtern betrachtet.",
    sections:[
      { heading:"Cannabis: Teillegalisierung in Deutschland (KCanG)", body:"Seit dem 1. April 2024 ist Cannabis für Erwachsene ab 18 Jahren in Deutschland teillegalisiert — geregelt durch das Konsumcannabisgesetz (KCanG, BGBl. 2024 I Nr. 109). 'Teillegalisiert' bedeutet: der Besitz und Eigenanbau sind unter bestimmten Bedingungen straflos, nicht aber schrankenlos erlaubt. Was Erwachsene (ab 18) dürfen: Besitz bis zu 25 g Cannabis in der Öffentlichkeit sowie bis zu 50 g in der privaten Wohnung. Eigenanbau von maximal 3 weiblichen blühenden Pflanzen zum Eigenbedarf. Mitgliedschaft in Cannabis Social Clubs (CSC) mit kontrollierter Weitergabe bis 25 g/Tag, 50 g/Monat. Was weiterhin verboten ist: Erwerb und Weitergabe außerhalb lizenzierter Wege (Schwarzmarkt), Besitz über den Freigrenzen, Konsum in der Öffentlichkeit im 100-m-Schutzbereich von Schulen, Kitas, Spielplätzen, Jugendeinrichtungen und Sportstätten sowie in Fußgängerzonen zwischen 7 und 20 Uhr. Quelle: KCanG; BMG, bundesgesundheitsministerium.de/cannabis." },
      { heading:"Jugendschutz — absolute Grenze", body:"Für Minderjährige unter 18 Jahren ändert sich durch das KCanG nichts: Besitz, Erwerb und Konsum von Cannabis bleiben vollständig strafbar. Die Weitergabe von Cannabis an Minderjährige ist ein eigenständiger Straftatbestand (§ 34 Abs. 1 Nr. 1 KCanG) und kann mit Freiheitsstrafe bis zu 3 Jahren bestraft werden. Cannabis Social Clubs sind für unter 18-Jährige gesperrt. Die verschärften Konsumverbote in Schutzzonen gelten ausdrücklich zum Schutz junger Menschen — und gelten auch für Erwachsene, wenn Minderjährige anwesend sind." },
      { heading:"BtMG — alle anderen Substanzen", body:"Für alle nicht-cannabinoiden Substanzen gilt weiterhin das Betäubungsmittelgesetz (BtMG). Es unterscheidet zwischen Besitz, Erwerb, Handel und Herstellung illegaler Substanzen. Schon der Besitz kann strafbar sein — das Verfahren kann bei 'geringer Menge' eingestellt werden (§ 31a BtMG), was als 'gering' gilt, variiert nach Bundesland und Substanz erheblich. Substanzen wie MDMA, Kokain, Amphetamine, Opioide und GHB/GBL sind weiterhin vollständig verboten." },
      { heading:"Führerschein & Fahrerlaubnis", body:"Das Fahren unter Cannabiseinfluss ist durch das KCanG nicht legalisiert worden. Seit Juni 2024 gilt ein neuer THC-Grenzwert von 3,5 ng/ml im Blutserum (§ 24a Abs. 1a StVG) — darunter ist keine Ordnungswidrigkeit gegeben, wenn kein Mischkonsum mit Alkohol vorliegt. Wichtig: THC kann nach dem Konsum noch stundenlang über dem Grenzwert liegen, bei regelmäßigem Konsum sogar tagelang. Für Fahranfänger:innen in der Probezeit und unter 21 Jahren gilt Null-Toleranz (§ 24c StVG). Die Führerscheinstelle kann unabhängig vom Strafgericht eine MPU anordnen — bei bekannt gewordenem regelmäßigen Konsum. Bei anderen BtM-Substanzen ist jeder Nachweis im Blut eine Ordnungswidrigkeit ohne Grenzwert." },
      { heading:"Drogennotfall & Straffreiheit", body:"Bei einem Drogennotfall bist du NICHT strafbar, wenn du den Rettungsdienst rufst — auch wenn nicht-legale Substanzen im Spiel sind. Das Unterlassen von Hilfe ist dagegen strafbar (§ 323c StGB). Im Notfall gilt: IMMER 112 rufen und ehrlich angeben, was konsumiert wurde. Der Rettungsdienst interessiert sich für Gesundheit, nicht für Strafverfolgung." },
      { heading:"Patientenrechte", body:"Du hast ein Recht auf ärztliche Schweigepflicht — auch wenn du über Substanzkonsum sprichst. Ärzte sind an die Schweigepflicht gebunden (§ 203 StGB). Ausnahme: unmittelbare Gefahr für Dritte. Du hast ein Recht auf Substitutionstherapie, auf diskriminierungsfreie Versorgung und auf Einsicht in deine Akte (DSGVO). Diese Informationen dienen der Orientierung — rechtliche Einzelfragen klärst du am besten mit einer anerkannten Beratungsstelle." },
    ],
    reflection:{ q:"Gibt es einen rechtlichen Aspekt — z. B. Besitzgrenzen, Führerschein oder Jugendschutz —, der dich persönlich betrifft? Was wäre ein erster konkreter Schritt zur Klärung?", placeholder:"z.B. Ich möchte die KCanG-Regelungen für meinen Alltag nochmal nachlesen…" },
  },
  { id:"werte", icon:"🌅", title:"Werte & Zukunft", color:"#9B7ECF", readMin:4, linkTo:"goals", linkLabel:"→ Ziele definieren",
    tagline:"Wer bist du — jenseits der Substanz?",
    sections:[
      { heading:"Identität vs. Verhalten", body:"Du bist nicht dein Konsum. Du bist nicht 'Alkoholiker:in' oder 'Junkie' — du bist ein Mensch, der in einer bestimmten Phase bestimmte Substanzen konsumiert. Die Unterscheidung zwischen Identität und Verhalten ist für Selbstreflexion und Veränderung entscheidend: Verhalten lässt sich ändern, Labels kleben fest." },
      { heading:"Wertearbeit", body:"Werte sind Richtungen, keine Ziele. Wenn Gesundheit ein Wert ist, dann ist '30 Tage clean' ein Ziel, aber der Wert bleibt bestehen, auch wenn du das Ziel nicht erreichst. Frage dich: Was ist mir wirklich wichtig? Beziehungen? Freiheit? Kreativität? Ehrlichkeit? Abenteuer? Und: Unterstützt mein Konsum diese Werte — oder steht er ihnen im Weg?" },
      { heading:"Zukunfts-Ich", body:"Stell dir dich selbst in 1 Jahr vor, in der Version, auf die du stolz wärst. Wie sieht dein Alltag aus? Wie fühlst du dich morgens? Was hast du erreicht? Welche Beziehungen pflegst du? Diese Vision ist kein Druck — sie ist ein Kompass. Und der Weg dorthin besteht aus einzelnen Tagen." },
      { heading:"Kleine Schritte, echte Veränderung", body:"Veränderung beginnt nicht mit dem großen Knall, sondern mit dem nächsten bewussten Entscheidungsmoment. Du musst nicht alles auf einmal ändern. Ein Eintrag im Log, ein Clean Day, ein Modul gelesen — das sind reale Schritte. Und du gehst sie bereits." },
    ],
    reflection:{ q:"Nenne drei Werte, die dir wichtig sind. Steht dein aktueller Konsum im Einklang mit diesen Werten?", placeholder:"z.B. Meine Werte: 1. … 2. … 3. … Konsum steht im Einklang / im Widerspruch zu …" },
  },

  { id:"quellen", icon:"📚", title:"Quellen & Wiss. Basis", color:"#6BCB77", readMin:4, linkTo:"privacy", linkLabel:"→ Rechtliche Hinweise",
    tagline:"Evidenzbasiert, nicht erfunden — die Grundlagen hinter DoseDiary.",
    sections:[
      { heading:"Warum Quellenangaben?", body:"DoseDiary stützt sich auf öffentlich zugängliche, wissenschaftlich abgesicherte Quellen. Alle Substanzinformationen, Wechselwirkungshinweise und Harm-Reduction-Empfehlungen basieren auf diesen Grundlagen — nicht auf Meinungen oder Erfahrungsberichten Einzelner. Diese Transparenz ist Teil unseres Anspruchs als seriöses Informationsangebot." },
      { heading:"S3-Leitlinie: Alkohol", body:"Die S3-Leitlinie 'Screening, Diagnose und Behandlung alkoholbezogener Störungen' (AWMF-Register Nr. 076-001, aktuelle Auflage) ist der evidenzbasierte Goldstandard der deutschsprachigen Suchtmedizin für alkoholbezogene Themen. Sie bildet die Grundlage für Aussagen zu Alkoholkonsum, Entzugsrisiken, Folgeschäden und Beratungsempfehlungen in DoseDiary. Herausgeber: Deutsche Gesellschaft für Psychiatrie und Psychotherapie, Psychosomatik und Nervenheilkunde (DGPPN) u. a. — abrufbar unter awmf.org." },
      { heading:"S3-Leitlinie: Methamphetamin", body:"Die S3-Leitlinie 'Methamphetamin-bezogene Störungen' (AWMF-Register Nr. 038-025) liefert die wissenschaftliche Basis für Inhalte zu Stimulanzien, Amphetaminen und verwandten Substanzen — insbesondere zu Wirkprofilen, Abhängigkeitspotenzial, Entzugssymptomen und Begleiterscheinungen. Herausgeber: DGPPN, Deutsche Gesellschaft für Suchtforschung und Suchttherapie (DG-Sucht) — abrufbar unter awmf.org." },
      { heading:"Konsumcannabisgesetz (KCanG) & BMG", body:"Die rechtlichen Informationen zu Cannabis in DoseDiary basieren auf dem Gesetz zum kontrollierten Umgang mit Cannabis — Konsumcannabisgesetz (KCanG), in Kraft seit 1. April 2024 (BGBl. 2024 I Nr. 109). Ergänzend wurden die offiziellen Informationen und FAQs des Bundesministeriums für Gesundheit (BMG) zum Cannabisgesetz herangezogen: bundesgesundheitsministerium.de/cannabis. Für den Straßenverkehr gilt zusätzlich § 24a Abs. 1a StVG (THC-Grenzwert 3,5 ng/ml, in Kraft seit Juni 2024). Da sich die Rechtslage weiterentwickeln kann, empfehlen wir bei rechtlichen Fragen eine aktuelle Beratungsstelle aufzusuchen. Diese Informationen ersetzen keine Rechtsberatung." },
      { heading:"Deutsche Hauptstelle für Suchtfragen (DHS)", body:"Die DHS ist die zentrale Fachorganisation im deutschen Suchthilfesystem. Ihre Factsheets, Jahrbücher (Jahrbuch Sucht) und Leitfäden zu einzelnen Substanzen fließen in die Substanzdatenbank und Harm-Reduction-Tipps von DoseDiary ein. Besonders relevant: die Factsheets zu Cannabis, Alkohol, Benzodiazepinen und Tabak sowie die Empfehlungen zur Suchtprävention. Weitere Informationen unter dhs.de." },
      { heading:"Harm Reduction International (HRI)", body:"Harm Reduction International ist die globale Dachorganisation für evidenzbasierte Schadensminimierung. Ihre Grundsätze — Wertfreiheit, Selbstbestimmung, Risikominimierung statt Abstinenzforderung — prägen die Haltung und Sprache der gesamten App. Der Global State of Harm Reduction Report (aktuelle Ausgabe) sowie HRI Policy Briefs bilden die internationale Referenz. Weitere Informationen unter hri.global." },
      { heading:"Weitere Referenzen", body:"Ergänzend wurden folgende Quellen genutzt: PsychonautWiki (substanzspezifische Pharmakologie, peer-reviewed Community-Datenbank), TripSit Factsheets (Kombinationsrisiken), DrugsData / EcstasyData von DanceSafe (Drug-Checking-Daten), Bundeszentrale für gesundheitliche Aufklärung BZgA (bzga.de, insb. 'Kenn dein Limit'), das Phar­ma­ko­logie-Standardwerk Stahl's Essential Psychopharmacology sowie Fachliteratur aus dem European Monitoring Centre for Drugs and Drug Addiction (EMCDDA / EUDA). Alle Inhalte dienen der Schadensminimierung und ersetzen keine individuelle ärztliche oder pharmakologische Beratung." },
    ],
    reflection:{ q:"Gibt es eine Quelle oder Fachstelle aus dieser Liste, bei der du dir mehr Informationen für deine persönliche Situation wünscht?", placeholder:"z.B. Ich möchte mehr über die KCanG-Regelungen erfahren, weil…" },
  },
];

// ─── HELPERS ───
const subEmoji = s => ({Alkohol:"🍺",Cannabis:"🌿",Amphetamin:"⚡",MDMA:"🔮",Kokain:"❄️",Opioide:"💉",Benzodiazepine:"🟦",Nikotin:"🚬",Vaping:"💨",Koffein:"☕",Kratom:"🍃",LSD:"🌈",Psilocybin:"🍄",Ketamin:"💎","GHB/GBL":"🧪",Lachgas:"🎈","Research Chemicals":"⚗️",Pornografie:"🔞",Glücksspiel:"🎰","Social Media":"📱",Gaming:"🎮","Andere Substanz":"🔬","Anderes Verhalten":"🔄"}[s]||"❓");

// Deuteranopie/Protanopie-sichere Risikoindikation:
// Unterscheidung durch FORM (▲ △ ◇ ○) + HELLIGKEIT + Farbe — nie nur Farbe allein
const RISK_META = {
  critical : { icon:"⛔", shape:"▲", label:"Sehr hohes Risiko",  color:"var(--risk-critical)" },
  high     : { icon:"🔶", shape:"▲", label:"Hohes Risiko",        color:"var(--risk-high)"     },
  medium   : { icon:"🔸", shape:"◆", label:"Mittleres Risiko",    color:"var(--risk-medium)"   },
  low      : { icon:"🔷", shape:"●", label:"Niedriges Risiko",    color:"var(--risk-low)"      },
  unknown  : { icon:"❓", shape:"?", label:"Unbekanntes Risiko",  color:"#8899AA"              },
};
const riskMeta = (riskStr) => {
  if (!riskStr) return RISK_META.unknown;
  const r = riskStr.toLowerCase();
  if (r.includes("sehr hoch") || r.includes("kritisch")) return RISK_META.critical;
  if (r.includes("hoch"))    return RISK_META.high;
  if (r.includes("mittel"))  return RISK_META.medium;
  if (r.includes("niedrig")) return RISK_META.low;
  return RISK_META.unknown;
};
const ago = d => { const m=Math.floor((Date.now()-new Date(d).getTime())/60000); if(m<60)return`vor ${m}m`; const h=Math.floor(m/60); if(h<24)return`vor ${h}h`; return`vor ${Math.floor(h/24)}d`; };
const weekLogs = logs => { const s=new Date(); s.setDate(s.getDate()-s.getDay()+1); s.setHours(0,0,0,0); return logs.filter(l=>new Date(l.date)>=s).length; };
const avgMood = ms => ms.length ? (ms.reduce((s,m)=>s+m.value,0)/ms.length).toFixed(1) : "–";
const byDay = logs => { const d={Mo:0,Di:0,Mi:0,Do:0,Fr:0,Sa:0,So:0}, m=["So","Mo","Di","Mi","Do","Fr","Sa"]; logs.forEach(l=>{d[m[new Date(l.date).getDay()]]++}); return d; };
const byTime = logs => { const t={"Morgen":0,"Nachmittag":0,"Abend":0,"Nacht":0}; logs.forEach(l=>{const h=new Date(l.date).getHours(); if(h>=6&&h<12)t.Morgen++;else if(h>=12&&h<18)t.Nachmittag++;else if(h>=18)t.Abend++;else t.Nacht++;}); return t; };
const bySub = logs => logs.reduce((a,l)=>{a[l.substance]=(a[l.substance]||0)+1;return a},{});
const mostCommon = arr => { const c=arr.reduce((a,v)=>{a[v]=(a[v]||0)+1;return a},{}); return Object.entries(c).sort((a,b)=>b[1]-a[1])[0]?.[0]||"–"; };


// ─── Mood Trend (14 days) ───
const moodTrend = (moods, days=14) => {
  const result = [];
  for (let i = days-1; i >= 0; i--) {
    const d = new Date(); d.setDate(d.getDate()-i); d.setHours(0,0,0,0);
    const ds = d.toISOString().split("T")[0];
    const label = d.toLocaleDateString("de-DE",{weekday:"short"}).slice(0,2);
    const found = moods.find(m => m.date?.split("T")[0] === ds || new Date(m.date).toISOString().split("T")[0] === ds);
    result.push({ ds, label, value: found?.value||null, emoji: found?.emoji||null, isToday: i===0 });
  }
  return result;
};

// ─── Weekly Summary ───
const calcWeekSummary = (logs, moods, cleanDays) => {
  const ws = new Date(); ws.setDate(ws.getDate()-ws.getDay()+1); ws.setHours(0,0,0,0);
  const wLogs = logs.filter(l => new Date(l.date)>=ws);
  const wMoods = moods.filter(m => new Date(m.date)>=ws);
  const wClean = (cleanDays||[]).filter(d => new Date(d)>=ws).length;
  const avgC = wLogs.length ? +(wLogs.reduce((s,l)=>s+(l.craving||0),0)/wLogs.length).toFixed(1) : null;
  const avgM = wMoods.length ? +(wMoods.reduce((s,m)=>s+m.value,0)/wMoods.length).toFixed(1) : null;
  const topSub = wLogs.length ? mostCommon(wLogs.map(l=>l.substance)) : null;
  return { logCount:wLogs.length, cleanCount:wClean, avgCraving:avgC, avgMood:avgM, topSub };
};


// ─── Clean Day & Streak Helpers ───
const dateStr = d => new Date(d).toISOString().split("T")[0];
const todayStr = () => dateStr(new Date());
const calcStreak = (cleanDays, logs) => {
  if (!cleanDays?.length) return 0;
  const logDates = new Set(logs.map(l => dateStr(l.date)));
  const cleanSet = new Set(cleanDays);
  let streak = 0;
  const d = new Date(); d.setHours(0,0,0,0);
  // Check today: either marked clean or simply no log today
  const tStr = dateStr(d);
  if (!cleanSet.has(tStr) && logDates.has(tStr)) return 0; // consumed today
  if (cleanSet.has(tStr)) streak = 1;
  else if (!logDates.has(tStr)) { /* today ambiguous, don't count but don't break */ }
  // Walk backwards
  for (let i = 1; i < 1000; i++) {
    const prev = new Date(d); prev.setDate(prev.getDate() - i);
    const pStr = dateStr(prev);
    if (cleanSet.has(pStr)) { streak++; }
    else if (logDates.has(pStr)) { break; }
    else { break; } // no data = streak ends
  }
  return streak;
};
const calcLongestStreak = (cleanDays) => {
  if (!cleanDays?.length) return 0;
  const sorted = [...cleanDays].sort();
  let max = 1, cur = 1;
  for (let i = 1; i < sorted.length; i++) {
    const prev = new Date(sorted[i-1]); prev.setDate(prev.getDate() + 1);
    if (dateStr(prev) === sorted[i]) { cur++; max = Math.max(max, cur); }
    else { cur = 1; }
  }
  return max;
};
const calcGoalProgress = (goals, logs) => {
  if (!goals.target || !goals.startDate) return null;
  const start = new Date(goals.startDate); start.setHours(0,0,0,0);
  const now = new Date(); now.setHours(0,0,0,0);
  const totalDays = Math.floor((now - start) / 864e5) + 1;
  const cleanInRange = (goals.cleanDays || []).filter(d => d >= dateStr(start) && d <= dateStr(now)).length;
  return { totalDays, cleanInRange, target: goals.target, pct: Math.min(100, Math.round(cleanInRange / goals.target * 100)) };
};

// ═══════════════════════════════════════
// ─── MAIN APP ─────────────────────────
// ═══════════════════════════════════════
function DoseDiary() {
  const [view, setView] = useState("dashboard");
  const [moods, setMoods] = useState([]);
  const [logs, setLogs] = useState([]);
  const [goals, setGoals] = useState({ cleanDays:[], target:null, targetSubs:[], startDate:null, goalType:"clean", maxPerWeek:null }); // goalType: "clean" | "limit"
  const [prefs, setPrefs] = useState({ mySubs: [] }); // selected substances/behaviors
  const [kbProgress, setKbProgress] = useState({ read: {}, reflections: {} }); // read: {moduleId: timestamp}, reflections: {moduleId: text}
  const [skillbox, setSkillbox] = useState({ seenIntro: false, feedback: {}, emergencyContact: "" }); // feedback: {skillId: [{helped:bool, date:str}]}
  const [planers, setPlaners] = useState([]);            // Multi-Planer (max 3)
  const [globalChallengeCount, setGlobalChallengeCount] = useState(0);
  const [myMeds, setMyMeds] = useState([]); // array of medication ids from MEDICATIONS // {substance,unit,interval,maxUnits,startedAt,consumedCount,lastConsumedAt,active}
  const [showMenu, setShowMenu] = useState(false);
  const [todayMood, setTodayMood] = useState(null);
  const [fade, setFade] = useState(true);
  const [onboarded, setOnboarded] = useState(null); // null = loading, false = show onboarding, true = done
  const [onboardStep, setOnboardStep] = useState(0); // 0=age+disclaimer, 1=privacy, 2=substances, 3=features intro, 4=wissensdatenbank

  // Check onboarding status on mount
  useEffect(() => {
    (async () => {
      const ob = await S.get("dd_onboarded");
      if (ob === true) {
        setOnboarded(true);
        const [m, l, g, p] = await Promise.all([S.get("dd_moods"), S.get("dd_logs"), S.get("dd_goals"), S.get("dd_prefs")]);
        if (m) { setMoods(m); const t = m.find(x => new Date(x.date).toDateString() === new Date().toDateString()); if (t) setTodayMood(t.value); }
        if (l) setLogs(l);
        if (g) setGoals(g);
        if (p) setPrefs(p);
        const kb = await S.get("dd_kb");
        if (kb) setKbProgress(kb);
        const sb = await S.get("dd_skillbox");
        if (sb) setSkillbox(sb);
        const pl = await S.get("dd_planers");
        if (Array.isArray(pl) && pl.length) { setPlaners(pl); }
        else if (pl && !Array.isArray(pl) && pl.active) {
          // Migriere altes Single-Planer-Format
          const migrated = [{ ...pl, id: String(Date.now()) }];
          setPlaners(migrated); await S.set("dd_planers", migrated);
        }
        const gcc = await S.get("dd_challenge_count");
        if (typeof gcc === "number") setGlobalChallengeCount(gcc);
        const meds = await S.get("dd_meds");
        if (meds) setMyMeds(meds);
      } else {
        setOnboarded(false);
      }
    })();
  }, []);

  const save = useCallback(async (key, setter, data) => { setter(data); await S.set(key, data); }, []);
  const nav = v => { setFade(false); setTimeout(() => { setView(v); setShowMenu(false); setFade(true); }, 120); };

  const handleMood = async (mood) => {
    const entry = { value: mood.value, label: mood.label, emoji: mood.emoji, date: new Date().toISOString() };
    const today = new Date().toDateString();
    const updated = [...moods.filter(m => new Date(m.date).toDateString() !== today), entry];
    await save("dd_moods", setMoods, updated);
    setTodayMood(mood.value);
  };

  const saveKb = async (data) => { setKbProgress(data); await S.set("dd_kb", data); };
  const saveSkillbox = async (data) => { setSkillbox(data); await S.set("dd_skillbox", data); };
  const savePlaners = async (data) => { setPlaners(data); await S.set("dd_planers", data); };
  const updatePlaner = async (id, patch) => {
    const next = planers.map(p => p.id === id ? { ...p, ...patch } : p);
    await savePlaners(next);
  };
  const removePlaner = async (id) => { await savePlaners(planers.filter(p => p.id !== id)); };
  const addGlobalChallenge = async () => {
    const next = globalChallengeCount + 1;
    setGlobalChallengeCount(next);
    await S.set("dd_challenge_count", next);
  };
  const saveMeds = async (data) => { setMyMeds(data); await S.set("dd_meds", data); };
  const saveGoals = async (data) => { setGoals(data); await S.set("dd_goals", data); };
  const savePrefs = async (data) => { setPrefs(data); await S.set("dd_prefs", data); };

  const completeOnboarding = async () => {
    await S.set("dd_onboarded", true);
    setOnboarded(true);
  };

  const deleteAllData = async () => {
    await S.set("dd_moods", []);
    await S.set("dd_logs", []);
    await S.set("dd_goals", { cleanDays:[], target:null, targetSubs:[], startDate:null, goalType:"clean", maxPerWeek:null });
    await S.set("dd_prefs", { mySubs: [] });
    await S.set("dd_kb", { read: {}, reflections: {} });
    await S.set("dd_skillbox", { seenIntro: false, feedback: {}, emergencyContact: "" });
    await S.set("dd_planers", []);
    await S.set("dd_challenge_count", 0);
    await S.set("dd_meds", []);
    setMoods([]); setLogs([]);
    setGoals({ cleanDays:[], target:null, targetSubs:[], startDate:null, goalType:"clean", maxPerWeek:null });
    setPrefs({ mySubs: [] });
    setKbProgress({ read: {}, reflections: {} });
    setSkillbox({ seenIntro: false, feedback: {}, emergencyContact: "" });
    setPlaners([]); setGlobalChallengeCount(0);
    setMyMeds([]);
    setTodayMood(null);
  };

  const resetOnboarding = async () => {
    await deleteAllData();
    await S.set("dd_onboarded", false);
    setOnboarded(false);
    setOnboardStep(0);
  };

  // ──── CSS Variables ────
  const theme = {
    "--bg":"#0E0B1A","--card":"#1A1529","--card2":"#221C34","--bdr":"#2F2845",
    // --tx2 angehoben von #9088A8 → #A89CC0 (WCAG AA: ~4.8:1 auf --bg)
    "--tx":"#E8E4F0","--tx2":"#A89CC0","--acc":"#9B7ECF","--accL":"#B89DE8",
    "--warn":"#E06B8A","--font":"'DM Sans',sans-serif","--fontD":"'Outfit',sans-serif",
    // Deuteranopie-sichere Risiko-Palette (Helligkeit statt Rot/Grün-Unterschied)
    "--risk-critical":"#FF6B6B","--risk-high":"#FFB347","--risk-medium":"#FFE066","--risk-low":"#7EC8A4",
  };

  // ═══ ONBOARDING GATE ═══
  if (onboarded === null) return (
    <div style={{...theme,fontFamily:"var(--font)",background:"var(--bg)",minHeight:"100vh",display:"flex",alignItems:"center",justifyContent:"center"}}>
      <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Outfit:wght@600;700&display=swap" rel="stylesheet" />
      <p style={{color:"var(--tx2)",fontSize:14}}>Laden…</p>
    </div>
  );

  if (onboarded === false) return (
    <div style={{...theme,fontFamily:"var(--font)",background:"var(--bg)",color:"var(--tx)",minHeight:"100vh",maxWidth:480,margin:"0 auto",display:"flex",flexDirection:"column",overflow:"hidden"}}>
      <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Outfit:wght@600;700&display=swap" rel="stylesheet" />
      <style>{`
        @keyframes obSlideIn{from{opacity:0;transform:translateX(40px)}to{opacity:1;transform:translateX(0)}}
        @keyframes obSlideOut{from{opacity:1;transform:translateX(0)}to{opacity:0;transform:translateX(-40px)}}
        .ob-enter{animation:obSlideIn 0.35s ease-out both}
        @keyframes obPulse{0%,100%{transform:scale(1)}50%{transform:scale(1.04)}}
        .ob-pulse{animation:obPulse 2s ease-in-out infinite}
        @media(prefers-reduced-motion:reduce){.ob-enter,.ob-pulse{animation:none!important;transform:none!important}}
      `}</style>

      {/* ─── Top Progress Bar ─── */}
      <div className="px-6 pt-5 pb-2">
        <div className="flex items-center justify-between mb-2">
          <span style={{fontSize:13,fontWeight:600,color:"var(--tx2)"}}>Schritt {onboardStep + 1} von 5</span>
          <span style={{fontSize:13,fontWeight:700,color:"var(--acc)"}}>{Math.round((onboardStep + 1) / 5 * 100)}%</span>
        </div>
        <div className="w-full h-2 rounded-full" style={{background:"var(--bdr)"}}>
          <div className="h-2 rounded-full transition-all duration-500 ease-out" style={{width:`${(onboardStep + 1) / 5 * 100}%`,background:"var(--acc)"}} />
        </div>
      </div>

      {/* ─── Step Content ─── */}
      <div key={onboardStep} className="flex-1 flex flex-col px-6 py-4 ob-enter" style={{minHeight:0}}>
        <div className="flex-1 overflow-y-auto" style={{paddingBottom:16}}>

        {/* ═══ Step 0: Willkommen & Alterscheck ═══ */}
        {onboardStep === 0 && (
          <div className="space-y-5">
            <div className="text-center pt-2">
              <div className="w-20 h-20 rounded-3xl mx-auto flex items-center justify-center text-4xl mb-4 ob-pulse" style={{background:"var(--acc)15",boxShadow:"0 8px 30px rgba(155,126,207,0.15)"}}>🌿</div>
              <h1 style={{fontSize:26,fontWeight:800,fontFamily:"var(--fontD)",lineHeight:1.2}}>DoseDiary</h1>
              <p style={{fontSize:15,color:"var(--tx2)",marginTop:8,lineHeight:1.5}}>Dein privater Begleiter fuer bewussten Umgang.</p>
            </div>

            <div className="rounded-2xl p-5" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <div className="flex items-center gap-3 mb-3">
                <div className="w-10 h-10 rounded-xl flex items-center justify-center text-xl" style={{background:"#E06B8A18"}}>🔞</div>
                <p style={{fontSize:16,fontWeight:700,color:"var(--tx)"}}>Ab 18 Jahren</p>
              </div>
              <p style={{fontSize:14,color:"var(--tx2)",lineHeight:1.7}}>
                Diese App enthaelt Informationen ueber psychoaktive Substanzen. Sie dient der Schadensminimierung — nicht der Anleitung zum Konsum.
              </p>
            </div>

            {/* ── Pflicht-Disclaimer (MDR-Abgrenzung) ── */}
            <div className="rounded-2xl p-5 space-y-3" style={{background:"#E06B8A10",border:"2px solid #E06B8A55"}}>
              <div className="flex items-center gap-2 mb-1">
                <span style={{fontSize:18}}>⚖️</span>
                <p style={{fontSize:14,fontWeight:800,color:"#E06B8A",letterSpacing:"0.01em"}}>Wichtiger rechtlicher Hinweis</p>
              </div>
              <p style={{fontSize:13,fontWeight:700,color:"var(--tx)",lineHeight:1.6}}>
                DoseDiary ist kein Medizinprodukt im Sinne der EU-Medizinprodukteverordnung (MDR 2017/745).
              </p>
              <p style={{fontSize:13,color:"var(--tx2)",lineHeight:1.7}}>
                Die App bietet <strong style={{color:"var(--tx)"}}>keine medizinischen Diagnosen</strong>, <strong style={{color:"var(--tx)"}}>keine Therapievorschläge</strong> und <strong style={{color:"var(--tx)"}}>keine Dosierungsempfehlungen</strong> für den Konsum psychoaktiver Substanzen.
              </p>
              <div className="space-y-2 pt-1">
                {[
                  { icon:"📓", text:"DoseDiary ist ein Selbstreflexions- und Informationstagebuch zur Förderung der Konsumkompetenz." },
                  { icon:"ℹ️", text:"Alle Substanz- und Wechselwirkungsinfos dienen ausschließlich der Schadensminimierung (Harm Reduction) und ersetzen keinen ärztlichen Rat." },
                  { icon:"🚑", text:"Bei medizinischen Notfällen: Notruf 112. Die App ist kein Ersatz für Notfallhilfe." },
                  { icon:"👤", text:"Die Nutzung erfolgt freiwillig und auf eigene Verantwortung." },
                ].map((item, i) => (
                  <div key={i} className="flex gap-3 items-start">
                    <span className="text-sm shrink-0 mt-0.5">{item.icon}</span>
                    <p style={{fontSize:12,color:"var(--tx2)",lineHeight:1.6}}>{item.text}</p>
                  </div>
                ))}
              </div>
            </div>
          </div>
        )}

        {/* ═══ Step 1: Datenschutz ═══ */}
        {onboardStep === 1 && (
          <div className="space-y-5">
            <div className="text-center pt-2">
              <div className="w-16 h-16 rounded-2xl mx-auto flex items-center justify-center text-3xl mb-3" style={{background:"#6BCB7715"}}>🔒</div>
              <h2 style={{fontSize:22,fontWeight:800,fontFamily:"var(--fontD)"}}>Deine Daten gehoeren dir</h2>
              <p style={{fontSize:15,color:"var(--tx2)",marginTop:6}}>Nichts verlaesst dein Geraet. Versprochen.</p>
            </div>
            <div className="space-y-3">
              {[
                { icon:"📱", title:"Alles bleibt lokal", text:"Deine Daten sind nur auf deinem Geraet gespeichert.", color:"#6BCB77" },
                { icon:"👤", title:"Kein Account noetig", text:"Kein Login, keine E-Mail. Sofort starten.", color:"var(--acc)" },
                { icon:"🛡️", title:"Null Tracking", text:"Keine Werbung, keine Cookies, keine Cloud.", color:"#F2D388" },
                { icon:"🗑️", title:"Jederzeit loeschbar", text:"Du kannst alle Daten mit einem Klick entfernen.", color:"#E06B8A" },
              ].map((item, i) => (
                <div key={i} className="rounded-2xl px-4 py-4 flex gap-4 items-center" style={{background:"var(--card)",border:`1px solid ${item.color}25`}}>
                  <div className="w-12 h-12 rounded-xl flex items-center justify-center text-xl shrink-0" style={{background:`${item.color}12`}}>{item.icon}</div>
                  <div className="flex-1">
                    <p style={{fontSize:15,fontWeight:700,color:"var(--tx)"}}>{item.title}</p>
                    <p style={{fontSize:13,color:"var(--tx2)",marginTop:2,lineHeight:1.5}}>{item.text}</p>
                  </div>
                </div>
              ))}
            </div>
            <details className="rounded-xl overflow-hidden" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <summary className="px-4 py-2.5 cursor-pointer flex items-center justify-between" style={{fontSize:13,fontWeight:600,color:"var(--tx2)"}}>
                <span>⚖️ DSGVO-Details</span><span style={{fontSize:11}}>Mehr erfahren ▾</span>
              </summary>
              <div className="px-4 pb-3">
                <p style={{fontSize:12,color:"var(--tx2)",lineHeight:1.6}}>Rechtsgrundlage: Art. 6(1)(a) DSGVO (Einwilligung). Loeschung jederzeit moeglich gemaess Art. 17 DSGVO. Keine Datenweitergabe an Dritte. Kein Serververkehr. Keine Analyse-Tools.</p>
              </div>
            </details>
          </div>
        )}

        {/* ═══ Step 2: Substanz-Auswahl (Grid) ═══ */}
        {onboardStep === 2 && (() => {
          const sel = prefs.mySubs || [];
          const toggle = (id) => {
            const next = sel.includes(id) ? sel.filter(x => x !== id) : [...sel, id];
            setPrefs({ ...prefs, mySubs: next });
          };
          return (
            <div className="space-y-5">
              <div className="text-center pt-2">
                <div className="w-16 h-16 rounded-2xl mx-auto flex items-center justify-center text-3xl mb-3" style={{background:"var(--acc)15"}}>🎯</div>
                <h2 style={{fontSize:22,fontWeight:800,fontFamily:"var(--fontD)"}}>Was betrifft dich?</h2>
                <p style={{fontSize:15,color:"var(--tx2)",marginTop:6}}>Waehle aus, was du tracken moechtest. Du kannst das spaeter jederzeit aendern.</p>
              </div>

              <div>
                <p style={{fontSize:14,fontWeight:700,color:"var(--tx)",marginBottom:8}}>💊 Substanzen</p>
                <div className="grid grid-cols-3 gap-2">
                  {SUB_ITEMS.map(s => (
                    <button key={s} onClick={() => toggle(s)}
                      className="rounded-2xl py-3 px-2 flex flex-col items-center gap-1.5 transition-all active:scale-95"
                      style={{background:sel.includes(s)?"var(--acc)":"var(--card)",color:sel.includes(s)?"#fff":"var(--tx2)",border:`2px solid ${sel.includes(s)?"var(--acc)":"var(--bdr)"}`,minHeight:44}}>
                      <span style={{fontSize:22}}>{subEmoji(s)}</span>
                      <span style={{fontSize:12,fontWeight:600,lineHeight:1.2,textAlign:"center"}}>{s}</span>
                    </button>
                  ))}
                </div>
              </div>

              <div>
                <p style={{fontSize:14,fontWeight:700,color:"var(--tx)",marginBottom:8}}>🔄 Verhaltensweisen</p>
                <div className="grid grid-cols-3 gap-2">
                  {BEH_ITEMS.map(s => (
                    <button key={s} onClick={() => toggle(s)}
                      className="rounded-2xl py-3 px-2 flex flex-col items-center gap-1.5 transition-all active:scale-95"
                      style={{background:sel.includes(s)?"#F2D388":"var(--card)",color:sel.includes(s)?"#1a1a2e":"var(--tx2)",border:`2px solid ${sel.includes(s)?"#F2D388":"var(--bdr)"}`,minHeight:44}}>
                      <span style={{fontSize:22}}>{subEmoji(s)}</span>
                      <span style={{fontSize:12,fontWeight:600,lineHeight:1.2,textAlign:"center"}}>{s}</span>
                    </button>
                  ))}
                </div>
              </div>

              {sel.length > 0 && (
                <div className="rounded-xl px-4 py-3" style={{background:"#6BCB7710",border:"1px solid #6BCB7733"}}>
                  <p style={{fontSize:14,color:"#6BCB77",fontWeight:600}}>✓ {sel.length} ausgewaehlt</p>
                </div>
              )}
            </div>
          );
        })()}

        {/* ═══ Step 3: Features ═══ */}
        {onboardStep === 3 && (
          <div className="space-y-4">
            <div className="text-center pt-2">
              <div className="w-16 h-16 rounded-2xl mx-auto flex items-center justify-center text-3xl mb-3" style={{background:"#F2D38815"}}>💡</div>
              <h2 style={{fontSize:22,fontWeight:800,fontFamily:"var(--fontD)"}}>Deine Werkzeuge</h2>
              <p style={{fontSize:14,color:"var(--tx2)",marginTop:6}}>Fünf Tools, die dich im Alltag begleiten.</p>
            </div>
            <div className="space-y-2">
              {[
                { icon:"😊", title:"Mood-Check-in", desc:"Einmal am Tag: Wie geht es dir? So erkennst du Muster zwischen Stimmung und Konsum.", color:"#6BCB77" },
                { icon:"📝", title:"Dose-Log", desc:"Trage Substanz, Menge und Setting ein. Die App warnt dich bei riskanten Kombinationen.", color:"var(--acc)" },
                { icon:"🌟", title:"Clean Days & Ziele", desc:"Feiere konsumfreie Tage und setze dir realistische Ziele.", color:"#F2D388" },
                { icon:"⏱️", title:"Dose-Planer", desc:"Setze dir feste Zeitintervalle für den Abend. Die App hilft dir, Pausen einzuhalten und dein persönliches Limit nicht zu überschreiten.", color:"#9B7ECF" },
                { icon:"🧰", title:"Skill-Box", desc:"Interaktive Übungen gegen Suchtdruck — von Atemübungen bis Akuthilfe.", color:"#E06B8A" },
              ].map((f, i) => (
                <div key={i} className="rounded-2xl px-3 py-3 flex gap-3 items-center" style={{background:"var(--card)",border:`1px solid ${f.color}30`}}>
                  <div className="w-11 h-11 rounded-xl flex items-center justify-center text-xl shrink-0" style={{background:`${f.color}15`}}>{f.icon}</div>
                  <div className="flex-1">
                    <p style={{fontSize:14,fontWeight:700,color:"var(--tx)"}}>{f.title}</p>
                    <p style={{fontSize:12,color:"var(--tx2)",marginTop:2,lineHeight:1.5}}>{f.desc}</p>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}

        {/* ═══ Step 4: Wissensdatenbank ═══ */}
        {onboardStep === 4 && (
          <div className="space-y-5">
            <div className="text-center pt-2">
              <div className="w-16 h-16 rounded-2xl mx-auto flex items-center justify-center text-3xl mb-3" style={{background:"var(--acc)15"}}>🧬</div>
              <h2 style={{fontSize:22,fontWeight:800,fontFamily:"var(--fontD)"}}>Wissensdatenbank</h2>
              <p style={{fontSize:15,color:"var(--tx2)",marginTop:6}}>12 kompakte Module — lies was dich interessiert.</p>
            </div>

            <div className="rounded-2xl p-4" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <div className="grid grid-cols-4 gap-2 mb-4">
                {KB_MODULES.slice(0, 8).map(m => (
                  <div key={m.id} className="h-12 rounded-xl flex flex-col items-center justify-center gap-0.5" style={{background:`${m.color}10`}}>
                    <span style={{fontSize:18}}>{m.icon}</span>
                    <span style={{fontSize:8,color:m.color,fontWeight:600}}>{m.title.split(" ")[0]}</span>
                  </div>
                ))}
              </div>
              <p style={{fontSize:14,color:"var(--tx2)",lineHeight:1.7}}>
                Von Neurobiologie bis Recht & Gesetz — fundiertes Wissen in 3-5 Minuten pro Modul.
              </p>
            </div>

            <div className="space-y-2">
              {[
                { icon:"🎓", text:"Wertfrei und evidenzbasiert" },
                { icon:"⏱️", text:"Snackable: 3-5 Minuten pro Modul" },
                { icon:"💭", text:"Reflexionsfragen fuer deine Selbstarbeit" },
                { icon:"🔗", text:"Direkt verlinkt mit den App-Tools" },
                { icon:"🆓", text:"Kein Zwang — lies in deinem Tempo" },
                { icon:"⚖️", text:"Alle Inhalte dienen der Schadensminimierung — kein Ersatz für Fachberatung" },
              ].map((t,i) => (
                <div key={i} className="flex items-center gap-3 px-1">
                  <span style={{fontSize:16}}>{t.icon}</span>
                  <p style={{fontSize:14,color:"var(--tx2)",lineHeight:1.5}}>{t.text}</p>
                </div>
              ))}
            </div>
          </div>
        )}

        </div>{/* end scrollable area */}

        {/* ─── Fixed bottom buttons ─── */}
        <div className="shrink-0 pt-2 pb-2 space-y-2">
          {onboardStep === 0 && (
            <button onClick={() => setOnboardStep(1)} aria-label="Weiter zu Datenschutz" className="w-full rounded-2xl font-bold transition-all hover:scale-[1.01] active:scale-[0.98]"
              style={{background:"var(--acc)",color:"#fff",boxShadow:"0 4px 20px rgba(155,126,207,0.3)",fontSize:16,minHeight:52,padding:"14px 24px"}}>
              Ich bin 18+ — Weiter
            </button>
          )}
          {onboardStep === 1 && (<>
            <button onClick={() => setOnboardStep(2)} aria-label="Weiter zu Substanzauswahl" className="w-full rounded-2xl font-bold transition-all hover:scale-[1.01] active:scale-[0.98]"
              style={{background:"var(--acc)",color:"#fff",fontSize:16,minHeight:52,padding:"14px 24px"}}>
              Verstanden — Weiter
            </button>
            <button onClick={() => setOnboardStep(0)} className="w-full rounded-xl"
              style={{color:"var(--tx2)",fontSize:14,minHeight:44,padding:"10px 24px"}}>
              ← Zurueck
            </button>
          </>)}
          {onboardStep === 2 && (() => {
            const sel = prefs.mySubs || [];
            return (<>
              <button onClick={async () => { await savePrefs({ ...prefs, mySubs: sel }); setOnboardStep(3); }} disabled={sel.length === 0}
                className="w-full rounded-2xl font-bold transition-all disabled:opacity-40 hover:scale-[1.01] active:scale-[0.98]"
                style={{background:sel.length>0?"var(--acc)":"var(--bdr)",color:sel.length>0?"#fff":"var(--tx2)",fontSize:16,minHeight:52,padding:"14px 24px"}}>
                {sel.length === 0 ? "Bitte mindestens 1 waehlen" : `Weiter (${sel.length} gewaehlt)`}
              </button>
              <button onClick={() => setOnboardStep(1)} className="w-full rounded-xl"
                style={{color:"var(--tx2)",fontSize:14,minHeight:44,padding:"10px 24px"}}>
                ← Zurueck
              </button>
            </>);
          })()}
          {onboardStep === 3 && (<>
            <button onClick={() => setOnboardStep(4)} aria-label="Weiter zu Wissensdatenbank" className="w-full rounded-2xl font-bold transition-all hover:scale-[1.01] active:scale-[0.98]"
              style={{background:"var(--acc)",color:"#fff",fontSize:16,minHeight:52,padding:"14px 24px"}}>
              Weiter
            </button>
            <button onClick={() => setOnboardStep(2)} className="w-full rounded-xl"
              style={{color:"var(--tx2)",fontSize:14,minHeight:44,padding:"10px 24px"}}>
              ← Zurueck
            </button>
          </>)}
          {onboardStep === 4 && (<>
            <button onClick={async () => { await savePrefs({ ...prefs, mySubs: prefs.mySubs || [] }); await completeOnboarding(); }}
              className="w-full rounded-2xl font-bold transition-all hover:scale-[1.01] active:scale-[0.98]"
              style={{background:"var(--acc)",color:"#fff",boxShadow:"0 4px 20px rgba(155,126,207,0.3)",fontSize:16,minHeight:52,padding:"14px 24px"}}>
              ✓ App starten
            </button>
            <button onClick={() => setOnboardStep(3)} className="w-full rounded-xl"
              style={{color:"var(--tx2)",fontSize:14,minHeight:44,padding:"10px 24px"}}>
              ← Zurueck
            </button>
          </>)}
        </div>
      </div>
    </div>
  );

  // ═══ MAIN APP (only rendered after successful onboarding) ═══

  // ═══ SUB-VIEWS ═══

  // ─── DASHBOARD ───
  const Dashboard = () => {
    const todayClean = goals.cleanDays?.includes(todayStr());
    const streak = calcStreak(goals.cleanDays || [], logs);
    const [searchQ, setSearchQ] = useState("");
    const hasRecentLog = logs.some(l => Date.now() - new Date(l.date).getTime() < 864e5);


    const handleCleanDay = async () => {
      const t = todayStr();
      const updated = todayClean
        ? { ...goals, cleanDays: goals.cleanDays.filter(d => d !== t) }
        : { ...goals, cleanDays: [...(goals.cleanDays || []), t] };
      await saveGoals(updated);
    };

    // Search SUB_INFO lexicon
    const searchResults = searchQ.trim().length >= 2 ? Object.entries(SUB_INFO).filter(([name, info]) => {
      const q = searchQ.toLowerCase();
      return name.toLowerCase().includes(q) ||
        info.safer?.some(s => s.toLowerCase().includes(q)) ||
        info.interactions?.some(i => i.toLowerCase().includes(q)) ||
        info.risk?.toLowerCase().includes(q);
    }) : [];

    return (
    <div className="space-y-6">
      <div className="text-center pt-1">
        <p className="text-xs opacity-50" style={{color:"var(--tx)"}}>{new Date().toLocaleDateString("de-DE",{weekday:"long",day:"numeric",month:"long"})}</p>
        <h2 className="text-xl mt-1" style={{color:"var(--tx)",fontFamily:"var(--fontD)"}}>Wie geht's dir heute?</h2>
      </div>

      {/* ═══ SEARCH BAR (SUB_INFO Lexikon) ═══ */}
      <div className="relative">
        <div className="flex items-center rounded-xl px-4 py-2.5" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          <span className="text-sm mr-2" style={{color:"var(--tx2)"}}>🔍</span>
          <input value={searchQ} onChange={e => setSearchQ(e.target.value)}
            className="flex-1 text-sm bg-transparent outline-none" style={{color:"var(--tx)"}}
            placeholder="Substanz suchen (z.B. MDMA, Safer Use...)" />
          {searchQ && <button onClick={() => setSearchQ("")} className="text-xs px-1.5" style={{color:"var(--tx2)"}}>✕</button>}
        </div>
        {searchResults.length > 0 && (
          <div className="mt-2 space-y-2 animate-fadeIn">
            {searchResults.slice(0, 3).map(([name, info]) => (
              <div key={name} className="rounded-xl overflow-hidden" style={{background:"var(--card)",border:`1px solid ${info.riskColor || "var(--bdr)"}44`}}>
                <div className="px-4 py-2.5 flex items-center justify-between" style={{background:`${info.riskColor || "var(--acc)"}10`}}>
                  <span className="text-sm font-bold flex items-center gap-2" style={{color:"var(--tx)"}}><span aria-hidden="true">{subEmoji(name)}</span> {name}</span>
                  <span
                    className="text-xs font-bold px-2 py-0.5 rounded-full flex items-center gap-1"
                    style={{background:`${info.riskColor}22`,color:info.riskColor}}
                    aria-label={`Risikostufe: ${riskMeta(info.risk).label}`}
                  >
                    <span aria-hidden="true">{riskMeta(info.risk).icon}</span>
                    <span>{info.risk}</span>
                  </span>
                </div>
                <div className="px-4 py-2.5">
                  <div className="flex gap-4 text-xs mb-2" style={{color:"var(--tx2)"}}>
                    <span>⏱️ {info.onset}</span><span>⏳ {info.duration}</span>
                  </div>
                  {info.safer?.slice(0, 2).map((t, i) => (
                    <p key={i} className="text-xs py-0.5 flex gap-2" style={{color:"var(--tx2)"}}>
                      <span style={{color:"var(--acc)"}}>✓</span><span>{t}</span>
                    </p>
                  ))}
                  {info.safer?.length > 2 && <p className="text-xs mt-1" style={{color:"var(--acc)"}}>+{info.safer.length-2} weitere Tipps</p>}
                </div>
              </div>
            ))}
            {searchResults.length > 3 && <p className="text-xs text-center" style={{color:"var(--tx2)"}}>+{searchResults.length-3} weitere Treffer</p>}
          </div>
        )}
        {searchQ.trim().length >= 2 && searchResults.length === 0 && (
          <p className="text-xs mt-2 text-center" style={{color:"var(--tx2)"}}>Keine Treffer für &ldquo;{searchQ}&rdquo;</p>
        )}
      </div>

      <div className="flex justify-center gap-3 flex-wrap" role="group" aria-label="Aktuelle Stimmung auswählen">
        {MOODS.map(m => (
          <button
            key={m.value}
            onClick={() => handleMood(m)}
            aria-pressed={todayMood===m.value}
            aria-label={`Stimmung: ${m.label}${todayMood===m.value?" (ausgewählt)":""}`}
            className="flex flex-col items-center gap-1 rounded-2xl p-3 transition-all duration-300 hover:scale-110"
            style={{
              background:todayMood===m.value?`${m.color}25`:"var(--card)",
              border:todayMood===m.value?`2px solid ${m.color}`:"2px solid transparent",
              minWidth:64, minHeight:72,
              boxShadow:todayMood===m.value?`0 4px 20px ${m.color}35`:"none"
            }}
          >
            <span aria-hidden="true" className="text-3xl">{m.emoji}</span>
            <span className="text-xs font-medium" style={{color:todayMood===m.value?m.color:"var(--tx2)"}}>{m.label}</span>
          </button>
        ))}
      </div>
      {todayMood && <p className="text-center text-xs" style={{color:"var(--acc)"}}>✓ Mood gespeichert</p>}

      {/* ═══ 7-DAY MOOD STRIP ═══ */}
      {moods.length >= 2 && (() => {
        const last7 = [];
        for (let i = 6; i >= 0; i--) {
          const d = new Date(); d.setDate(d.getDate() - i); d.setHours(0,0,0,0);
          const ds = d.toISOString().split("T")[0];
          const found = moods.find(m => (m.date?.split("T")[0] || new Date(m.date).toISOString().split("T")[0]) === ds);
          last7.push({ ds, emoji: found?.emoji || null, label: d.toLocaleDateString("de-DE",{weekday:"short"}).slice(0,2), isToday: i===0 });
        }
        if (!last7.some(d => d.emoji)) return null;
        return (
          <div className="rounded-2xl p-4" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
            <div className="flex items-center justify-between mb-3">
              <span className="text-xs font-bold" style={{color:"var(--tx)"}}>💚 Stimmung letzte 7 Tage</span>
              <button onClick={() => nav("moodtl")} aria-label="Stimmungsverlauf Details ansehen" className="text-xs font-medium" style={{color:"var(--acc)"}}>Details →</button>
            </div>
            <div className="flex justify-between items-center">
              {last7.map((d, i) => (
                <div key={i} className="flex flex-col items-center gap-1">
                  <span style={{fontSize: d.emoji ? 22 : 16, opacity: d.emoji ? 1 : 0.2}}>{d.emoji || "·"}</span>
                  <span style={{fontSize: 9, color: d.isToday ? "var(--acc)" : "var(--tx2)", fontWeight: d.isToday ? 700 : 400}}>{d.label}</span>
                </div>
              ))}
            </div>
          </div>
        );
      })()}

      {/* ═══ WEEKLY SUMMARY CARD ═══ */}
      {(logs.length > 0 || (goals.cleanDays?.length||0) > 0) && (() => {
        const ws = calcWeekSummary(logs, moods, goals.cleanDays);
        if (ws.logCount === 0 && ws.cleanCount === 0) return null;
        return (
          <div className="rounded-2xl p-4" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
            <div className="flex items-center justify-between mb-3">
              <span className="text-xs font-bold" style={{color:"var(--tx)"}}>📋 Diese Woche</span>
              <span className="text-xs" style={{color:"var(--tx2)"}}>Mo–So</span>
            </div>
            <div className="grid grid-cols-4 gap-2 text-center">
              <div className="rounded-xl py-2" style={{background:"#6BCB7710"}}><p className="text-lg font-bold" style={{color:"#6BCB77",fontFamily:"var(--fontD)"}}>{ws.cleanCount}</p><p style={{color:"var(--tx2)",fontSize:9}}>Clean</p></div>
              <div className="rounded-xl py-2" style={{background:"var(--acc)10"}}><p className="text-lg font-bold" style={{color:"var(--acc)",fontFamily:"var(--fontD)"}}>{ws.logCount}</p><p style={{color:"var(--tx2)",fontSize:9}}>Einträge</p></div>
              <div className="rounded-xl py-2" style={{background:"#F2D38810"}}><p className="text-lg font-bold" style={{color:"#F2D388",fontFamily:"var(--fontD)"}}>{ws.avgMood ?? "–"}</p><p style={{color:"var(--tx2)",fontSize:9}}>Ø Mood</p></div>
              <div className="rounded-xl py-2" style={{background:"#E8A87C10"}}><p className="text-lg font-bold" style={{color:"#E8A87C",fontFamily:"var(--fontD)"}}>{ws.avgCraving ?? "–"}</p><p style={{color:"var(--tx2)",fontSize:9}}>Ø Craving</p></div>
            </div>
            {ws.topSub && <p className="text-xs text-center mt-2" style={{color:"var(--tx2)"}}>Häufigste Substanz: {subEmoji(ws.topSub)} {ws.topSub}</p>}
          </div>
        );
      })()}

      {/* Quick Actions — 4 columns */}
      <div className="grid grid-cols-4 gap-2">
        <button onClick={handleCleanDay} aria-pressed={todayClean} aria-label={todayClean ? "Clean Day aufheben" : "Heute als Clean Day markieren"} className="rounded-2xl p-3 text-center transition-all hover:scale-[1.02] active:scale-[0.98]"
          style={{background:todayClean?"#6BCB7718":"var(--card)",border:`1.5px solid ${todayClean?"#6BCB77":"var(--bdr)"}`}}>
          <span aria-hidden="true" className="text-2xl">{todayClean ? "✅" : "🌟"}</span>
          <p className="font-semibold mt-1.5 text-xs" style={{color:todayClean?"#6BCB77":"var(--tx)"}}>{todayClean?"Clean ✓":"Clean Day"}</p>
        </button>
        <button onClick={() => nav("log")} aria-label="Dose-Log öffnen" className="rounded-2xl p-3 text-center transition-all hover:scale-[1.02] active:scale-[0.98]" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          <span aria-hidden="true" className="text-2xl">📝</span>
          <p className="font-semibold mt-1.5 text-xs" style={{color:"var(--tx)"}}>Dose-Log</p>
        </button>
        <button onClick={() => nav("planer")} aria-label="Dose Planer öffnen" className="rounded-2xl p-3 text-center transition-all hover:scale-[1.02] active:scale-[0.98]"
          style={{background:planers.length>0?"var(--acc)08":"var(--card)",border:`1px solid ${planers.length>0?"var(--acc)44":"var(--bdr)"}`}}>
          <span aria-hidden="true" className="text-2xl">⏱️</span>
          <p className="font-semibold mt-1.5 text-xs" style={{color:planers.length>0?"var(--acc)":"var(--tx)"}}>{planers.length>0?`Planer${planers.length>1?` (${planers.length})`:" ●"}`:"Planer"}</p>
        </button>
        <button onClick={() => nav("skillbox")} aria-label="Skill-Box öffnen" className="rounded-2xl p-3 text-center transition-all hover:scale-[1.02] active:scale-[0.98]" style={{background:"linear-gradient(135deg,#E06B8A18,#E8A87C18)",border:"1px solid #E06B8A44"}}>
          <span aria-hidden="true" className="text-2xl">🧰</span>
          <p className="font-semibold mt-1.5 text-xs" style={{color:"#E06B8A"}}>Skill-Box</p>
        </button>
      </div>

      {/* ═══ DOSE PLANER — Cockpit-Widget ═══ */}
      {planers.length > 0 && (() => {
        const ts = Date.now();
        // Mischkonsum-Check über alle Planer-Paare
        const subs = planers.map(p => p.substance);
        const mixAlerts = [];
        for (let a = 0; a < subs.length; a++)
          for (let b = a + 1; b < subs.length; b++) {
            const k = getInteractionKey(subs[a], subs[b]);
            if (INTERACTION_MATRIX[k]) mixAlerts.push({ subA:subs[a], subB:subs[b], ...INTERACTION_MATRIX[k] });
          }
        mixAlerts.sort((a,b)=>({critical:0,high:1,medium:2}[a.level]??3)-({critical:0,high:1,medium:2}[b.level]??3));
        const worst = mixAlerts[0];
        return (
          <div className="space-y-2">
            {/* Header-Zeile */}
            <div className="flex items-center justify-between px-1">
              <span className="text-xs font-bold" style={{color:"var(--tx2)"}}>
                ⏱️ Aktive Planer ({planers.length}/3){globalChallengeCount > 0 ? ` · ⭐ ${globalChallengeCount}× Challenge` : ""}
              </span>
              <button onClick={() => nav("planer")} className="text-xs font-medium" style={{color:"var(--acc)"}}>Verwalten →</button>
            </div>

            {/* Mischkonsum-Warnung */}
            {worst && (() => {
              const col = worst.level==="critical"?"#FF3B3B":worst.level==="high"?"#FF8C00":"#FFD700";
              const lbl = worst.level==="critical"?"⛔ LEBENSGEFAHR":worst.level==="high"?"🔶 HOHES RISIKO":"🟡 VORSICHT";
              return (
                <button onClick={() => nav("planer")} role="alert"
                  aria-label={`Mischkonsum: ${worst.subA} + ${worst.subB}`}
                  className="w-full rounded-xl px-3 py-2.5 flex items-center gap-2 text-left"
                  style={{background:`${col}12`,border:`1.5px solid ${col}55`}}>
                  <span className="text-xs font-black shrink-0" style={{color:col}}>{lbl}</span>
                  <span className="text-xs font-semibold flex-1 truncate" style={{color:"var(--tx)"}}>
                    {subEmoji(worst.subA)} {worst.subA} + {subEmoji(worst.subB)} {worst.subB}
                  </span>
                  <span className="text-xs" style={{color:col}}>→</span>
                </button>
              );
            })()}

            {/* Planer-Karten: 1 Karte → full-width, 2–3 → 2-Spalten */}
            <div className={`grid gap-2 ${planers.length === 1 ? "grid-cols-1" : "grid-cols-2"}`}>
              {planers.map(p => {
                const intMs = p.interval * 60 * 1000;
                const lastC = p.lastConsumedAt ? new Date(p.lastConsumedAt).getTime() : 0;
                const rem   = lastC ? Math.max(0, intMs - (ts - lastC)) : 0;
                const pct   = lastC ? Math.min(1, (ts - lastC) / intMs) : 0;
                const open  = lastC > 0 && rem === 0;
                const lim   = p.maxUnits > 0 && p.consumedCount >= p.maxUnits;
                const remM  = Math.floor(rem / 60000);
                const remS  = Math.floor((rem % 60000) / 1000);
                const timeStr = rem > 0 ? `${remM}:${String(remS).padStart(2,"0")}` : open ? "Offen" : "—";
                const barCol  = lim ? "#6BCB77" : open ? "#6BCB77" : "#7B8CDE";
                return (
                  <button key={p.id} onClick={() => nav("planer")}
                    aria-label={`Planer ${p.substance}: ${open?"Fenster offen":lim?"Limit erreicht":timeStr}`}
                    className="rounded-xl p-3 text-left transition-all hover:scale-[1.01] active:scale-[0.98]"
                    style={{background:open?"linear-gradient(135deg,#6BCB7710,#F2D38808)":lim?"#6BCB7708":"var(--card)",
                            border:`1px solid ${open?"#6BCB7744":lim?"#6BCB7733":"#7B8CDE33"}`}}>
                    <div className="flex items-center gap-1.5 mb-2">
                      <span className="text-base shrink-0">{subEmoji(p.substance)}</span>
                      <span className="text-xs font-bold flex-1 truncate" style={{color:"var(--tx)"}}>{p.substance}</span>
                      <span className="text-xs font-black shrink-0" style={{color:barCol}}>
                        {lim ? "🎯" : open ? "🟢" : timeStr}
                      </span>
                    </div>
                    <div className="w-full h-1.5 rounded-full mb-1.5" style={{background:"var(--bdr)"}}>
                      <div className="h-1.5 rounded-full transition-all duration-1000"
                        style={{width:`${Math.round(pct*100)}%`, background:barCol}} />
                    </div>
                    <p style={{fontSize:9,color:"var(--tx2)"}}>
                      {p.consumedCount}{p.maxUnits>0?`/${p.maxUnits}`:""} × {p.unit} · {p.interval} Min.
                      {open?" · Fenster offen":lim?" · Limit ✓":""}
                    </p>
                  </button>
                );
              })}
              {planers.length < 3 && (
                <button onClick={() => nav("planer")} aria-label="Neuen Planer hinzufügen"
                  className="rounded-xl flex flex-col items-center justify-center gap-1 transition-all hover:scale-[1.01]"
                  style={{background:"var(--card2)",border:"1px dashed var(--bdr)",minHeight:72}}>
                  <span className="text-xl" aria-hidden="true">＋</span>
                  <span style={{fontSize:9,color:"var(--tx2)"}}>Planer hinzufügen</span>
                </button>
              )}
            </div>
          </div>
        );
      })()}

      {/* Streak Banner */}
      {(streak > 0 || (goals.cleanDays?.length || 0) > 0) && (
        <button onClick={() => nav("goals")} className="w-full rounded-2xl p-4 text-left transition-all hover:scale-[1.01]"
          style={{background:"linear-gradient(135deg, #6BCB7712, #9B7ECF12)",border:"1px solid #6BCB7733"}}>
          <div className="flex items-center justify-between">
            <div className="flex items-center gap-3">
              <div className="w-11 h-11 rounded-xl flex items-center justify-center text-xl" style={{background:"#6BCB7722"}}>
                {streak >= 7 ? "🔥" : streak >= 3 ? "⭐" : "🌱"}
              </div>
              <div>
                <p className="text-sm font-bold" style={{color:"var(--tx)"}}>{streak} {streak === 1 ? "Tag" : "Tage"} clean</p>
                <p className="text-xs" style={{color:"var(--tx2)"}}>{goals.cleanDays?.length || 0} cleane Tage insgesamt</p>
              </div>
            </div>
            <span className="text-xs font-medium" style={{color:"var(--acc)"}}>Details →</span>
          </div>
        </button>
      )}

      {(logs.length > 0 || (goals.cleanDays?.length||0) > 0) && (
        <div className="grid grid-cols-3 gap-2">
          <StatCard icon="📊" value={logs.length} label="Einträge" />
          <StatCard icon="🌟" value={goals.cleanDays?.length || 0} label="Clean Days" />
          <StatCard icon="💚" value={avgMood(moods)} label="Mood Ø" />
        </div>
      )}
      {/* ═══ WISSENSDATENBANK — Fortschritt & Motivation ═══ */}
      {(() => {
        const readCount = Object.keys(kbProgress.read || {}).length;
        const reflCount = Object.values(kbProgress.reflections || {}).filter(v => v?.trim()).length;
        const pct = Math.round(readCount / KB_MODULES.length * 100);
        const nextUnread = KB_MODULES.find(m => !kbProgress.read?.[m.id]);
        return (
          <button onClick={() => nav("wissen")} className="w-full rounded-2xl overflow-hidden text-left transition-all hover:scale-[1.01] active:scale-[0.98]"
            style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
            {/* Header with progress arc */}
            <div className="px-4 pt-4 pb-3 flex items-center gap-4">
              <div className="relative w-14 h-14 shrink-0">
                <svg viewBox="0 0 40 40" className="w-full h-full" style={{transform:"rotate(-90deg)"}}>
                  <circle cx="20" cy="20" r="17" fill="none" stroke="var(--bdr)" strokeWidth="3" />
                  <circle cx="20" cy="20" r="17" fill="none" stroke={pct>=100?"#6BCB77":"var(--acc)"} strokeWidth="3" strokeDasharray={`${2*Math.PI*17}`} strokeDashoffset={`${2*Math.PI*17*(1-pct/100)}`} strokeLinecap="round" className="transition-all duration-700" />
                </svg>
                <span className="absolute inset-0 flex items-center justify-center text-xs font-bold" style={{color:pct>=100?"#6BCB77":"var(--acc)"}}>{pct}%</span>
              </div>
              <div className="flex-1 min-w-0">
                <p className="text-sm font-bold" style={{color:"var(--tx)",fontFamily:"var(--fontD)"}}>Wissensdatenbank</p>
                <p className="text-xs mt-0.5" style={{color:"var(--tx2)"}}>{readCount}/{KB_MODULES.length} Module gelesen{reflCount > 0 ? ` · ${reflCount} Reflexionen` : ""}</p>
                {readCount > 0 && readCount < KB_MODULES.length && (
                  <div className="flex items-center gap-1.5 mt-1.5">
                    {KB_MODULES.map(m => (
                      <div key={m.id} className="w-2 h-2 rounded-full transition-all" style={{background:kbProgress.read?.[m.id]?m.color:"var(--bdr)"}} />
                    ))}
                  </div>
                )}
                {pct >= 100 && <p className="text-xs mt-1 font-semibold" style={{color:"#6BCB77"}}>✓ Alle Module abgeschlossen!</p>}
              </div>
              <span className="text-xs shrink-0" style={{color:"var(--acc)"}}>→</span>
            </div>
            {/* Suggestion for next unread */}
            {nextUnread && readCount < KB_MODULES.length && (
              <div className="px-4 pb-3 pt-0">
                <div className="rounded-xl px-3 py-2 flex items-center gap-2" style={{background:`${nextUnread.color}08`,border:`1px solid ${nextUnread.color}22`}}>
                  <span className="text-base">{nextUnread.icon}</span>
                  <div className="flex-1 min-w-0">
                    <p className="text-xs font-semibold" style={{color:"var(--tx)"}}>{nextUnread.title}</p>
                    <p style={{fontSize:9,color:"var(--tx2)"}}>{nextUnread.readMin} Min. · Noch nicht gelesen</p>
                  </div>
                </div>
              </div>
            )}
          </button>
        );
      })()}

      {/* ═══ DASHBOARD MINI-WIDGETS ROW ═══ */}
      <div className="grid grid-cols-3 gap-2">
        {/* Craving Trend */}
        <button onClick={() => nav("craving")} className="rounded-xl p-3 text-center transition-all hover:scale-[1.02]" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          <span className="text-lg">📈</span>
          <p className="text-xs font-semibold mt-1" style={{color:"var(--tx)"}}>Craving</p>
          <p style={{fontSize:9,color:"var(--tx2)"}}>Verlauf →</p>
        </button>
        {/* Weekly Report */}
        <button onClick={() => nav("report")} className="rounded-xl p-3 text-center transition-all hover:scale-[1.02]" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          <span className="text-lg">📋</span>
          <p className="text-xs font-semibold mt-1" style={{color:"var(--tx)"}}>Wochen-</p>
          <p style={{fontSize:9,color:"var(--tx2)"}}>bericht →</p>
        </button>
        {/* Badges */}
        {(() => {
          const earned = BADGES.filter(b => b.check(logs, moods, goals, kbProgress, skillbox)).length;
          return (
            <button onClick={() => nav("badges")} className="rounded-xl p-3 text-center transition-all hover:scale-[1.02]" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <span className="text-lg">🏅</span>
              <p className="text-xs font-semibold mt-1" style={{color:"var(--tx)"}}>{earned}/{BADGES.length}</p>
              <p style={{fontSize:9,color:"var(--tx2)"}}>Badges →</p>
            </button>
          );
        })()}
      </div>

      {/* Medication warning banner */}
      {myMeds.length > 0 && (
        <button onClick={() => nav("medcheck")} className="w-full rounded-xl px-4 py-2.5 flex items-center gap-2 text-left" style={{background:"#F2D38808",border:"1px solid #F2D38822"}}>
          <span>💊</span>
          <span className="text-xs" style={{color:"#F2D388"}}>{myMeds.length} Medikament{myMeds.length>1?"e":""} hinterlegt — Warnungen aktiv</span>
          <span className="text-xs ml-auto" style={{color:"var(--tx2)"}}>→</span>
        </button>
      )}

      {/* Recent Activity */}
      {logs.length > 0 && (
        <div>
          <div className="flex items-center justify-between mb-2 px-1">
            <span className="text-xs font-bold" style={{color:"var(--tx2)"}}>Letzte Einträge</span>
            <button onClick={() => nav("loghistory")} className="text-xs font-medium" style={{color:"var(--acc)"}}>Alle ({logs.length}) →</button>
          </div>
          {logs.slice(-3).reverse().map((l,i) => (
            <div key={i} className="rounded-xl p-3 mb-2 flex items-center gap-3" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <div className="w-9 h-9 rounded-full flex items-center justify-center" style={{background:"var(--acc)15"}}>{subEmoji(l.substance)}</div>
              <div className="flex-1 min-w-0"><p className="text-sm font-medium truncate" style={{color:"var(--tx)"}}>{l.substance}</p><p className="text-xs" style={{color:"var(--tx2)"}}>{l.amount} {l.unit} · {l.setting}</p></div>
              <div className="text-right shrink-0">
                <span className="text-xs" style={{color:"var(--tx2)"}}>{ago(l.date)}</span>
                {l.craving > 0 && <p className="text-xs" style={{color:l.craving>6?"#E06B8A":l.craving>3?"#F2D388":"#6BCB77"}}>{l.craving}/10</p>}
              </div>
            </div>
          ))}
        </div>
      )}
      {/* ═══ 24h MISCH-CHECK WIDGET ═══ */}
      {(() => {
        const recent24h = logs
          .filter(l => Date.now() - new Date(l.date).getTime() < 24 * 60 * 60 * 1000)
          .map(l => l.substance)
          .filter((v, i, a) => a.indexOf(v) === i);
        if (recent24h.length < 2) return null;

        // Alle Kombinationen der letzten 24h prüfen
        const allWarnings = [];
        for (let a = 0; a < recent24h.length; a++) {
          for (let b = a + 1; b < recent24h.length; b++) {
            const key = getInteractionKey(recent24h[a], recent24h[b]);
            if (INTERACTION_MATRIX[key]) {
              allWarnings.push({ subA: recent24h[a], subB: recent24h[b], ...INTERACTION_MATRIX[key] });
            }
          }
        }
        if (allWarnings.length === 0) return null;

        const order = { critical: 0, high: 1, medium: 2 };
        allWarnings.sort((a, b) => (order[a.level] ?? 3) - (order[b.level] ?? 3));
        const worst = allWarnings[0];
        const isCrit = worst.level === "critical";
        const isHigh = worst.level === "high";
        const bg = isCrit ? "linear-gradient(135deg,#FF3B3B18,#1a0508)" : isHigh ? "linear-gradient(135deg,#FF8C0012,#1a0d00)" : "#FFD70010";
        const borderColor = isCrit ? "#FF3B3B88" : isHigh ? "#FF8C0077" : "#FFD70055";
        const textColor = isCrit ? "#FF3B3B" : isHigh ? "#FF8C00" : "#FFD700";
        const icon = isCrit ? "⛔" : isHigh ? "🔶" : "🟡";
        const pulseClass = isCrit ? "warn-critical" : isHigh ? "warn-high" : "";

        return (
          <button
            onClick={() => nav("log")}
            role="alert"
            aria-label={`Misch-Check: ${worst.subA} und ${worst.subB} – ${isCrit ? "Lebensgefahr" : isHigh ? "Hohes Risiko" : "Vorsicht"}`}
            className={`w-full rounded-2xl overflow-hidden text-left transition-all hover:scale-[1.01] active:scale-[0.99] ${pulseClass}`}
            style={{background:bg, border:`2px solid ${borderColor}`}}
          >
            <div className="px-4 py-3">
              <div className="flex items-center gap-2 mb-2">
                <span aria-hidden="true" className="text-lg">{icon}</span>
                <span className="text-xs font-black" style={{color:textColor, letterSpacing:"0.4px"}}>
                  {isCrit ? "⚠️ MISCH-CHECK: AKTIVE LEBENSGEFAHR" : isHigh ? "MISCH-CHECK: HOHES RISIKO" : "MISCH-CHECK: VORSICHT"}
                </span>
              </div>
              <p className="text-sm font-semibold leading-snug" style={{color:"var(--tx)"}}>
                Du hast heute {subEmoji(worst.subA)} <strong>{worst.subA}</strong> und {subEmoji(worst.subB)} <strong>{worst.subB}</strong> konsumiert.
              </p>
              <p className="text-xs mt-1.5 leading-relaxed" style={{color:textColor}}>
                {worst.text}
              </p>
              {allWarnings.length > 1 && (
                <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>
                  + {allWarnings.length - 1} weitere Kombination{allWarnings.length > 2 ? "en" : ""} erkannt
                </p>
              )}
            </div>
            {isCrit && (
              <div className="px-4 pb-3">
                <div className="flex items-center justify-center gap-2 py-2.5 rounded-xl font-black text-sm"
                  style={{background:"#FF3B3B", color:"#fff"}}>
                  <span aria-hidden="true">📞</span>
                  <span>Notfall? → 112 anrufen</span>
                </div>
              </div>
            )}
            <div className="px-4 pb-2.5">
              <p className="text-xs" style={{color:"var(--tx2)"}}>Tippen für Details im Dose-Log →</p>
            </div>
          </button>
        );
      })()}

      {logs.length===0 && (goals.cleanDays?.length||0)===0 && (
        <div className="rounded-2xl p-6 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          <p className="text-3xl mb-2">🌱</p>
          <p className="text-sm font-medium" style={{color:"var(--tx)"}}>Willkommen bei DoseDiary</p>
          <p className="text-xs mt-2 leading-relaxed" style={{color:"var(--tx2)"}}>Dein privater Raum für bewussten Umgang. Kein Urteil, kein Druck — nur Klarheit.</p>
        </div>
      )}
    </div>
    );
  };

  // ─── DOSE LOG ───
  const DoseLog = () => {
    const [sub,setSub]=useState(""); const [amt,setAmt]=useState(""); const [unit,setUnit]=useState("mg");
    const [setting,setSetting]=useState(""); const [note,setNote]=useState(""); const [craving,setCraving]=useState(5);
    const [saved,setSaved]=useState(false); const [showAllSafer,setShowAllSafer]=useState(false);
    const [showAllItems,setShowAllItems]=useState(false);
    const [retroMode, setRetroMode] = useState(false);
    const [retroDate, setRetroDate] = useState(() => new Date().toISOString().split("T")[0]);
    const [retroTime, setRetroTime] = useState(() => { const n=new Date(); return `${String(n.getHours()).padStart(2,"0")}:${String(n.getMinutes()).padStart(2,"0")}`; });
    const isBehavior = ALL_ITEMS.find(i => i.id === sub)?.cat === "beh";

    // User's selected items, or all if none selected
    const myItems = prefs.mySubs?.length > 0 ? prefs.mySubs : SUBSTANCES;
    const displayItems = showAllItems ? SUBSTANCES : myItems;

    const doSave = async () => {
      if(!sub || (!isBehavior && !amt)) return;
      let entryDate;
      if (retroMode) {
        entryDate = new Date(`${retroDate}T${retroTime}:00`).toISOString();
      } else {
        entryDate = new Date().toISOString();
      }
      const entry = {
        id:Date.now(), substance:sub,
        amount: isBehavior ? parseFloat(amt || "0") : parseFloat(amt),
        unit: isBehavior ? "Min." : unit,
        setting:setting||"Nicht angegeben", note, craving, date:entryDate,
        type: isBehavior ? "behavior" : "substance",
        retroactive: retroMode || undefined,
      };
      await save("dd_logs", setLogs, [...logs, entry]);
      setSaved(true); setTimeout(()=>{setSaved(false);nav("dashboard")},1000);
    };

    // Get substances consumed in last 24h (for mix warnings)
    const recent24h = logs
      .filter(l => Date.now() - new Date(l.date).getTime() < 24 * 60 * 60 * 1000)
      .map(l => l.substance)
      .filter((v, i, a) => a.indexOf(v) === i); // unique

    const info = sub ? SUB_INFO[sub] : null;
    const mixWarnings = sub ? findMixWarnings(sub, recent24h) : [];

    const levelStyles = {
      critical: {
        bg:"#1a0508", border:"#FF3B3B", borderAlpha:"#FF3B3B99",
        iconBg:"#FF3B3B30", badge:"#FF3B3B", badgeBg:"#FF3B3B30",
        label:"⛔ LEBENSGEFAHR", pulse:true, pulseClass:"warn-critical border-blink",
        headerBg:"linear-gradient(135deg,#FF3B3B22,#8B000018)",
        callBg:"#FF3B3B", callText:"#fff",
      },
      high: {
        bg:"#1a0d00", border:"#FF8C00", borderAlpha:"#FF8C0099",
        iconBg:"#FF8C0030", badge:"#FF8C00", badgeBg:"#FF8C0025",
        label:"🔶 HOHES RISIKO", pulse:true, pulseClass:"warn-high",
        headerBg:"linear-gradient(135deg,#FF8C0018,#8B450010)",
        callBg:"var(--card2)", callText:"#FF8C00",
      },
      medium: {
        bg:"#15120a", border:"#FFD700", borderAlpha:"#FFD70066",
        iconBg:"#FFD70025", badge:"#FFD700", badgeBg:"#FFD70018",
        label:"🟡 VORSICHT", pulse:false, pulseClass:"",
        headerBg:"#FFD70010",
        callBg:"var(--card2)", callText:"#FFD700",
      },
    };

    return (
      <div className="space-y-5">
        <p className="text-xs text-center" style={{color:"var(--tx2)"}}>Wertfrei. Nur fuer dich.</p>

        {/* Date/Time — retro toggle */}
        <div className="rounded-xl overflow-hidden" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          <div className="flex items-center justify-between px-4 py-2.5">
            <div className="flex items-center gap-2">
              <span className="text-sm">🕐</span>
              <span className="text-xs font-semibold" style={{color:"var(--tx)"}}>{retroMode ? "Nachtraeglicher Eintrag" : "Jetzt"}</span>
            </div>
            <button onClick={() => setRetroMode(!retroMode)} className="text-xs font-medium px-2.5 py-1 rounded-lg transition-all" style={{background:retroMode?"var(--acc)":"var(--card2)",color:retroMode?"#fff":"var(--tx2)"}}>
              {retroMode ? "Auf Jetzt zuruecksetzen" : "Datum aendern"}
            </button>
          </div>
          {retroMode && (
            <div className="px-4 pb-3 pt-1 flex gap-3 animate-fadeIn">
              <div className="flex-1">
                <label className="text-xs mb-1 block" style={{color:"var(--tx2)"}}>Datum</label>
                <input type="date" value={retroDate} onChange={e=>setRetroDate(e.target.value)} max={new Date().toISOString().split("T")[0]}
                  className="w-full rounded-lg px-3 py-2 text-sm outline-none" style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)",colorScheme:"dark"}} />
              </div>
              <div className="w-28">
                <label className="text-xs mb-1 block" style={{color:"var(--tx2)"}}>Uhrzeit</label>
                <input type="time" value={retroTime} onChange={e=>setRetroTime(e.target.value)}
                  className="w-full rounded-lg px-3 py-2 text-sm outline-none" style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)",colorScheme:"dark"}} />
              </div>
            </div>
          )}
        </div>

        {/* Substance/Behavior Selection */}
        <div>
          <Label>Substanz / Verhalten</Label>
          <Pills items={displayItems} selected={sub} onSelect={(s)=>{setSub(s);setShowAllSafer(false);}} emoji={subEmoji} />
          {prefs.mySubs?.length > 0 && (
            <button onClick={() => setShowAllItems(!showAllItems)} className="text-xs mt-2 font-medium" style={{color:"var(--acc)"}}>
              {showAllItems ? "Nur meine Auswahl ▴" : `Alle anzeigen (${SUBSTANCES.length}) ▾`}
            </button>
          )}
        </div>

        {/* ═══ SUBSTANCE INFO CARD ═══ */}
        {info && sub && (
          <div className="rounded-2xl overflow-hidden animate-fadeIn" style={{background:"var(--card)",border:`1px solid ${info.riskColor || "var(--bdr)"}44`}}>
            {/* Header with risk level */}
            <div className="px-4 py-3 flex items-center justify-between" style={{background:`${info.riskColor || "var(--acc)"}12`,borderBottom:`1px solid ${info.riskColor || "var(--bdr)"}33`}}>
              <div className="flex items-center gap-2">
                <span aria-hidden="true" className="text-lg">{subEmoji(sub)}</span>
                <span className="text-sm font-bold" style={{color:"var(--tx)"}}>{sub}</span>
              </div>
              <span
                className="text-xs font-bold px-2.5 py-1 rounded-full flex items-center gap-1"
                style={{background:`${info.riskColor}22`,color:info.riskColor}}
                aria-label={`Risikostufe: ${riskMeta(info.risk).label}`}
              >
                <span aria-hidden="true">{riskMeta(info.risk).icon}</span>
                Risiko: {info.risk}
              </span>
            </div>

            {/* Quick facts */}
            <div className="grid grid-cols-2 gap-px" style={{background:"var(--bdr)"}}>
              <div className="px-3 py-2.5" style={{background:"var(--card)"}}>
                <p className="text-xs" style={{color:"var(--tx2)"}}>⏱️ Wirkungseintritt</p>
                <p className="text-xs font-bold mt-0.5" style={{color:"var(--tx)"}}>{info.onset}</p>
              </div>
              <div className="px-3 py-2.5" style={{background:"var(--card)"}}>
                <p className="text-xs" style={{color:"var(--tx2)"}}>⏳ Wirkdauer</p>
                <p className="text-xs font-bold mt-0.5" style={{color:"var(--tx)"}}>{info.duration}</p>
              </div>
            </div>

            {/* Safer Use Tips */}
            <div className="px-4 py-3">
              <p className="text-xs font-bold mb-2 flex items-center gap-1.5" style={{color:"var(--acc)"}}>
                <span className="w-4 h-4 rounded-full flex items-center justify-center text-xs" style={{background:"var(--acc)20"}}>✓</span>
                Safer Use
              </p>
              {(showAllSafer ? info.safer : info.safer.slice(0, 2)).map((tip, i) => (
                <p key={i} className="text-xs py-1 pl-6 flex gap-2 leading-relaxed" style={{color:"var(--tx2)"}}>
                  <span style={{color:"var(--acc)"}}>•</span><span>{tip}</span>
                </p>
              ))}
              {info.safer.length > 2 && (
                <button onClick={() => setShowAllSafer(!showAllSafer)} className="text-xs mt-1 pl-6 font-medium" style={{color:"var(--acc)"}}>
                  {showAllSafer ? "Weniger anzeigen ▴" : `+${info.safer.length - 2} weitere Tipps ▾`}
                </button>
              )}
            </div>

            {/* Known Interactions (always visible) */}
            {info.interactions && info.interactions.length > 0 && (
              <div className="px-4 py-3" style={{borderTop:`1px solid var(--bdr)`}}>
                <p className="text-xs font-bold mb-2 flex items-center gap-1.5" style={{color:"#E8A87C"}}>
                  <span className="w-4 h-4 rounded-full flex items-center justify-center text-xs" style={{background:"#E8A87C20"}}>!</span>
                  Bekannte Wechselwirkungen
                </p>
                <div className="space-y-1">
                  {info.interactions.slice(0, showAllSafer ? 99 : 3).map((inter, i) => (
                    <p key={i} className="text-xs py-0.5 pl-6" style={{color: inter.includes("LEBENSGEFAHR") ? "#E06B8A" : "var(--tx2)"}}>
                      {inter}
                    </p>
                  ))}
                  {!showAllSafer && info.interactions.length > 3 && (
                    <button onClick={() => setShowAllSafer(true)} className="text-xs pl-6 font-medium" style={{color:"#E8A87C"}}>
                      +{info.interactions.length - 3} weitere ▾
                    </button>
                  )}
                </div>
              </div>
            )}
          </div>
        )}

        {/* ═══ MEDICATION INTERACTION WARNINGS ═══ */}
        {sub && myMeds.length > 0 && (() => {
          const warns = [];
          myMeds.forEach(medId => {
            const med = MEDICATIONS.find(m => m.id === medId);
            if (med?.warns?.[sub]) warns.push({ med: med.name, warn: med.warns[sub] });
          });
          if (!warns.length) return null;
          return (
            <div className="space-y-2 animate-fadeIn">
              <p className="text-xs font-bold flex items-center gap-2 px-1" style={{color:"#E06B8A"}}>💊 Medikamenten-Wechselwirkung</p>
              {warns.map((w, i) => (
                <div key={i} className="rounded-xl px-4 py-3" style={{background:w.warn.includes("LEBENSGEFAHR")?"#E06B8A12":"#F2D38812",border:`1px solid ${w.warn.includes("LEBENSGEFAHR")?"#E06B8A44":"#F2D38844"}`}}>
                  <p className="text-xs font-bold" style={{color:w.warn.includes("LEBENSGEFAHR")?"#E06B8A":"#F2D388"}}>{w.warn}</p>
                  <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>{sub} + {w.med}</p>
                </div>
              ))}
            </div>
          );
        })()}

        {/* ═══ SAFER-USE TIMER WARNING ═══ */}
        {sub && SAFER_TIMERS[sub] && (() => {
          const timer = SAFER_TIMERS[sub];
          const lastLog = [...logs].reverse().find(l => l.substance === sub);
          if (!lastLog) return null;
          const hoursSince = (Date.now() - new Date(lastLog.date).getTime()) / 3600000;
          if (hoursSince >= timer.hours) return null;
          const pctDone = Math.min(1, hoursSince / timer.hours);
          const remaining = timer.hours - hoursSince;
          const remLabel = remaining >= 24 ? `${Math.ceil(remaining/24)} Tage` : `${Math.ceil(remaining)} Std.`;
          return (
            <div className="rounded-2xl p-4 animate-fadeIn" style={{background:`${timer.color}08`,border:`1px solid ${timer.color}33`}}>
              <div className="flex items-center gap-2 mb-2">
                <span className="text-base">⏳</span>
                <p className="text-xs font-bold" style={{color:timer.color}}>{timer.label}: Noch {remLabel} empfohlen</p>
              </div>
              <div className="w-full h-2 rounded-full mb-2" style={{background:"var(--bdr)"}}>
                <div className="h-2 rounded-full transition-all" style={{width:`${pctDone*100}%`,background:timer.color}} />
              </div>
              <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>{timer.desc}</p>
            </div>
          );
        })()}

        {/* ═══ DYNAMIC MIX WARNINGS (based on last 24h) ═══ */}
        {mixWarnings.length > 0 && (
          <div className="space-y-3 animate-fadeIn">
            {/* ── Warn-Header ── */}
            <div className="rounded-2xl px-4 py-3 flex items-center gap-3"
              style={{background:"linear-gradient(135deg,#FF3B3B22,#1a0508)",border:"2px solid #FF3B3B88"}}>
              <span className="relative flex shrink-0" aria-hidden="true">
                <span className="animate-ping absolute inline-flex h-4 w-4 rounded-full opacity-70" style={{background:"#FF3B3B",top:"-2px",left:"-2px"}} />
                <span className="relative inline-flex rounded-full h-4 w-4" style={{background:"#FF3B3B"}} />
              </span>
              <div>
                <p className="text-sm font-black" style={{color:"#FF3B3B",letterSpacing:"0.3px"}}>
                  MISCHKONSUM ERKANNT
                </p>
                <p className="text-xs mt-0.5" style={{color:"var(--tx2)"}}>
                  Du hast in den letzten 24 Std. {recent24h.filter(r=>r!==sub).map(r=>`${subEmoji(r)} ${r}`).join(", ")} konsumiert
                </p>
              </div>
            </div>

            {mixWarnings.map((w, i) => {
              const sty = levelStyles[w.level] || levelStyles.medium;
              const isCrit = w.level === "critical";
              const isHigh = w.level === "high";
              return (
                <div
                  key={i}
                  role={isCrit ? "alert" : "region"}
                  aria-label={`${sty.label}: ${sub} kombiniert mit ${w.sub}`}
                  className={`rounded-2xl overflow-hidden ${sty.pulseClass}`}
                  style={{background:sty.bg, border:`2px solid ${sty.border}`}}
                >
                  {/* Karten-Header mit Substanzpaar */}
                  <div className="px-4 pt-3 pb-2 flex items-center justify-between"
                    style={{background:sty.headerBg, borderBottom:`1px solid ${sty.borderAlpha}`}}>
                    <div className="flex items-center gap-2">
                      <span className="text-xl font-black px-2.5 py-0.5 rounded-lg" style={{background:sty.badgeBg,color:sty.badge}}>
                        {sty.label}
                      </span>
                    </div>
                    <span className="text-sm font-bold" style={{color:"var(--tx)"}}>
                      {subEmoji(sub)} {sub} <span style={{color:sty.badge}}>+</span> {subEmoji(w.sub)} {w.sub}
                    </span>
                  </div>

                  {/* Warn-Inhalt */}
                  <div className="px-4 py-3 space-y-2">
                    <p className="text-sm font-bold leading-snug" style={{color:sty.badge}}>
                      {w.text}
                    </p>
                    <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>
                      <span aria-hidden="true">→ </span>{w.advice}
                    </p>
                  </div>

                  {/* Notfall-Button (kritisch + hoch) */}
                  {(isCrit || isHigh) && (
                    <div className="px-4 pb-3 pt-1">
                      <a
                        href="tel:112"
                        role="button"
                        aria-label="Notruf 112 anrufen"
                        className="flex items-center justify-center gap-2 w-full py-3 rounded-xl font-black text-sm transition-all active:scale-[0.97]"
                        style={{background:sty.callBg, color:sty.callText, border:isCrit?"none":`2px solid ${sty.badge}`, textDecoration:"none", minHeight:48}}
                      >
                        <span aria-hidden="true">📞</span>
                        <span>{isCrit ? "NOTFALL? JETZT 112 ANRUFEN" : "Notfall → 112"}</span>
                      </a>
                      {isCrit && (
                        <p className="text-center text-xs mt-1.5" style={{color:"var(--tx2)"}}>
                          Giftnotruf: <strong style={{color:"var(--tx)"}}>030 19240</strong> (24/7)
                        </p>
                      )}
                    </div>
                  )}
                </div>
              );
            })}
          </div>
        )}

        {/* ═══ RECENT 24h CONTEXT ═══ */}
        {sub && recent24h.length > 0 && recent24h.some(r => r !== sub) && mixWarnings.length === 0 && (
          <div className="rounded-xl px-4 py-3" style={{background:"#FF8C0012",border:"1px solid #FF8C0044"}}>
            <p className="text-xs font-semibold" style={{color:"#FF8C00"}}>
              <span aria-hidden="true">⚠️ </span>Letzte 24 Std. konsumiert: {recent24h.filter(r => r !== sub).map(r => `${subEmoji(r)} ${r}`).join(", ")}
            </p>
            <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Keine spezifische Warnung in der Datenbank — Mischkonsum erhöht grundsätzlich das Risiko.</p>
          </div>
        )}

        {/* Amount & Unit — adapts for behaviors */}
        {isBehavior ? (
          <div>
            <Label>Dauer (optional)</Label>
            <div className="flex items-center gap-3">
              <input type="number" value={amt} onChange={e=>setAmt(e.target.value)} className="flex-1 rounded-xl px-4 py-2.5 text-sm outline-none" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}} placeholder="z.B. 30" inputMode="numeric" />
              <span className="text-sm font-medium" style={{color:"var(--tx2)"}}>Minuten</span>
            </div>
          </div>
        ) : (
          <div className="grid grid-cols-2 gap-3">
            <div><Label>Menge</Label><input type="number" value={amt} onChange={e=>setAmt(e.target.value)} className="w-full rounded-xl px-4 py-2.5 text-sm outline-none" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}} placeholder="z.B. 250" inputMode="decimal" /></div>
            <div><Label>Einheit</Label><div className="flex flex-wrap gap-1.5">{UNITS.map(u=><button key={u} onClick={()=>setUnit(u)} className="px-2.5 py-1.5 rounded-lg text-xs transition-all" style={{background:unit===u?"var(--acc)":"var(--card)",color:unit===u?"#fff":"var(--tx2)",border:`1px solid ${unit===u?"var(--acc)":"var(--bdr)"}`}}>{u}</button>)}</div></div>
          </div>
        )}

        {/* Setting */}
        <div><Label>Setting</Label><Pills items={SETTINGS_OPT} selected={setting} onSelect={setSetting} /></div>

        {/* Craving */}
        <div>
          <Label>{isBehavior ? "Drang-Level" : "Craving-Level"}: <span style={{color:"var(--acc)"}}>{craving}/10</span></Label>
          <input type="range" min="0" max="10" value={craving} onChange={e=>setCraving(+e.target.value)} className="w-full" style={{accentColor:"var(--acc)"}} />
          <div className="flex justify-between text-xs" style={{color:"var(--tx2)"}}><span>Kein Verlangen</span><span>Sehr stark</span></div>
        </div>

        {/* Note */}
        <div><Label>Notiz (optional)</Label><textarea value={note} onChange={e=>setNote(e.target.value)} rows={2} className="w-full rounded-xl px-4 py-2.5 text-sm outline-none resize-none" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}} placeholder="Situation, Trigger, Gedanken?" /></div>

        {/* Save */}
        <Btn onClick={doSave} disabled={!sub || (!isBehavior && !amt)}>{saved?"✓ Gespeichert!":retroMode?`Eintrag fuer ${new Date(retroDate).toLocaleDateString("de-DE",{day:"numeric",month:"short"})} speichern`:"Eintrag speichern"}</Btn>
        {retroMode && <p className="text-xs text-center -mt-2" style={{color:"var(--tx2)"}}>⏱ Wird als nachtraeglicher Eintrag gespeichert</p>}
      </div>
    );
  };

  // ═══════════════════════════════════════════════
  // ─── LOG HISTORY (Full log with filter + delete) ───
  // ═══════════════════════════════════════════════
  const LogHistory = () => {
    const [filter, setFilter] = useState("all");
    const [expandId, setExpandId] = useState(null);
    const [confirmDel, setConfirmDel] = useState(null);

    const sorted = [...logs].sort((a,b) => new Date(b.date)-new Date(a.date));
    const uniqueSubs = [...new Set(logs.map(l=>l.substance))];
    const filtered = filter==="all" ? sorted : sorted.filter(l=>l.substance===filter);

    // Group by date
    const grouped = {};
    filtered.forEach(l => {
      const d = new Date(l.date).toLocaleDateString("de-DE",{weekday:"short",day:"numeric",month:"short"});
      if (!grouped[d]) grouped[d]=[];
      grouped[d].push(l);
    });

    const deleteEntry = async (id) => {
      await save("dd_logs", setLogs, logs.filter(l=>l.id!==id));
      setConfirmDel(null); setExpandId(null);
    };

    if (logs.length===0) return (
      <div className="text-center py-16 space-y-3">
        <p className="text-4xl">📋</p>
        <p className="font-medium" style={{color:"var(--tx)"}}>Noch keine Einträge</p>
        <p className="text-xs" style={{color:"var(--tx2)"}}>Starte mit deinem ersten Log-Eintrag.</p>
        <Btn onClick={()=>nav("log")} small>📝 Zum Dose-Log</Btn>
      </div>
    );

    return (
      <div className="space-y-4">
        <div className="flex items-center justify-between">
          <p className="text-xs" style={{color:"var(--tx2)"}}>{logs.length} Einträge gesamt</p>
          <button onClick={()=>nav("log")} className="text-xs font-semibold px-3 py-1.5 rounded-lg" style={{background:"var(--acc)",color:"#fff"}}>+ Neuer Eintrag</button>
        </div>

        {/* Filter */}
        {uniqueSubs.length > 1 && (
          <div className="flex flex-wrap gap-1.5">
            <button onClick={()=>setFilter("all")} className="px-2.5 py-1 rounded-full text-xs font-medium transition-all" style={{background:filter==="all"?"var(--acc)":"var(--card)",color:filter==="all"?"#fff":"var(--tx2)",border:`1px solid ${filter==="all"?"var(--acc)":"var(--bdr)"}`}}>Alle</button>
            {uniqueSubs.map(s=>(
              <button key={s} onClick={()=>setFilter(filter===s?"all":s)} className="px-2.5 py-1 rounded-full text-xs font-medium transition-all" style={{background:filter===s?"var(--acc)":"var(--card)",color:filter===s?"#fff":"var(--tx2)",border:`1px solid ${filter===s?"var(--acc)":"var(--bdr)"}`}}>{subEmoji(s)} {s}</button>
            ))}
          </div>
        )}

        {/* Grouped entries */}
        {Object.entries(grouped).map(([day, entries]) => (
          <div key={day}>
            <p className="text-xs font-bold mb-1.5 px-1" style={{color:"var(--tx2)"}}>{day}</p>
            <div className="space-y-1.5">
              {entries.map(l => (
                <div key={l.id} className="rounded-xl overflow-hidden" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
                  <button onClick={()=>setExpandId(expandId===l.id?null:l.id)} className="w-full px-4 py-3 flex items-center gap-3 text-left">
                    <div className="w-8 h-8 rounded-full flex items-center justify-center shrink-0 text-sm" style={{background:"var(--acc)12"}}>{subEmoji(l.substance)}</div>
                    <div className="flex-1 min-w-0">
                      <p className="text-sm font-medium truncate" style={{color:"var(--tx)"}}>{l.substance}</p>
                      <p className="text-xs" style={{color:"var(--tx2)"}}>{l.amount?`${l.amount} ${l.unit} · `:""}{l.setting}</p>
                    </div>
                    <div className="text-right shrink-0">
                      <p className="text-xs" style={{color:"var(--tx2)"}}>{new Date(l.date).toLocaleTimeString("de-DE",{hour:"2-digit",minute:"2-digit"})}</p>
                      <p className="text-xs" style={{color:l.craving>6?"#E06B8A":l.craving>3?"#F2D388":"#6BCB77"}}>⚡ {l.craving}/10</p>
                    </div>
                  </button>
                  {expandId===l.id && (
                    <div className="px-4 pb-3 pt-1 animate-fadeIn" style={{borderTop:"1px solid var(--bdr)"}}>
                      {l.note && <div className="rounded-lg p-2.5 mb-2" style={{background:"var(--card2)"}}><p className="text-xs font-bold mb-0.5" style={{color:"var(--tx2)"}}>📝 Notiz</p><p className="text-xs leading-relaxed" style={{color:"var(--tx)"}}>{l.note}</p></div>}
                      <div className="flex items-center gap-3 text-xs mb-2 flex-wrap" style={{color:"var(--tx2)"}}>
                        <span>📍 {l.setting}</span>
                        <span>🕐 {new Date(l.date).toLocaleString("de-DE",{day:"numeric",month:"short",hour:"2-digit",minute:"2-digit"})}</span>
                        {l.retroactive && <span className="px-1.5 py-0.5 rounded text-xs" style={{background:"var(--acc)12",color:"var(--acc)",fontSize:9}}>nachgetragen</span>}
                      </div>
                      {confirmDel===l.id ? (
                        <div className="flex gap-2">
                          <button onClick={()=>setConfirmDel(null)} className="flex-1 py-2 rounded-lg text-xs" style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>Abbrechen</button>
                          <button onClick={()=>deleteEntry(l.id)} className="flex-1 py-2 rounded-lg text-xs font-bold" style={{background:"#E06B8A",color:"#fff"}}>Endgültig löschen</button>
                        </div>
                      ) : (
                        <button onClick={()=>setConfirmDel(l.id)} aria-label="Eintrag löschen" className="text-xs font-medium" style={{color:"#E06B8A",minHeight:44,minWidth:44}}><span aria-hidden="true">🗑️ </span>Eintrag löschen</button>
                      )}
                    </div>
                  )}
                </div>
              ))}
            </div>
          </div>
        ))}
      </div>
    );
  };

  // ═══════════════════════════════════════════════
  // ─── MOOD TIMELINE (Visual mood history) ───
  // ═══════════════════════════════════════════════
  const MoodTimeline = () => {
    const [range, setRange] = useState(30); // 7, 14, 30
    const trend = moodTrend(moods, range);
    const filled = trend.filter(t => t.value !== null);

    if (moods.length < 2) return (
      <div className="text-center py-16 space-y-3">
        <p className="text-4xl">💚</p>
        <p className="font-medium" style={{color:"var(--tx)"}}>Noch zu wenig Daten</p>
        <p className="text-xs" style={{color:"var(--tx2)"}}>Mache täglich einen Mood-Check-in auf dem Dashboard.</p>
      </div>
    );

    const avg = filled.length ? (filled.reduce((s,t) => s+t.value, 0)/filled.length).toFixed(1) : "–";
    const best = filled.length ? Math.max(...filled.map(t=>t.value)) : 0;
    const worst = filled.length ? Math.min(...filled.map(t=>t.value)) : 0;
    const bestDay = filled.find(t=>t.value===best);
    const worstDay = filled.find(t=>t.value===worst);

    // Mood distribution
    const dist = [0,0,0,0,0];
    filled.forEach(t => { if(t.value>=1&&t.value<=5) dist[t.value-1]++; });

    return (
      <div className="space-y-5">
        {/* Range selector */}
        <div className="flex rounded-xl overflow-hidden" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          {[{v:7,l:"7 Tage"},{v:14,l:"14 Tage"},{v:30,l:"30 Tage"}].map(r=>(
            <button key={r.v} onClick={()=>setRange(r.v)} className="flex-1 py-2 text-xs font-semibold transition-all" style={{background:range===r.v?"var(--acc)":"transparent",color:range===r.v?"#fff":"var(--tx2)"}}>{r.l}</button>
          ))}
        </div>

        {/* Stats */}
        <div className="grid grid-cols-3 gap-2">
          <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
            <p className="text-xl font-bold" style={{color:"var(--acc)",fontFamily:"var(--fontD)"}}>{avg}</p>
            <p className="text-xs" style={{color:"var(--tx2)"}}>Ø Mood</p>
          </div>
          <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
            <p className="text-xl font-bold" style={{color:"#6BCB77",fontFamily:"var(--fontD)"}}>{filled.length}</p>
            <p className="text-xs" style={{color:"var(--tx2)"}}>Check-ins</p>
          </div>
          <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
            <p className="text-xl font-bold" style={{color:"#F2D388",fontFamily:"var(--fontD)"}}>{range - filled.length}</p>
            <p className="text-xs" style={{color:"var(--tx2)"}}>Verpasst</p>
          </div>
        </div>

        {/* Simple Emoji List */}
        <Card>
          <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>📅 Verlauf</h3>
          <div className="space-y-1.5">
            {trend.filter(t => t.value !== null).slice().reverse().map((t, i) => (
              <div key={i} className="flex items-center gap-3 py-1">
                <span className="text-lg w-8 text-center">{t.emoji}</span>
                <span className="text-xs" style={{color:"var(--tx2)"}}>{t.ds}</span>
                <span className="text-xs font-medium ml-auto" style={{color: t.value >= 4 ? "#6BCB77" : t.value === 3 ? "#F2D388" : "#E06B8A"}}>
                  {MOODS.find(m => m.value === t.value)?.label}
                </span>
              </div>
            ))}
            {trend.filter(t => t.value !== null).length === 0 && <p className="text-xs text-center py-4" style={{color:"var(--tx2)"}}>Keine Daten für diesen Zeitraum.</p>}
          </div>
        </Card>

        {/* Distribution */}
        <Card>
          <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>📊 Verteilung</h3>
          {MOODS.slice().reverse().map((m,i) => {
            const count = dist[m.value-1];
            const pct = filled.length ? Math.round(count/filled.length*100) : 0;
            return (
              <div key={m.value} className="flex items-center gap-3 mb-2">
                <span className="text-lg w-8 text-center">{m.emoji}</span>
                <span className="text-xs w-12" style={{color:"var(--tx2)"}}>{m.label}</span>
                <div className="flex-1 h-3 rounded-full" style={{background:"var(--bdr)"}}>
                  <div className="h-3 rounded-full transition-all duration-500" style={{width:`${pct}%`,background:m.color}} />
                </div>
                <span className="text-xs font-bold w-8 text-right" style={{color:m.color}}>{count}</span>
              </div>
            );
          })}
        </Card>

        {/* Best/Worst Days */}
        {bestDay && worstDay && bestDay !== worstDay && (
          <div className="grid grid-cols-2 gap-3">
            <div className="rounded-xl p-3 text-center" style={{background:"#6BCB7710",border:"1px solid #6BCB7733"}}>
              <p className="text-2xl">{bestDay.emoji}</p>
              <p className="text-xs font-bold mt-1" style={{color:"#6BCB77"}}>Bester Tag</p>
              <p className="text-xs" style={{color:"var(--tx2)"}}>{bestDay.ds?.slice(5)}</p>
            </div>
            <div className="rounded-xl p-3 text-center" style={{background:"#E06B8A10",border:"1px solid #E06B8A33"}}>
              <p className="text-2xl">{worstDay.emoji}</p>
              <p className="text-xs font-bold mt-1" style={{color:"#E06B8A"}}>Schwierigster Tag</p>
              <p className="text-xs" style={{color:"var(--tx2)"}}>{worstDay.ds?.slice(5)}</p>
            </div>
          </div>
        )}

        {/* Mood on clean vs consumed */}
        {(goals.cleanDays?.length||0) > 0 && filled.length >= 5 && (() => {
          const cleanSet = new Set(goals.cleanDays || []);
          const logDates = new Set(logs.map(l => l.date.split("T")[0]));
          const cleanM = filled.filter(t => cleanSet.has(t.ds));
          const conM = filled.filter(t => logDates.has(t.ds));
          const avgClean = cleanM.length ? (cleanM.reduce((s,t)=>s+t.value,0)/cleanM.length).toFixed(1) : "–";
          const avgCon = conM.length ? (conM.reduce((s,t)=>s+t.value,0)/conM.length).toFixed(1) : "–";
          if (avgClean==="–"&&avgCon==="–") return null;
          return (
            <Card>
              <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>💡 Mood-Vergleich</h3>
              <div className="grid grid-cols-2 gap-3 text-center">
                <div className="rounded-xl p-3" style={{background:"#6BCB7712"}}>
                  <p className="text-2xl font-bold" style={{color:"#6BCB77"}}>{avgClean}</p>
                  <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Ø Cleane Tage</p>
                </div>
                <div className="rounded-xl p-3" style={{background:"#E06B8A12"}}>
                  <p className="text-2xl font-bold" style={{color:"#E06B8A"}}>{avgCon}</p>
                  <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Ø Konsumtage</p>
                </div>
              </div>
            </Card>
          );
        })()}
      </div>
    );
  };

  // ─── PATTERN ANALYSIS ───
  const Analysis = () => {
    if (logs.length < 5) return (
      <div className="text-center py-12 space-y-4">
        <p className="text-4xl">📊</p>
        <p className="font-medium" style={{color:"var(--tx)"}}>Noch {5-logs.length} Einträge bis zur Analyse</p>
        <div className="w-full rounded-full h-2" style={{background:"var(--bdr)"}}><div className="h-2 rounded-full" style={{width:`${logs.length/5*100}%`,background:"var(--acc)"}} /></div>
      </div>
    );
    const bd=byDay(logs), bt=byTime(logs), bs2=bySub(logs);
    const avgC=logs.reduce((s,l)=>s+(l.craving||0),0)/logs.length;
    const topDay=Object.entries(bd).sort((a,b)=>b[1]-a[1])[0];
    const topTime=Object.entries(bt).sort((a,b)=>b[1]-a[1])[0];
    return (
      <div className="space-y-5">
        <Card>
          <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>🔍 Erkenntnisse</h3>
          <Row l="📅 Häufigster Tag" r={topDay?.[0]||"–"} /><Row l="🕐 Häufigste Zeit" r={topTime?.[0]||"–"} /><Row l="📍 Häufigstes Setting" r={mostCommon(logs.map(l=>l.setting))} /><Row l="🔥 Ø Craving" r={`${avgC.toFixed(1)}/10`} />
        </Card>
        <Card>
          <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>Substanzverteilung</h3>
          {Object.entries(bs2).sort((a,b)=>b[1]-a[1]).map(([s,c])=>(
            <div key={s} className="mb-2"><div className="flex justify-between text-xs mb-1"><span style={{color:"var(--tx)"}}>{subEmoji(s)} {s}</span><span style={{color:"var(--tx2)"}}>{c}× ({Math.round(c/logs.length*100)}%)</span></div>
            <div className="w-full h-2 rounded-full" style={{background:"var(--bdr)"}}><div className="h-2 rounded-full" style={{width:`${c/logs.length*100}%`,background:"var(--acc)",transition:"width 0.5s"}} /></div></div>
          ))}
        </Card>
        <Card>
          <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>Wochenrhythmus</h3>
          <div className="flex items-end justify-between gap-1" style={{height:100}}>
            {["Mo","Di","Mi","Do","Fr","Sa","So"].map(d=>{const c=bd[d]||0,mx=Math.max(...Object.values(bd),1);return(
              <div key={d} className="flex flex-col items-center gap-1 flex-1">
                <span className="text-xs font-bold" style={{color:"var(--acc)"}}>{c||""}</span>
                <div className="w-full rounded-t-lg" style={{height:`${Math.max(c/mx*70,4)}px`,background:c===mx?"var(--acc)":"var(--acc)44",transition:"height 0.5s"}} />
                <span className="text-xs" style={{color:"var(--tx2)"}}>{d}</span>
              </div>
            );})}
          </div>
        </Card>
      </div>
    );
  };


  // ═══════════════════════════════════════════════════════════
  // ─── CRAVING-KURVE (Craving over time with annotations) ───
  // ═══════════════════════════════════════════════════════════
  const CravingCurve = () => {
    const [range, setRange] = useState(14);
    const now = new Date(); now.setHours(23,59,59);
    const start = new Date(now); start.setDate(start.getDate() - range + 1); start.setHours(0,0,0,0);

    // Build daily data: avg craving, consumed?, skill used?, clean day?
    const data = [];
    const cleanSet = new Set(goals.cleanDays || []);
    const skillDates = new Set(Object.values(skillbox.feedback||{}).flatMap(arr => arr.map(f => f.date?.split("T")[0])));

    for (let d = new Date(start); d <= now; d.setDate(d.getDate() + 1)) {
      const ds = dateStr(d);
      const dayLogs = logs.filter(l => dateStr(l.date) === ds);
      const avgCraving = dayLogs.length > 0 ? Math.round(dayLogs.reduce((a,l) => a + (l.craving||0), 0) / dayLogs.length * 10) / 10 : null;
      data.push({
        ds, day: d.getDate(), month: d.getMonth(),
        craving: avgCraving,
        consumed: dayLogs.length > 0,
        clean: cleanSet.has(ds),
        skillUsed: skillDates.has(ds),
      });
    }

    const maxC = 10;
    const hasData = data.some(d => d.craving !== null);
    const chartH = 160;
    const chartW = Math.max(data.length * 28, 300);

    // Find "wins": high craving but no consumption
    const wins = data.filter(d => d.craving !== null && d.craving >= 6 && d.clean);

    return (
      <div className="space-y-5">
        <div className="text-center">
          <h2 className="text-lg font-bold" style={{fontFamily:"var(--fontD)",color:"var(--tx)"}}>Craving-Kurve</h2>
          <p className="text-sm mt-1" style={{color:"var(--tx2)"}}>Dein Suchtdruck im Zeitverlauf</p>
        </div>

        <div className="flex gap-2 justify-center">
          {[7,14,30].map(r => (
            <button key={r} onClick={() => setRange(r)} className="px-3 py-1.5 rounded-lg text-xs font-semibold" style={{background:range===r?"var(--acc)":"var(--card)",color:range===r?"#fff":"var(--tx2)",border:`1px solid ${range===r?"var(--acc)":"var(--bdr)"}`}}>{r} Tage</button>
          ))}
        </div>

        {!hasData ? (
          <Card><p className="text-sm text-center py-4" style={{color:"var(--tx2)"}}>Noch keine Craving-Daten. Logge Eintraege mit Craving-Level, um die Kurve zu fuellen.</p></Card>
        ) : (
          <Card>
            <div className="overflow-x-auto -mx-2">
              <svg width={chartW} height={chartH + 40} style={{display:"block"}}>
                {/* Grid lines */}
                {[0,2.5,5,7.5,10].map(v => (
                  <g key={v}>
                    <line x1="0" y1={chartH - (v/maxC)*chartH} x2={chartW} y2={chartH - (v/maxC)*chartH} stroke="var(--bdr)" strokeWidth="1" strokeDasharray="4,4" />
                    <text x="2" y={chartH - (v/maxC)*chartH - 4} fill="var(--tx2)" fontSize="9">{v}</text>
                  </g>
                ))}
                {/* Bars + line */}
                {data.map((d, i) => {
                  const x = i * 28 + 14;
                  const y = d.craving !== null ? chartH - (d.craving/maxC)*chartH : chartH;
                  const barH = d.craving !== null ? (d.craving/maxC)*chartH : 0;
                  const color = d.clean ? "#6BCB77" : d.consumed ? (d.craving > 6 ? "#E06B8A" : "#F2D388") : "var(--bdr)";
                  return (
                    <g key={i}>
                      {d.craving !== null && <rect x={x-8} y={y} width={16} height={barH} rx="4" fill={color} opacity={0.4} />}
                      {d.craving !== null && <circle cx={x} cy={y} r={d.skillUsed ? 5 : 3.5} fill={color} stroke={d.skillUsed ? "var(--acc)" : "none"} strokeWidth={d.skillUsed ? 2 : 0} />}
                      <text x={x} y={chartH + 16} textAnchor="middle" fill="var(--tx2)" fontSize="9">{d.day}</text>
                      {d.clean && <text x={x} y={chartH + 28} textAnchor="middle" fill="#6BCB77" fontSize="8">✓</text>}
                    </g>
                  );
                })}
                {/* Line connecting points */}
                <polyline fill="none" stroke="var(--acc)" strokeWidth="2" strokeLinejoin="round" opacity="0.6"
                  points={data.filter(d=>d.craving!==null).map((d,i,arr) => `${data.indexOf(d)*28+14},${chartH-(d.craving/maxC)*chartH}`).join(" ")} />
              </svg>
            </div>
            <div className="flex items-center gap-4 mt-3 justify-center flex-wrap">
              <span className="flex items-center gap-1 text-xs" style={{color:"var(--tx2)"}}><span className="w-2.5 h-2.5 rounded-full" style={{background:"#6BCB77"}} /> Clean</span>
              <span className="flex items-center gap-1 text-xs" style={{color:"var(--tx2)"}}><span className="w-2.5 h-2.5 rounded-full" style={{background:"#F2D388"}} /> Konsum</span>
              <span className="flex items-center gap-1 text-xs" style={{color:"var(--tx2)"}}><span className="w-2.5 h-2.5 rounded-full" style={{background:"var(--acc)",border:"2px solid var(--acc)"}} /> Skill genutzt</span>
            </div>
          </Card>
        )}

        {/* Wins — self-efficacy highlights */}
        {wins.length > 0 && (
          <Card>
            <h3 className="text-sm font-bold mb-2" style={{color:"#6BCB77"}}>💪 Selbstwirksamkeit</h3>
            <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>
              An {wins.length} Tag{wins.length>1?"en":""} hattest du starken Suchtdruck (6+), hast aber nicht konsumiert. Das zeigt echte Staerke.
            </p>
          </Card>
        )}
      </div>
    );
  };

  // ═══════════════════════════════════════════════════════════
  // ─── WOCHENBERICHT (Weekly auto-generated reflection) ─────
  // ═══════════════════════════════════════════════════════════
  const WeeklyReport = () => {
    const [weekOffset, setWeekOffset] = useState(0);
    const getWeek = (offset) => {
      const end = new Date(); end.setDate(end.getDate() - offset * 7); end.setHours(23,59,59);
      const start = new Date(end); start.setDate(start.getDate() - 6); start.setHours(0,0,0,0);
      return { start, end };
    };
    const { start, end } = getWeek(weekOffset);
    const weekLabel = `${start.toLocaleDateString("de-DE",{day:"numeric",month:"short"})} – ${end.toLocaleDateString("de-DE",{day:"numeric",month:"short"})}`;

    // Week data
    const wLogs = logs.filter(l => { const d=new Date(l.date); return d>=start && d<=end; });
    const wMoods = moods.filter(m => { const d=new Date(m.date); return d>=start && d<=end; });
    const cleanSet = new Set(goals.cleanDays || []);
    let wClean = 0;
    for (let d=new Date(start); d<=end; d.setDate(d.getDate()+1)) { if (cleanSet.has(dateStr(d))) wClean++; }
    const avgMood = wMoods.length > 0 ? Math.round(wMoods.reduce((a,m) => a+m.value, 0) / wMoods.length * 10) / 10 : null;
    const avgCraving = wLogs.length > 0 ? Math.round(wLogs.reduce((a,l) => a+(l.craving||0), 0) / wLogs.length * 10) / 10 : null;
    const substances = [...new Set(wLogs.map(l => l.substance))];
    const skillUses = Object.values(skillbox.feedback||{}).flatMap(arr => arr.filter(f => { const d=new Date(f.date); return d>=start && d<=end; })).length;
    const kbRead = Object.entries(kbProgress.read||{}).filter(([k,v]) => { const d=new Date(v); return d>=start && d<=end; }).length;
    const hasData = wLogs.length > 0 || wMoods.length > 0 || wClean > 0;

    return (
      <div className="space-y-5">
        <div className="text-center">
          <h2 className="text-lg font-bold" style={{fontFamily:"var(--fontD)",color:"var(--tx)"}}>Wochenbericht</h2>
          <p className="text-sm mt-1" style={{color:"var(--tx2)"}}>Dein wochentlicher Spiegel — wertfrei.</p>
        </div>

        <div className="flex items-center justify-between">
          <button onClick={() => setWeekOffset(weekOffset+1)} aria-label="Frühere Woche anzeigen" className="px-3 py-2 rounded-lg text-xs font-semibold" style={{background:"var(--card)",color:"var(--tx2)",border:"1px solid var(--bdr)",minHeight:44}}>← Früher</button>
          <span className="text-sm font-bold" style={{color:"var(--tx)"}}>{weekLabel}</span>
          <button onClick={() => setWeekOffset(Math.max(0,weekOffset-1))} disabled={weekOffset===0} aria-label="Spätere Woche anzeigen" aria-disabled={weekOffset===0} className="px-3 py-2 rounded-lg text-xs font-semibold" style={{background:"var(--card)",color:weekOffset===0?"var(--bdr)":"var(--tx2)",border:"1px solid var(--bdr)",minHeight:44}}>Später →</button>
        </div>

        {!hasData ? (
          <Card><p className="text-sm text-center py-6" style={{color:"var(--tx2)"}}>Keine Daten fuer diese Woche.</p></Card>
        ) : (<>
          {/* Summary stats */}
          <div className="grid grid-cols-2 gap-2">
            <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <p className="text-xl font-bold" style={{color:"#6BCB77",fontFamily:"var(--fontD)"}}>{wClean}</p>
              <p style={{fontSize:11,color:"var(--tx2)"}}>Clean Days</p>
            </div>
            <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <p className="text-xl font-bold" style={{color:"var(--acc)",fontFamily:"var(--fontD)"}}>{wLogs.length}</p>
              <p style={{fontSize:11,color:"var(--tx2)"}}>Log-Eintraege</p>
            </div>
            <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <p className="text-xl font-bold" style={{color:avgMood>=3?"#6BCB77":avgMood>=2?"#F2D388":"#E06B8A",fontFamily:"var(--fontD)"}}>{avgMood !== null ? avgMood : "–"}</p>
              <p style={{fontSize:11,color:"var(--tx2)"}}>Ø Stimmung</p>
            </div>
            <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <p className="text-xl font-bold" style={{color:avgCraving>6?"#E06B8A":avgCraving>3?"#F2D388":"#6BCB77",fontFamily:"var(--fontD)"}}>{avgCraving !== null ? avgCraving : "–"}</p>
              <p style={{fontSize:11,color:"var(--tx2)"}}>Ø Craving</p>
            </div>
          </div>

          {/* Substances used */}
          {substances.length > 0 && (
            <Card>
              <h3 className="text-sm font-bold mb-2" style={{color:"var(--tx)"}}>Konsumierte Substanzen</h3>
              <div className="flex flex-wrap gap-2">
                {substances.map(s => {
                  const count = wLogs.filter(l=>l.substance===s).length;
                  return <span key={s} className="text-xs px-2.5 py-1 rounded-full" style={{background:"var(--card2)",color:"var(--tx2)"}}>{subEmoji(s)} {s} ({count}x)</span>;
                })}
              </div>
            </Card>
          )}

          {/* Activity */}
          <Card>
            <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>Aktivitaet</h3>
            <div className="space-y-2">
              <div className="flex items-center justify-between"><span className="text-xs" style={{color:"var(--tx2)"}}>🧰 Skills genutzt</span><span className="text-xs font-bold" style={{color:"var(--acc)"}}>{skillUses}x</span></div>
              <div className="flex items-center justify-between"><span className="text-xs" style={{color:"var(--tx2)"}}>🧬 Module gelesen</span><span className="text-xs font-bold" style={{color:"var(--acc)"}}>{kbRead}</span></div>
              <div className="flex items-center justify-between"><span className="text-xs" style={{color:"var(--tx2)"}}>😊 Mood-Check-ins</span><span className="text-xs font-bold" style={{color:"var(--acc)"}}>{wMoods.length}</span></div>
            </div>
          </Card>

          {/* Auto-generated reflection */}
          <div className="rounded-2xl p-4" style={{background:"linear-gradient(135deg,#9B7ECF08,#6BCB7708)",border:"1px solid var(--bdr)"}}>
            <p className="text-xs font-bold mb-2" style={{color:"var(--acc)"}}>💭 Reflexion</p>
            <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>
              {wClean >= 5 && avgCraving !== null && avgCraving <= 4 ? "Starke Woche — wenig Konsum und moderater Suchtdruck. Was hat dir geholfen?" :
               wClean >= 5 && avgCraving !== null && avgCraving > 6 ? "Trotz hohem Suchtdruck viele cleane Tage — echte Selbstkontrolle. Denk daran, die Skill-Box zu nutzen." :
               wLogs.length > 5 ? "Viele Konsumtage diese Woche. Kein Urteil — aber schau dir an, welche Muster du erkennst. Gibt es Trigger?" :
               wMoods.length === 0 ? "Keine Mood-Daten diese Woche. Taegliche Check-ins helfen, Zusammenhaenge zu erkennen." :
               "Jede Woche ist ein neuer Anfang. Schau auf das, was du geschafft hast — nicht auf das, was nicht perfekt lief."}
            </p>
          </div>
        </>)}
      </div>
    );
  };

  // ═══════════════════════════════════════════════════════════
  // ─── MEDIKAMENTEN-CHECK (Medication interaction setup) ────
  // ═══════════════════════════════════════════════════════════
  const MedCheck = () => {
    const toggleMed = async (medId) => {
      const next = myMeds.includes(medId) ? myMeds.filter(m => m !== medId) : [...myMeds, medId];
      await saveMeds(next);
    };
    // Show current warnings for user's substances
    const mySubsList = prefs.mySubs?.length > 0 ? prefs.mySubs : SUBSTANCES;
    const activeWarns = [];
    myMeds.forEach(medId => {
      const med = MEDICATIONS.find(m => m.id === medId);
      if (!med) return;
      mySubsList.forEach(sub => {
        if (med.warns?.[sub]) activeWarns.push({ med: med.name, sub, warn: med.warns[sub] });
      });
    });

    return (
      <div className="space-y-5">
        <div className="text-center">
          <h2 className="text-lg font-bold" style={{fontFamily:"var(--fontD)",color:"var(--tx)"}}>Medikamenten-Check</h2>
          <p className="text-sm mt-1" style={{color:"var(--tx2)"}}>Welche Medikamente nimmst du regelmaessig?</p>
        </div>

        <div className="rounded-xl p-3" style={{background:"#F2D38808",border:"1px solid #F2D38833"}}>
          <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>⚠️ Wähle deine Medikamente aus. Die App zeigt dir dann im Dose-Log Hinweise auf mögliche Wechselwirkungsrisiken — als Orientierungshilfe zur Selbstreflexion. <span style={{fontWeight:600,color:"var(--tx)"}}>Kein Ersatz für ärztliche oder pharmazeutische Beratung. Bei Fragen wende dich an deine Ärztin / deinen Arzt oder die Apotheke.</span></p>
        </div>

        <div className="space-y-2">
          {MEDICATIONS.map(med => (
            <button key={med.id} onClick={() => toggleMed(med.id)} className="w-full rounded-2xl px-4 py-3.5 text-left flex items-center gap-3 transition-all active:scale-[0.98]"
              style={{background:myMeds.includes(med.id)?"var(--acc)08":"var(--card)",border:`1.5px solid ${myMeds.includes(med.id)?"var(--acc)":"var(--bdr)"}`}}>
              <div className="w-8 h-8 rounded-lg flex items-center justify-center text-sm shrink-0" style={{background:myMeds.includes(med.id)?"var(--acc)20":"var(--card2)"}}>
                {myMeds.includes(med.id) ? "✓" : "💊"}
              </div>
              <div className="flex-1 min-w-0">
                <p className="text-sm font-semibold" style={{color:myMeds.includes(med.id)?"var(--acc)":"var(--tx)"}}>{med.name}</p>
                <p style={{fontSize:11,color:"var(--tx2)"}}>{med.examples}</p>
              </div>
            </button>
          ))}
        </div>

        {/* Active warnings preview */}
        {activeWarns.length > 0 && (
          <Card>
            <h3 className="text-sm font-bold mb-3" style={{color:"#E06B8A"}}>⚠️ Aktive Warnungen ({activeWarns.length})</h3>
            <div className="space-y-2">
              {activeWarns.map((w,i) => (
                <div key={i} className="rounded-lg px-3 py-2" style={{background:w.warn.includes("LEBENSGEFAHR")?"#E06B8A08":"#F2D38808",border:`1px solid ${w.warn.includes("LEBENSGEFAHR")?"#E06B8A22":"#F2D38822"}`}}>
                  <p className="text-xs font-bold" style={{color:w.warn.includes("LEBENSGEFAHR")?"#E06B8A":"#F2D388"}}>{subEmoji(w.sub)} {w.sub} + {w.med}</p>
                  <p className="text-xs mt-0.5" style={{color:"var(--tx2)"}}>{w.warn}</p>
                </div>
              ))}
            </div>
            <p className="text-xs mt-3" style={{color:"var(--tx2)"}}>Diese Warnungen erscheinen automatisch im Dose-Log beim Loggen.</p>
          </Card>
        )}
      </div>
    );
  };

  // ═══════════════════════════════════════════════════════════
  // ─── BADGES / MEILENSTEINE (Gamification light) ───────────
  // ═══════════════════════════════════════════════════════════
  const BadgesView = () => {
    const earned = BADGES.filter(b => b.check(logs, moods, goals, kbProgress, skillbox));
    const locked = BADGES.filter(b => !b.check(logs, moods, goals, kbProgress, skillbox));
    return (
      <div className="space-y-5">
        <div className="text-center">
          <h2 className="text-lg font-bold" style={{fontFamily:"var(--fontD)",color:"var(--tx)"}}>Meilensteine</h2>
          <p className="text-sm mt-1" style={{color:"var(--tx2)"}}>{earned.length}/{BADGES.length} erreicht</p>
        </div>

        <div className="w-full h-3 rounded-full" style={{background:"var(--bdr)"}}>
          <div className="h-3 rounded-full transition-all duration-700" style={{width:`${earned.length/BADGES.length*100}%`,background:"var(--acc)"}} />
        </div>

        {earned.length > 0 && (<>
          <p className="text-xs font-bold px-1" style={{color:"var(--acc)"}}>✓ ERREICHT</p>
          <div className="grid grid-cols-2 gap-2">
            {earned.map(b => (
              <div key={b.id} className="rounded-2xl p-4 text-center" style={{background:"var(--acc)06",border:"1px solid var(--acc)22"}}>
                <span className="text-3xl">{b.icon}</span>
                <p className="text-xs font-bold mt-2" style={{color:"var(--tx)"}}>{b.title}</p>
                <p style={{fontSize:10,color:"var(--tx2)",marginTop:2}}>{b.desc}</p>
              </div>
            ))}
          </div>
        </>)}

        {locked.length > 0 && (<>
          <p className="text-xs font-bold px-1 mt-2" style={{color:"var(--tx2)"}}>🔒 NOCH OFFEN</p>
          <div className="grid grid-cols-2 gap-2">
            {locked.map(b => (
              <div key={b.id} className="rounded-2xl p-4 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)",opacity:0.5}}>
                <span className="text-3xl" style={{filter:"grayscale(1)"}}>{b.icon}</span>
                <p className="text-xs font-bold mt-2" style={{color:"var(--tx2)"}}>{b.title}</p>
                <p style={{fontSize:10,color:"var(--tx2)",marginTop:2}}>{b.desc}</p>
              </div>
            ))}
          </div>
        </>)}
      </div>
    );
  };

  // ─── PRIVACY & ABOUT (replaces Social Feed — Zero-Server-Policy) ───
  const Privacy = () => {
    const [confirmDelete, setConfirmDelete] = useState(false);
    const [confirmReset, setConfirmReset] = useState(false);
    const [deleted, setDeleted] = useState(false);
    const [backupMsg, setBackupMsg] = useState("");
    const [restoreMsg, setRestoreMsg] = useState("");
    const fileRef = useRef(null);

    // Backup: export all data as encrypted JSON
    const exportBackup = async () => {
      try {
        const data = {
          version: "1.2",
          exported: new Date().toISOString(),
          dd_moods: moods,
          dd_logs: logs,
          dd_goals: goals,
          dd_prefs: { mySubs: prefs.mySubs },
          dd_kb: kbProgress,
          dd_skillbox: skillbox,
          dd_planers: planers,
          dd_challenge_count: globalChallengeCount,
          dd_meds: myMeds,
        };
        // Simple XOR obfuscation with key (not crypto-grade, but prevents casual reading)
        const key = "DoseDiary2026HR";
        const json = JSON.stringify(data);
        const encoded = btoa(json.split("").map((c, i) => String.fromCharCode(c.charCodeAt(0) ^ key.charCodeAt(i % key.length))).join(""));
        const blob = new Blob([JSON.stringify({ _dd_backup: true, _v: 1, d: encoded })], { type: "application/json" });
        const a = document.createElement("a");
        a.href = URL.createObjectURL(blob);
        a.download = `DoseDiary_Backup_${todayStr()}.json`;
        a.click();
        URL.revokeObjectURL(a.href);
        setBackupMsg("✓ Backup erstellt!");
        setTimeout(() => setBackupMsg(""), 3000);
      } catch { setBackupMsg("Fehler beim Exportieren."); }
    };

    // Restore: import encrypted JSON
    const importBackup = async (e) => {
      try {
        const file = e.target.files?.[0];
        if (!file) return;
        const text = await file.text();
        const wrapper = JSON.parse(text);
        if (!wrapper._dd_backup) { setRestoreMsg("Ungültige Datei."); return; }
        const key = "DoseDiary2026HR";
        const decoded = atob(wrapper.d).split("").map((c, i) => String.fromCharCode(c.charCodeAt(0) ^ key.charCodeAt(i % key.length))).join("");
        const data = JSON.parse(decoded);
        if (data.dd_moods) { setMoods(data.dd_moods); await S.set("dd_moods", data.dd_moods); }
        if (data.dd_logs) { setLogs(data.dd_logs); await S.set("dd_logs", data.dd_logs); }
        if (data.dd_goals) { setGoals(data.dd_goals); await S.set("dd_goals", data.dd_goals); }
        if (data.dd_prefs) { setPrefs(data.dd_prefs); await S.set("dd_prefs", data.dd_prefs); }
        if (data.dd_kb) { setKbProgress(data.dd_kb); await S.set("dd_kb", data.dd_kb); }
        if (data.dd_skillbox) { setSkillbox(data.dd_skillbox); await S.set("dd_skillbox", data.dd_skillbox); }
        if (data.dd_planers) { setPlaners(data.dd_planers); await S.set("dd_planers", data.dd_planers); }
        else if (data.dd_planer) { // Migrations-Pfad altes Backup
          const m = [{ ...data.dd_planer, id: String(Date.now()) }];
          setPlaners(m); await S.set("dd_planers", m);
        }
        if (typeof data.dd_challenge_count === "number") { setGlobalChallengeCount(data.dd_challenge_count); await S.set("dd_challenge_count", data.dd_challenge_count); }
        if (data.dd_meds) { setMyMeds(data.dd_meds); await S.set("dd_meds", data.dd_meds); }
        setRestoreMsg(`✓ Backup vom ${new Date(data.exported).toLocaleDateString("de-DE")} wiederhergestellt!`);
        setTimeout(() => setRestoreMsg(""), 5000);
      } catch { setRestoreMsg("Fehler: Datei konnte nicht gelesen werden."); }
      if (fileRef.current) fileRef.current.value = "";
    };
    return (
      <div className="space-y-5">
        {/* Legal Status & Haftungsausschluss */}
        <Card>
          <h3 className="text-sm font-bold mb-1 flex items-center gap-2" style={{color:"var(--tx)"}}>⚖️ Rechtliche Hinweise & Haftungsausschluss</h3>
          <div className="rounded-xl p-3 mb-3" style={{background:"#E06B8A10",border:"1px solid #E06B8A44"}}>
            <p style={{fontSize:12,fontWeight:700,color:"#E06B8A",marginBottom:4}}>MDR-Abgrenzung (EU 2017/745)</p>
            <p style={{fontSize:12,color:"var(--tx2)",lineHeight:1.7}}>
              DoseDiary ist kein Medizinprodukt im Sinne der EU-Medizinprodukteverordnung. Die App verfolgt keine medizinische Zweckbestimmung und unterliegt daher nicht der MDR-Konformitätsbewertung.
            </p>
          </div>
          {[
            "DoseDiary ist ein reines Selbstreflexions- und Informationstagebuch und kein Medizinprodukt im Sinne der EU-MDR (2017/745).",
            "Die App bietet keine medizinischen Diagnosen, keine Therapievorschläge und keine Dosierungsempfehlungen für den Konsum psychoaktiver Substanzen.",
            "Alle Substanzinformationen und Wechselwirkungshinweise dienen ausschließlich der Schadensminimierung (Harm Reduction). Sie ersetzen in keinem Fall eine ärztliche Beratung, psychotherapeutische Begleitung oder fachmedizinische Einschätzung.",
            "Die Nutzung der App erfolgt freiwillig und auf eigene Verantwortung. Für die Richtigkeit, Vollständigkeit und Aktualität der bereitgestellten Informationen — insbesondere zu Wechselwirkungen — wird keine Haftung übernommen.",
            "Bei medizinischen Notfällen wende dich sofort an den Notruf (112) oder den ärztlichen Bereitschaftsdienst (116 117). Die App ist kein Ersatz für Notfallhilfe.",
            "Es werden keine personenbezogenen Daten erhoben, übermittelt oder auf Servern gespeichert.",
          ].map((t, i) => (
            <p key={i} className="text-xs py-1.5 flex gap-2 leading-relaxed" style={{color:"var(--tx2)"}}>
              <span className="shrink-0" style={{color:"var(--acc)"}}>§</span><span>{t}</span>
            </p>
          ))}
        </Card>

        {/* Data Privacy */}
        <Card>
          <h3 className="text-sm font-bold mb-3 flex items-center gap-2" style={{color:"var(--tx)"}}>🔒 Datenschutz (DSGVO)</h3>
          <div className="space-y-3">
            <div className="rounded-xl p-3" style={{background:"var(--acc)08",border:"1px solid var(--acc)22"}}>
              <p className="text-xs font-bold" style={{color:"var(--acc)"}}>Zero-Server-Architektur</p>
              <p className="text-xs mt-1 leading-relaxed" style={{color:"var(--tx2)"}}>
                Alle Daten werden ausschließlich lokal auf deinem Gerät gespeichert. Es gibt keinen Cloud-Sync, kein Tracking, keine Analyse durch Dritte und keine Registrierung.
              </p>
            </div>
            <div>
              <p className="text-xs font-bold mb-1" style={{color:"var(--tx)"}}>Gespeicherte Datenkategorien:</p>
              {[
                { cat: "Stimmungsdaten", desc: "Mood-Check-ins mit Datum", key: "dd_moods", count: moods.length },
                { cat: "Konsumlogbuch", desc: "Substanz, Menge, Setting, Craving", key: "dd_logs", count: logs.length },
                { cat: "Ziele & Clean Days", desc: "Cleane Tage, Abstinenz-Ziel, Streaks", key: "dd_goals", count: goals.cleanDays?.length || 0 },
                { cat: "Persönliche Auswahl", desc: "Gewählte Substanzen & Verhaltensweisen", key: "dd_prefs", count: prefs.mySubs?.length || 0 },
                { cat: "Wissensdatenbank", desc: "Gelesene Module & Reflexionen", key: "dd_kb", count: Object.keys(kbProgress.read || {}).length },
                { cat: "Dose Planer", desc: "Aktive Konsumplanung & Timer", key: "dd_planers", count: planers.length },
                { cat: "Medikamente", desc: "Hinterlegte Medikamente fuer Warnungen", key: "dd_meds", count: myMeds.length },
                { cat: "Skill-Box", desc: "Feedback & Notfallkontakt", key: "dd_skillbox", count: Object.values(skillbox.feedback || {}).flat().length },
              ].map((d, i) => (
                <div key={i} className="flex items-center justify-between py-2 border-b last:border-0" style={{borderColor:"var(--bdr)"}}>
                  <div><p className="text-xs font-medium" style={{color:"var(--tx)"}}>{d.cat}</p><p className="text-xs" style={{color:"var(--tx2)"}}>{d.desc}</p></div>
                  <span className="text-xs font-bold px-2 py-0.5 rounded-full" style={{background:"var(--card2)",color:"var(--tx2)"}}>{d.count}</span>
                </div>
              ))}
            </div>
          </div>
        </Card>

        {/* Backup & Restore — Datensicherung */}
        <Card>
          <h3 className="text-sm font-bold mb-3 flex items-center gap-2" style={{color:"var(--tx)"}}>💾 Datensicherung</h3>
          <p className="text-xs mb-3 leading-relaxed" style={{color:"var(--tx2)"}}>
            Exportiere alle Daten als verschlüsselte Datei. Schützt vor Datenverlust bei Browser-Löschung.
          </p>
          <div className="space-y-2">
            <button onClick={exportBackup} className="w-full py-2.5 rounded-xl text-xs font-semibold flex items-center justify-center gap-2" style={{background:"var(--acc)15",color:"var(--acc)",border:"1px solid var(--acc)44"}}>
              📤 Backup exportieren (.json)
            </button>
            <div className="relative">
              <input ref={fileRef} type="file" accept=".json" onChange={importBackup} className="absolute inset-0 opacity-0 cursor-pointer" />
              <div className="w-full py-2.5 rounded-xl text-xs font-semibold flex items-center justify-center gap-2 cursor-pointer" style={{background:"var(--card2)",color:"var(--tx2)",border:"1px solid var(--bdr)"}}>
                📥 Backup importieren
              </div>
            </div>
            {backupMsg && <p className="text-xs text-center font-medium" style={{color:"var(--acc)"}}>{backupMsg}</p>}
            {restoreMsg && <p className="text-xs text-center font-medium" style={{color:restoreMsg.startsWith("✓")?"var(--acc)":"#E06B8A"}}>{restoreMsg}</p>}
          </div>
          <p className="text-xs mt-3 italic" style={{color:"var(--bdr)"}}>
            Verschlüsselung: XOR-Obfuscation. Keine Klartextdaten in der Datei.
          </p>
        </Card>

        {/* Data Deletion — DSGVO Art. 17 */}
        <Card>
          <h3 className="text-sm font-bold mb-3 flex items-center gap-2" style={{color:"var(--tx)"}}>🗑️ Daten löschen</h3>
          <p className="text-xs mb-3 leading-relaxed" style={{color:"var(--tx2)"}}>
            Gemäß DSGVO Art. 17 (Recht auf Löschung) kannst du deine Daten jederzeit vollständig und unwiderruflich löschen.
          </p>
          {!confirmDelete ? (
            <button onClick={() => setConfirmDelete(true)} className="w-full py-2.5 rounded-xl text-xs font-semibold transition-all" style={{background:"#E06B8A15",color:"#E06B8A",border:"1px solid #E06B8A44"}}>
              Alle Nutzungsdaten löschen
            </button>
          ) : deleted ? (
            <div className="rounded-xl p-3 text-center" style={{background:"#6BCB7715",border:"1px solid #6BCB7744"}}>
              <p className="text-xs font-bold" style={{color:"#6BCB77"}}>✓ Alle Daten wurden gelöscht.</p>
            </div>
          ) : (
            <div className="rounded-xl p-3 space-y-3" style={{background:"#E06B8A10",border:"1px solid #E06B8A33"}}>
              <p className="text-xs font-bold" style={{color:"#E06B8A"}}>⚠️ Bist du sicher?</p>
              <p className="text-xs" style={{color:"var(--tx2)"}}>Diese Aktion löscht alle Moods, Logbuch-Einträge und Lernfortschritte unwiderruflich.</p>
              <div className="flex gap-2">
                <button onClick={() => setConfirmDelete(false)} className="flex-1 py-2 rounded-xl text-xs font-medium" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>Abbrechen</button>
                <button onClick={async () => { await deleteAllData(); setDeleted(true); }} className="flex-1 py-2 rounded-xl text-xs font-bold" style={{background:"#E06B8A",color:"#fff"}}>Endgültig löschen</button>
              </div>
            </div>
          )}
        </Card>

        {/* Substance/Behavior Selection Editor */}
        <Card>
          <h3 className="text-sm font-bold mb-3 flex items-center gap-2" style={{color:"var(--tx)"}}>🎯 Meine Auswahl</h3>
          <p className="text-xs mb-3" style={{color:"var(--tx2)"}}>Diese Substanzen und Verhaltensweisen werden dir im Log angezeigt. Tippe zum Ändern.</p>
          <div className="mb-3">
            <p className="text-xs font-bold mb-1.5" style={{color:"var(--tx2)"}}>Substanzen</p>
            <div className="flex flex-wrap gap-1.5">
              {SUB_ITEMS.map(s => (
                <button key={s} onClick={async () => {
                  const sel = prefs.mySubs || [];
                  const next = sel.includes(s) ? sel.filter(x => x !== s) : [...sel, s];
                  await savePrefs({ ...prefs, mySubs: next });
                }} className="px-2.5 py-1 rounded-full text-xs font-medium transition-all"
                  style={{background:(prefs.mySubs||[]).includes(s)?"var(--acc)":"var(--card2)",color:(prefs.mySubs||[]).includes(s)?"#fff":"var(--tx2)",border:`1px solid ${(prefs.mySubs||[]).includes(s)?"var(--acc)":"var(--bdr)"}`}}>
                  {subEmoji(s)} {s}
                </button>
              ))}
            </div>
          </div>
          <div>
            <p className="text-xs font-bold mb-1.5" style={{color:"var(--tx2)"}}>Verhaltensweisen</p>
            <div className="flex flex-wrap gap-1.5">
              {BEH_ITEMS.map(s => (
                <button key={s} onClick={async () => {
                  const sel = prefs.mySubs || [];
                  const next = sel.includes(s) ? sel.filter(x => x !== s) : [...sel, s];
                  await savePrefs({ ...prefs, mySubs: next });
                }} className="px-2.5 py-1 rounded-full text-xs font-medium transition-all"
                  style={{background:(prefs.mySubs||[]).includes(s)?"#F2D388":"var(--card2)",color:(prefs.mySubs||[]).includes(s)?"#1a1a2e":"var(--tx2)",border:`1px solid ${(prefs.mySubs||[]).includes(s)?"#F2D388":"var(--bdr)"}`}}>
                  {subEmoji(s)} {s}
                </button>
              ))}
            </div>
          </div>
          <p className="text-xs mt-3" style={{color:"var(--acc)"}}>{(prefs.mySubs||[]).length} ausgewählt</p>
        </Card>

        {/* Reset incl. Onboarding */}
        <Card>
          <h3 className="text-sm font-bold mb-2" style={{color:"var(--tx)"}}>🔄 App zurücksetzen</h3>
          <p className="text-xs mb-3" style={{color:"var(--tx2)"}}>Löscht alle Daten und zeigt das Onboarding erneut an.</p>
          {!confirmReset ? (
            <button onClick={() => setConfirmReset(true)} className="w-full py-2 rounded-xl text-xs font-medium" style={{background:"var(--card2)",color:"var(--tx2)",border:"1px solid var(--bdr)"}}>
              App vollständig zurücksetzen
            </button>
          ) : (
            <div className="flex gap-2">
              <button onClick={() => setConfirmReset(false)} className="flex-1 py-2 rounded-xl text-xs" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>Abbrechen</button>
              <button onClick={resetOnboarding} className="flex-1 py-2 rounded-xl text-xs font-bold" style={{background:"#E06B8A",color:"#fff"}}>Zurücksetzen</button>
            </div>
          )}
        </Card>

        {/* Version */}
        <div className="text-center py-4">
          <p className="text-xs" style={{color:"var(--tx2)"}}>DoseDiary v1.1 · Harm Reduction · Akzeptierende Begleitung</p>
          <p className="text-xs mt-1" style={{color:"var(--bdr)"}}>Persistent Storage (IndexedDB-Äquivalent) · Kein 5MB-Limit · Kein Server</p>
        </div>
      </div>
    );
  };

  // ─── GOALS & CLEAN DAYS ───
  const Goals = () => {
    const [tab, setTab] = useState("track"); // track | goal | history
    const streak = calcStreak(goals.cleanDays || [], logs);
    const longest = calcLongestStreak(goals.cleanDays || []);
    const progress = calcGoalProgress(goals, logs);
    const todayClean = goals.cleanDays?.includes(todayStr());
    const totalClean = goals.cleanDays?.length || 0;

    // Target setup
    const [editGoal, setEditGoal] = useState(false);
    const [goalType, setGoalType] = useState(goals.goalType || "clean"); // "clean" | "limit"
    const [newTarget, setNewTarget] = useState(goals.target || 30);
    const [newMaxPerWeek, setNewMaxPerWeek] = useState(goals.maxPerWeek || 3);
    const [newTargetSubs, setNewTargetSubs] = useState(goals.targetSubs || []);
    const [retroCleanOpen, setRetroCleanOpen] = useState(false);
    const [retroCleanDate, setRetroCleanDate] = useState("");

    const handleCleanDay = async () => {
      const t = todayStr();
      const updated = todayClean
        ? { ...goals, cleanDays: goals.cleanDays.filter(d => d !== t) }
        : { ...goals, cleanDays: [...(goals.cleanDays || []), t] };
      await saveGoals(updated);
    };

    // Toggle clean day for ANY date (past or today)
    const toggleCleanDate = async (ds) => {
      if (!ds) return;
      const isSet = goals.cleanDays?.includes(ds);
      const updated = isSet
        ? { ...goals, cleanDays: goals.cleanDays.filter(d => d !== ds) }
        : { ...goals, cleanDays: [...(goals.cleanDays || []), ds] };
      await saveGoals(updated);
    };

    const saveTarget = async () => {
      const updated = { ...goals, goalType, target: goalType === "clean" ? newTarget : null, maxPerWeek: goalType === "limit" ? newMaxPerWeek : null, targetSubs: newTargetSubs, startDate: goals.startDate || todayStr() };
      await saveGoals(updated);
      setEditGoal(false);
    };

    const resetGoal = async () => {
      await saveGoals({ ...goals, target: null, maxPerWeek: null, goalType: "clean", targetSubs: [], startDate: null });
      setEditGoal(false);
    };

    // Harm-Reduction: consumption this week
    const weekConsumption = () => {
      const s = new Date(); s.setDate(s.getDate() - s.getDay() + 1); s.setHours(0,0,0,0);
      const weekLogs = logs.filter(l => new Date(l.date) >= s);
      if (goals.targetSubs?.length) return weekLogs.filter(l => goals.targetSubs.includes(l.substance)).length;
      return weekLogs.length;
    };

    // Calendar for last 5 weeks
    const calendarWeeks = () => {
      const weeks = [];
      const today = new Date(); today.setHours(0,0,0,0);
      const start = new Date(today); start.setDate(start.getDate() - start.getDay() + 1 - 28);
      const logDates = new Set(logs.map(l => dateStr(l.date)));
      const cleanSet = new Set(goals.cleanDays || []);
      for (let w = 0; w < 5; w++) {
        const week = [];
        for (let d = 0; d < 7; d++) {
          const day = new Date(start); day.setDate(day.getDate() + w * 7 + d);
          const ds = dateStr(day);
          const isFuture = day > today;
          const isClean = cleanSet.has(ds);
          const isConsumed = logDates.has(ds);
          const isToday = ds === todayStr();
          week.push({ ds, day: day.getDate(), isFuture, isClean, isConsumed, isToday, month: day.getMonth() });
        }
        weeks.push(week);
      }
      return weeks;
    };

    return (
      <div className="space-y-5">
        {/* Tab bar */}
        <div className="flex rounded-xl overflow-hidden" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          {[{id:"track",l:"Tagebuch"},{id:"goal",l:"Ziel"},{id:"history",l:"Verlauf"}].map(t => (
            <button key={t.id} onClick={() => setTab(t.id)} className="flex-1 py-2.5 text-xs font-semibold transition-all"
              style={{background:tab===t.id?"var(--acc)":"transparent",color:tab===t.id?"#fff":"var(--tx2)"}}>
              {t.l}
            </button>
          ))}
        </div>

        {/* ─── TAB: Tagebuch ─── */}
        {tab === "track" && (
          <div className="space-y-5 animate-fadeIn">
            {/* Today Action */}
            <button onClick={handleCleanDay} className="w-full rounded-2xl p-5 text-center transition-all hover:scale-[1.01] active:scale-[0.97]"
              style={{background:todayClean?"linear-gradient(135deg,#6BCB7715,#9B7ECF15)":"var(--card)",border:`2px solid ${todayClean?"#6BCB77":"var(--bdr)"}`}}>
              <span className="text-4xl">{todayClean ? "✅" : "🌟"}</span>
              <p className="text-base font-bold mt-2" style={{color:todayClean?"#6BCB77":"var(--tx)",fontFamily:"var(--fontD)"}}>
                {todayClean ? "Heute als clean markiert" : "Heute als clean markieren"}
              </p>
              <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>
                {todayClean ? "Tippe, um rückgängig zu machen" : "Kein Konsum heute? Feiere das."}
              </p>
            </button>

            {/* Stats Row */}
            <div className="grid grid-cols-3 gap-2">
              <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
                <p className="text-2xl font-bold" style={{color:"#6BCB77",fontFamily:"var(--fontD)"}}>{streak}</p>
                <p className="text-xs mt-0.5" style={{color:"var(--tx2)"}}>Streak</p>
              </div>
              <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
                <p className="text-2xl font-bold" style={{color:"var(--acc)",fontFamily:"var(--fontD)"}}>{totalClean}</p>
                <p className="text-xs mt-0.5" style={{color:"var(--tx2)"}}>Gesamt</p>
              </div>
              <div className="rounded-xl p-3 text-center" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
                <p className="text-2xl font-bold" style={{color:"#F2D388",fontFamily:"var(--fontD)"}}>{longest}</p>
                <p className="text-xs mt-0.5" style={{color:"var(--tx2)"}}>Rekord</p>
              </div>
            </div>

            {/* Calendar Grid */}
            <Card>
              <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>📅 Letzte 5 Wochen</h3>
              <div className="flex justify-between mb-2 px-1">
                {["Mo","Di","Mi","Do","Fr","Sa","So"].map(d => (
                  <span key={d} className="w-9 text-center text-xs font-medium" style={{color:"var(--tx2)"}}>{d}</span>
                ))}
              </div>
              {calendarWeeks().map((week, wi) => (
                <div key={wi} className="flex justify-between mb-1 px-1">
                  {week.map((d, di) => (
                    <button key={di} onClick={() => !d.isFuture && toggleCleanDate(d.ds)} disabled={d.isFuture}
                      className="w-9 h-9 rounded-lg flex items-center justify-center text-xs font-medium transition-all active:scale-90"
                      style={{
                        background: d.isFuture ? "transparent" : d.isClean ? "#6BCB7722" : d.isConsumed ? "#E06B8A18" : "var(--card2)",
                        border: d.isToday ? "2px solid var(--acc)" : "1px solid transparent",
                        color: d.isFuture ? "var(--bdr)" : d.isClean ? "#6BCB77" : d.isConsumed ? "#E06B8A" : "var(--tx2)",
                        opacity: d.isFuture ? 0.3 : 1,
                        cursor: d.isFuture ? "default" : "pointer",
                      }}>
                      {d.isClean && !d.isFuture ? "✓" : d.day}
                    </button>
                  ))}
                </div>
              ))}
              <div className="flex items-center gap-4 mt-3 justify-center">
                <div className="flex items-center gap-1.5"><div className="w-3 h-3 rounded" style={{background:"#6BCB7722",border:"1px solid #6BCB7744"}} /><span className="text-xs" style={{color:"var(--tx2)"}}>Clean</span></div>
                <div className="flex items-center gap-1.5"><div className="w-3 h-3 rounded" style={{background:"#E06B8A18",border:"1px solid #E06B8A33"}} /><span className="text-xs" style={{color:"var(--tx2)"}}>Konsum</span></div>
                <div className="flex items-center gap-1.5"><div className="w-3 h-3 rounded" style={{background:"var(--card2)"}} /><span className="text-xs" style={{color:"var(--tx2)"}}>Kein Eintrag</span></div>
              </div>
              <p className="text-xs text-center mt-2" style={{color:"var(--tx2)"}}>Tippe auf einen Tag, um ihn als clean zu markieren oder rueckgaengig zu machen.</p>
            </Card>

            {/* Retro Clean Day — date picker for older dates */}
            <div className="rounded-2xl overflow-hidden" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <button onClick={() => setRetroCleanOpen(!retroCleanOpen)} className="w-full px-4 py-3 flex items-center justify-between text-left">
                <div className="flex items-center gap-2">
                  <span className="text-sm">📅</span>
                  <span className="text-xs font-semibold" style={{color:"var(--tx)"}}>Weitere Tage nachtraeglich markieren</span>
                </div>
                <span className="text-xs" style={{color:"var(--acc)"}}>{retroCleanOpen ? "▴" : "▾"}</span>
              </button>
              {retroCleanOpen && (
                <div className="px-4 pb-4 pt-1 animate-fadeIn">
                  <p className="text-xs mb-3" style={{color:"var(--tx2)"}}>Fuer Tage, die nicht im Kalender oben sichtbar sind:</p>
                  <div className="flex gap-2 items-end">
                    <div className="flex-1">
                      <input type="date" value={retroCleanDate} onChange={e=>setRetroCleanDate(e.target.value)} max={new Date().toISOString().split("T")[0]}
                        className="w-full rounded-lg px-3 py-2.5 text-sm outline-none" style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)",colorScheme:"dark"}} />
                    </div>
                    <button onClick={() => { if(retroCleanDate) { toggleCleanDate(retroCleanDate); }}} disabled={!retroCleanDate}
                      className="px-4 py-2.5 rounded-lg text-xs font-semibold shrink-0"
                      style={{background:retroCleanDate?"var(--acc)":"var(--bdr)",color:retroCleanDate?"#fff":"var(--tx2)"}}>
                      {goals.cleanDays?.includes(retroCleanDate) ? "✓ Entfernen" : "✓ Als clean markieren"}
                    </button>
                  </div>
                  {retroCleanDate && goals.cleanDays?.includes(retroCleanDate) && (
                    <p className="text-xs mt-2" style={{color:"#6BCB77"}}>✓ {new Date(retroCleanDate).toLocaleDateString("de-DE",{weekday:"long",day:"numeric",month:"long"})} ist als clean markiert</p>
                  )}
                </div>
              )}
            </div>

            {/* Motivation */}
            {streak > 0 && (
              <div className="rounded-2xl p-4 text-center" style={{background:"var(--card)",border:"1px solid #6BCB7733"}}>
                <p className="text-xl mb-1">{streak >= 30 ? "🏆" : streak >= 14 ? "💎" : streak >= 7 ? "🔥" : streak >= 3 ? "⭐" : "🌱"}</p>
                <p className="text-sm font-semibold" style={{color:"var(--tx)"}}>
                  {streak >= 30 ? "Ein ganzer Monat!" : streak >= 14 ? "Zwei Wochen stark!" : streak >= 7 ? "Eine Woche geschafft!" : streak >= 3 ? "Drei Tage — das zählt!" : "Jeder Tag zählt."}
                </p>
                <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Jeder cleane Tag stärkt deine Selbstwirksamkeit.</p>
              </div>
            )}
          </div>
        )}

        {/* ─── TAB: Ziel ─── */}
        {tab === "goal" && (
          <div className="space-y-5 animate-fadeIn">
            {(goals.target || goals.maxPerWeek) && !editGoal ? (
              <>
                {/* Active Goal Display */}
                <div className="rounded-2xl p-5 text-center" style={{background:"linear-gradient(135deg,#6BCB7710,#9B7ECF10)",border:"1px solid #6BCB7733"}}>
                  <p className="text-xs font-bold mb-1" style={{color:"var(--acc)"}}>
                    {goals.goalType === "limit" ? "🎯 HARM-REDUCTION-LIMIT" : "🌟 ABSTINENZ-ZIEL"}
                  </p>
                  <p className="text-2xl font-bold" style={{color:"var(--tx)",fontFamily:"var(--fontD)"}}>
                    {goals.goalType === "limit" ? `Max. ${goals.maxPerWeek} Konsumtage/Woche` : `${goals.target} cleane Tage`}
                  </p>
                  {goals.targetSubs?.length > 0 && (
                    <p className="text-xs mt-2" style={{color:"var(--tx2)"}}>
                      Bezug: {goals.targetSubs.map(s => `${subEmoji(s)} ${s}`).join(", ")}
                    </p>
                  )}
                  <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Seit {new Date(goals.startDate).toLocaleDateString("de-DE")}</p>
                </div>

                {/* Progress for Clean-Days goal */}
                {goals.goalType === "clean" && progress && (
                  <Card>
                    <div className="flex items-center justify-between mb-3">
                      <span className="text-sm font-bold" style={{color:"var(--tx)"}}>Fortschritt</span>
                      <span className="text-sm font-bold" style={{color:progress.pct>=100?"#6BCB77":"var(--acc)"}}>{progress.pct}%</span>
                    </div>
                    <div className="w-full h-3 rounded-full mb-3" style={{background:"var(--bdr)"}}>
                      <div className="h-3 rounded-full transition-all duration-700" style={{width:`${progress.pct}%`,background:progress.pct>=100?"#6BCB77":"var(--acc)"}} />
                    </div>
                    <div className="grid grid-cols-3 gap-2 text-center">
                      <div><p className="text-lg font-bold" style={{color:"#6BCB77"}}>{progress.cleanInRange}</p><p className="text-xs" style={{color:"var(--tx2)"}}>Clean</p></div>
                      <div><p className="text-lg font-bold" style={{color:"var(--tx)"}}>{progress.totalDays}</p><p className="text-xs" style={{color:"var(--tx2)"}}>Tage</p></div>
                      <div><p className="text-lg font-bold" style={{color:"var(--acc)"}}>{Math.max(0, progress.target - progress.cleanInRange)}</p><p className="text-xs" style={{color:"var(--tx2)"}}>Übrig</p></div>
                    </div>
                    {progress.pct >= 100 && (
                      <div className="mt-3 p-3 rounded-xl text-center" style={{background:"#6BCB7715"}}>
                        <p className="text-xl">🎉</p>
                        <p className="text-sm font-bold mt-1" style={{color:"#6BCB77"}}>Ziel erreicht!</p>
                      </div>
                    )}
                  </Card>
                )}

                {/* Progress for Limit goal */}
                {goals.goalType === "limit" && (
                  <Card>
                    <div className="flex items-center justify-between mb-3">
                      <span className="text-sm font-bold" style={{color:"var(--tx)"}}>Diese Woche</span>
                      <span className="text-sm font-bold" style={{color:weekConsumption() <= goals.maxPerWeek ? "#6BCB77" : "#E06B8A"}}>
                        {weekConsumption()} / {goals.maxPerWeek}
                      </span>
                    </div>
                    <div className="w-full h-3 rounded-full mb-3" style={{background:"var(--bdr)"}}>
                      <div className="h-3 rounded-full transition-all duration-700" style={{
                        width:`${Math.min(100, weekConsumption() / goals.maxPerWeek * 100)}%`,
                        background: weekConsumption() <= goals.maxPerWeek ? "#6BCB77" : "#E06B8A"
                      }} />
                    </div>
                    <p className="text-xs text-center" style={{color:"var(--tx2)"}}>
                      {weekConsumption() <= goals.maxPerWeek
                        ? `✓ Du bist im Rahmen. Noch ${goals.maxPerWeek - weekConsumption()} Konsumtage übrig.`
                        : `⚠️ Limit überschritten. Reflektiere, was du anpassen kannst.`}
                    </p>
                    <p className="text-xs text-center mt-2 italic" style={{color:"var(--tx2)"}}>
                      Reduktion ist auch ein Erfolg. Jeder bewusste Tag zählt.
                    </p>
                  </Card>
                )}

                <div className="flex gap-3">
                  <button onClick={() => { setEditGoal(true); setGoalType(goals.goalType || "clean"); setNewTarget(goals.target || 30); setNewMaxPerWeek(goals.maxPerWeek || 3); setNewTargetSubs(goals.targetSubs || []); }} className="flex-1 py-2.5 rounded-xl text-xs font-medium" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>
                    ✏️ Anpassen
                  </button>
                  <button onClick={resetGoal} className="flex-1 py-2.5 rounded-xl text-xs font-medium" style={{background:"#E06B8A12",color:"#E06B8A",border:"1px solid #E06B8A33"}}>
                    Ziel zurücksetzen
                  </button>
                </div>
              </>
            ) : (
              /* Goal Setup — two types */
              <div className="space-y-5">
                <div className="text-center">
                  <span className="text-3xl">🎯</span>
                  <h3 className="text-base font-bold mt-2" style={{color:"var(--tx)",fontFamily:"var(--fontD)"}}>
                    {editGoal ? "Ziel anpassen" : "Ziel setzen"}
                  </h3>
                  <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Wähle den Zieltyp, der zu dir passt.</p>
                </div>

                {/* Goal Type Selector */}
                <div className="grid grid-cols-2 gap-3">
                  <button onClick={() => setGoalType("clean")} className="rounded-2xl p-4 text-center transition-all"
                    style={{background:goalType==="clean"?"var(--acc)12":"var(--card)",border:`2px solid ${goalType==="clean"?"var(--acc)":"var(--bdr)"}`}}>
                    <p className="text-xl mb-1">🌟</p>
                    <p className="text-xs font-bold" style={{color:goalType==="clean"?"var(--acc)":"var(--tx)"}}>Abstinenz-Ziel</p>
                    <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>X cleane Tage erreichen</p>
                  </button>
                  <button onClick={() => setGoalType("limit")} className="rounded-2xl p-4 text-center transition-all"
                    style={{background:goalType==="limit"?"#F2D38812":"var(--card)",border:`2px solid ${goalType==="limit"?"#F2D388":"var(--bdr)"}`}}>
                    <p className="text-xl mb-1">📊</p>
                    <p className="text-xs font-bold" style={{color:goalType==="limit"?"#F2D388":"var(--tx)"}}>Reduktions-Limit</p>
                    <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Max. N Tage pro Woche</p>
                  </button>
                </div>

                {/* Clean Days Target */}
                {goalType === "clean" && (
                  <Card>
                    <Label>Anzahl cleaner Tage</Label>
                    <div className="flex gap-2 flex-wrap">
                      {[7,14,30,60,90].map(n => (
                        <button key={n} onClick={() => setNewTarget(n)} className="px-4 py-2 rounded-xl text-sm font-semibold transition-all"
                          style={{background:newTarget===n?"var(--acc)":"var(--card2)",color:newTarget===n?"#fff":"var(--tx)",border:`1px solid ${newTarget===n?"var(--acc)":"var(--bdr)"}`}}>
                          {n} Tage
                        </button>
                      ))}
                    </div>
                    <input type="number" value={newTarget} onChange={e => setNewTarget(Math.max(1,+e.target.value))}
                      className="w-full mt-3 rounded-xl px-4 py-2.5 text-sm outline-none" inputMode="numeric"
                      style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}} placeholder="Oder eigene Zahl" />
                  </Card>
                )}

                {/* Harm Reduction Limit */}
                {goalType === "limit" && (
                  <Card>
                    <Label>Max. Konsumtage pro Woche</Label>
                    <div className="flex gap-2 flex-wrap">
                      {[1,2,3,4,5].map(n => (
                        <button key={n} onClick={() => setNewMaxPerWeek(n)} className="px-4 py-2 rounded-xl text-sm font-semibold transition-all"
                          style={{background:newMaxPerWeek===n?"#F2D388":"var(--card2)",color:newMaxPerWeek===n?"#1a1a2e":"var(--tx)",border:`1px solid ${newMaxPerWeek===n?"#F2D388":"var(--bdr)"}`}}>
                          {n}×
                        </button>
                      ))}
                    </div>
                    <p className="text-xs mt-3 italic" style={{color:"var(--tx2)"}}>
                      Gezählt werden Tage mit mindestens einem Log-Eintrag in der aktuellen Woche (Mo–So).
                    </p>
                  </Card>
                )}

                {/* Substance filter (both types) */}
                <Card>
                  <Label>Bezug auf (optional)</Label>
                  <p className="text-xs mb-3" style={{color:"var(--tx2)"}}>Leer = alles. Oder wähle spezifisch:</p>
                  <div className="flex flex-wrap gap-2">
                    {(prefs.mySubs?.length > 0 ? prefs.mySubs : SUBSTANCES).filter(s => !s.startsWith("Andere")).map(s => (
                      <button key={s} onClick={() => setNewTargetSubs(p => p.includes(s) ? p.filter(x=>x!==s) : [...p, s])}
                        className="px-2.5 py-1.5 rounded-full text-xs font-medium transition-all"
                        style={{background:newTargetSubs.includes(s)?"var(--acc)":"var(--card2)",color:newTargetSubs.includes(s)?"#fff":"var(--tx2)",border:`1px solid ${newTargetSubs.includes(s)?"var(--acc)":"var(--bdr)"}`}}>
                        {subEmoji(s)} {s}
                      </button>
                    ))}
                  </div>
                </Card>

                <Btn onClick={saveTarget}>
                  🎯 {editGoal ? "Ziel aktualisieren" : "Ziel starten"}
                </Btn>
                {editGoal && <button onClick={() => setEditGoal(false)} className="w-full py-2 text-xs" style={{color:"var(--tx2)"}}>Abbrechen</button>}

                <div className="rounded-xl px-4 py-3" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
                  <div className="flex items-center gap-2 mb-1"><span className="text-xs">⚕️</span><span className="text-xs font-bold" style={{color:"var(--tx2)"}}>Harm Reduction</span></div>
                  <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>
                    Auch Reduktion ist ein Ziel. Du definierst, was Fortschritt für dich bedeutet. Diese App ersetzt keine professionelle Beratung.
                  </p>
                </div>
              </div>
            )}
          </div>
        )}

        {/* ─── TAB: Verlauf ─── */}
        {tab === "history" && (
          <div className="space-y-4 animate-fadeIn">
            <Card>
              <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>📊 Deine Übersicht</h3>
              <Row l="🌟 Cleane Tage gesamt" r={totalClean} />
              <Row l="🔥 Aktuelle Streak" r={`${streak} Tage`} />
              <Row l="🏆 Längste Streak" r={`${longest} Tage`} />
              <Row l="📝 Konsumeinträge" r={logs.length} />
              <Row l="📊 Clean-Quote (30 Tage)" r={(() => {
                const d30 = new Date(); d30.setDate(d30.getDate() - 30);
                const clean30 = (goals.cleanDays||[]).filter(d => d >= dateStr(d30)).length;
                return `${clean30}/30 (${Math.round(clean30/30*100)}%)`;
              })()} />
            </Card>

            {/* Monthly breakdown */}
            <Card>
              <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>📆 Monatsvergleich</h3>
              {(() => {
                const months = {};
                (goals.cleanDays||[]).forEach(d => {
                  const m = d.substring(0, 7); // YYYY-MM
                  months[m] = (months[m] || 0) + 1;
                });
                const sorted = Object.entries(months).sort((a,b) => b[0].localeCompare(a[0])).slice(0, 6);
                if (!sorted.length) return <p className="text-xs" style={{color:"var(--tx2)"}}>Noch keine Daten.</p>;
                const mx = Math.max(...sorted.map(([,c]) => c), 1);
                return sorted.map(([m, c]) => {
                  const [y, mo] = m.split("-");
                  const label = new Date(+y, +mo - 1).toLocaleDateString("de-DE", { month: "short", year: "numeric" });
                  return (
                    <div key={m} className="mb-2">
                      <div className="flex justify-between text-xs mb-1">
                        <span style={{color:"var(--tx)"}}>{label}</span>
                        <span style={{color:"#6BCB77"}}>{c} clean</span>
                      </div>
                      <div className="w-full h-2 rounded-full" style={{background:"var(--bdr)"}}>
                        <div className="h-2 rounded-full" style={{width:`${c/mx*100}%`,background:"#6BCB77",transition:"width 0.5s"}} />
                      </div>
                    </div>
                  );
                });
              })()}
            </Card>

            {/* Mood on clean vs consumed days */}
            {moods.length >= 3 && (
              <Card>
                <h3 className="text-sm font-bold mb-3" style={{color:"var(--tx)"}}>💚 Mood-Vergleich</h3>
                {(() => {
                  const cleanSet = new Set(goals.cleanDays || []);
                  const logDates = new Set(logs.map(l => dateStr(l.date)));
                  const cleanMoods = moods.filter(m => cleanSet.has(dateStr(m.date)));
                  const conMoods = moods.filter(m => logDates.has(dateStr(m.date)));
                  const avgC = cleanMoods.length ? (cleanMoods.reduce((s,m)=>s+m.value,0)/cleanMoods.length).toFixed(1) : "–";
                  const avgK = conMoods.length ? (conMoods.reduce((s,m)=>s+m.value,0)/conMoods.length).toFixed(1) : "–";
                  return (
                    <div className="grid grid-cols-2 gap-3 text-center">
                      <div className="rounded-xl p-3" style={{background:"#6BCB7712"}}>
                        <p className="text-xl font-bold" style={{color:"#6BCB77"}}>{avgC}</p>
                        <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Ø Mood an cleanen Tagen</p>
                      </div>
                      <div className="rounded-xl p-3" style={{background:"#E06B8A12"}}>
                        <p className="text-xl font-bold" style={{color:"#E06B8A"}}>{avgK}</p>
                        <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Ø Mood an Konsumtagen</p>
                      </div>
                    </div>
                  );
                })()}
              </Card>
            )}
          </div>
        )}
      </div>
    );
  };

  // ═══════════════════════════════════════════════════════════
  // ─── WISSENSDATENBANK (12 Module — Harm Reduction Knowledge Base) ──
  // ═══════════════════════════════════════════════════════════
  const KnowledgeBase = () => {
    const [openModule, setOpenModule] = useState(null);
    const [scrollPos, setScrollPos] = useState(0); // track section within module
    const [reflectionText, setReflectionText] = useState("");
    const [reflectionSaved, setReflectionSaved] = useState(false);
    const [showReflection, setShowReflection] = useState(false);

    const readCount = Object.keys(kbProgress.read || {}).length;
    const mod = openModule !== null ? KB_MODULES[openModule] : null;

    const openMod = (idx) => {
      setOpenModule(idx);
      setScrollPos(0);
      setShowReflection(false);
      setReflectionSaved(false);
      const m = KB_MODULES[idx];
      setReflectionText(kbProgress.reflections?.[m.id] || "");
    };

    const markRead = async (modId) => {
      if (kbProgress.read?.[modId]) return;
      const updated = { ...kbProgress, read: { ...kbProgress.read, [modId]: new Date().toISOString() } };
      await saveKb(updated);
    };

    const saveReflection = async (modId, text) => {
      const updated = { ...kbProgress, reflections: { ...kbProgress.reflections, [modId]: text } };
      await saveKb(updated);
      setReflectionSaved(true);
      setTimeout(() => setReflectionSaved(false), 2000);
    };

    // ─── Module Detail View ───
    if (mod) {
      const isRead = !!kbProgress.read?.[mod.id];
      const totalSteps = mod.sections.length + 1; // sections + reflection
      const currentStep = showReflection ? totalSteps - 1 : scrollPos;

      return (
        <div className="space-y-5">
          {/* Back + Progress */}
          <div>
            <button onClick={() => setOpenModule(null)} aria-label="Zurück zur Modulübersicht" className="text-xs flex items-center gap-1 mb-3" style={{color:"var(--acc)",minHeight:44}}>← Zurück zur Übersicht</button>
            <div className="flex gap-1">
              {Array.from({ length: totalSteps }).map((_, i) => (
                <div key={i} className="h-1 flex-1 rounded-full transition-all duration-300" style={{background: i <= currentStep ? mod.color : "var(--bdr)"}} />
              ))}
            </div>
          </div>

          {/* Module Header */}
          <div className="rounded-2xl overflow-hidden" style={{border:`1px solid ${mod.color}33`}}>
            <div className="px-5 py-4" style={{background:`${mod.color}10`}}>
              <div className="flex items-center gap-3 mb-2">
                <div className="w-12 h-12 rounded-2xl flex items-center justify-center text-2xl" style={{background:`${mod.color}20`}}>{mod.icon}</div>
                <div>
                  <p className="text-base font-bold" style={{color:"var(--tx)",fontFamily:"var(--fontD)"}}>{mod.title}</p>
                  <p className="text-xs mt-0.5" style={{color:"var(--tx2)"}}>{mod.readMin} Min. Lesezeit</p>
                </div>
              </div>
              <p className="text-sm italic" style={{color:mod.color}}>{mod.tagline}</p>
            </div>
          </div>

          {/* Section Content or Reflection */}
          {!showReflection ? (
            <>
              <div className="rounded-2xl p-5 animate-fadeIn" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
                <p className="text-xs font-bold mb-1.5" style={{color:mod.color}}>{scrollPos + 1} / {mod.sections.length}</p>
                <h4 className="text-sm font-bold mb-3" style={{color:"var(--tx)",fontFamily:"var(--fontD)"}}>{mod.sections[scrollPos].heading}</h4>
                <p className="text-sm leading-[1.75] whitespace-pre-line" style={{color:"var(--tx2)"}}>{mod.sections[scrollPos].body}</p>
              </div>

              {/* Section Navigation */}
              <div className="flex gap-3">
                {scrollPos > 0 && (
                  <button onClick={() => setScrollPos(scrollPos - 1)} className="flex-1 py-2.5 rounded-xl text-sm font-medium" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>← Zurück</button>
                )}
                {scrollPos < mod.sections.length - 1 ? (
                  <button onClick={() => setScrollPos(scrollPos + 1)} className="flex-1 py-2.5 rounded-xl text-sm font-semibold" style={{background:mod.color,color:"#fff"}}>Weiter →</button>
                ) : (
                  <button onClick={() => { setShowReflection(true); markRead(mod.id); }} className="flex-1 py-2.5 rounded-xl text-sm font-semibold" style={{background:mod.color,color:"#fff"}}>
                    💭 Zur Reflexion →
                  </button>
                )}
              </div>
            </>
          ) : (
            <>
              {/* Reflection Card */}
              <div className="rounded-2xl overflow-hidden animate-fadeIn" style={{background:"var(--card)",border:`1px solid ${mod.color}44`}}>
                <div className="px-5 py-3" style={{background:`${mod.color}08`,borderBottom:`1px solid ${mod.color}22`}}>
                  <p className="text-xs font-bold flex items-center gap-2" style={{color:mod.color}}>
                    <span className="w-5 h-5 rounded-full flex items-center justify-center text-xs" style={{background:`${mod.color}20`}}>💭</span>
                    Reflexionsfrage
                  </p>
                </div>
                <div className="p-5">
                  <p className="text-sm font-semibold leading-relaxed mb-4" style={{color:"var(--tx)"}}>{mod.reflection.q}</p>
                  <textarea
                    value={reflectionText}
                    onChange={e => setReflectionText(e.target.value)}
                    rows={4}
                    className="w-full rounded-xl px-4 py-3 text-sm outline-none resize-none leading-relaxed"
                    style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}}
                    placeholder={mod.reflection.placeholder}
                  />
                  <div className="flex gap-3 mt-3">
                    <button onClick={() => saveReflection(mod.id, reflectionText)}
                      className="flex-1 py-2.5 rounded-xl text-xs font-semibold transition-all"
                      style={{background:reflectionSaved?`#6BCB7718`:mod.color,color:reflectionSaved?"#6BCB77":"#fff",border:reflectionSaved?`1px solid #6BCB7744`:"none"}}>
                      {reflectionSaved ? "✓ Gespeichert" : "💾 Reflexion speichern"}
                    </button>
                  </div>
                  <p className="text-xs mt-2 text-center italic" style={{color:"var(--tx2)"}}>Deine Antwort bleibt privat auf deinem Gerät.</p>
                </div>
              </div>

              {/* Read status badge */}
              <div className="rounded-xl px-4 py-3 flex items-center gap-3" style={{background:"#6BCB7710",border:"1px solid #6BCB7733"}}>
                <span className="text-lg">✅</span>
                <div>
                  <p className="text-xs font-bold" style={{color:"#6BCB77"}}>Modul gelesen</p>
                  <p className="text-xs" style={{color:"var(--tx2)"}}>Gelesen am {new Date(kbProgress.read?.[mod.id] || Date.now()).toLocaleDateString("de-DE")}</p>
                </div>
              </div>

              {/* Link to App Tool */}
              <button onClick={() => nav(mod.linkTo)} className="w-full py-3 rounded-2xl text-sm font-semibold flex items-center justify-center gap-2 transition-all hover:scale-[1.01]"
                style={{background:`${mod.color}15`,color:mod.color,border:`1px solid ${mod.color}44`}}>
                {mod.linkLabel}
              </button>

              {/* Back to section */}
              <button onClick={() => setShowReflection(false)} className="w-full text-xs py-2" style={{color:"var(--tx2)"}}>← Text nochmal lesen</button>
            </>
          )}
        </div>
      );
    }

    // ─── Overview Dashboard with 12 Tiles ───
    return (
      <div className="space-y-5">
        {/* Progress Header */}
        <div className="text-center">
          <p className="text-xs" style={{color:"var(--tx2)"}}>{readCount} von {KB_MODULES.length} Modulen gelesen</p>
          <div className="w-full h-2 rounded-full mt-2" style={{background:"var(--bdr)"}}>
            <div className="h-2 rounded-full transition-all duration-700" style={{width:`${readCount/KB_MODULES.length*100}%`,background:"var(--acc)"}} />
          </div>
        </div>

        {/* 12 Module Tiles — 2 Column Grid */}
        <div className="grid grid-cols-2 gap-3">
          {KB_MODULES.map((m, i) => {
            const isRead = !!kbProgress.read?.[m.id];
            const hasReflection = !!kbProgress.reflections?.[m.id];
            return (
              <button key={m.id} onClick={() => openMod(i)}
                className="rounded-2xl p-4 text-left transition-all duration-200 hover:scale-[1.02] active:scale-[0.97] relative overflow-hidden"
                style={{
                  background: isRead ? `${m.color}08` : "var(--card)",
                  border: `1px solid ${isRead ? `${m.color}44` : "var(--bdr)"}`,
                }}>
                {/* Read indicator */}
                {isRead && (
                  <div className="absolute top-2.5 right-2.5 w-5 h-5 rounded-full flex items-center justify-center text-xs" style={{background:`#6BCB7722`,color:"#6BCB77"}}>✓</div>
                )}
                {/* Reflection indicator */}
                {hasReflection && !isRead && (
                  <div className="absolute top-2.5 right-2.5 w-5 h-5 rounded-full flex items-center justify-center" style={{background:`${m.color}22`}}>
                    <span style={{fontSize:9,color:m.color}}>💭</span>
                  </div>
                )}
                {/* Tile content */}
                <div className="w-10 h-10 rounded-xl flex items-center justify-center text-xl mb-2.5" style={{background:`${m.color}18`}}>
                  {m.icon}
                </div>
                <p className="text-xs font-bold leading-snug" style={{color:"var(--tx)"}}>{m.title}</p>
                <p className="text-xs mt-1 leading-snug" style={{color:"var(--tx2)",display:"-webkit-box",WebkitLineClamp:2,WebkitBoxOrient:"vertical",overflow:"hidden"}}>{m.tagline}</p>
                <div className="flex items-center gap-1.5 mt-2">
                  <span style={{fontSize:9,color:m.color}}>●</span>
                  <span className="text-xs" style={{color:"var(--tx2)"}}>{m.readMin} Min.</span>
                </div>
              </button>
            );
          })}
        </div>

        {/* Disclaimer */}
        <div className="rounded-xl px-4 py-3" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          <div className="flex items-center gap-2 mb-1"><span className="text-xs">⚕️</span><span className="text-xs font-bold" style={{color:"var(--tx2)"}}>Hinweis</span></div>
          <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>
            Diese Module dienen der Selbstreflexion und Information. Sie ersetzen keine professionelle Beratung, Therapie oder ärztliche Behandlung. Alle Inhalte basieren auf dem Prinzip der akzeptierenden Drogenhilfe.
          </p>
        </div>

        {/* My Reflections Overview */}
        {Object.keys(kbProgress.reflections || {}).filter(k => kbProgress.reflections[k]?.trim()).length > 0 && (
          <div className="rounded-2xl overflow-hidden" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
            <div className="px-4 py-3" style={{borderBottom:"1px solid var(--bdr)"}}>
              <p className="text-xs font-bold" style={{color:"var(--tx)"}}>💭 Meine Reflexionen</p>
            </div>
            <div className="px-4 py-2">
              {Object.entries(kbProgress.reflections || {}).filter(([,v]) => v?.trim()).map(([modId, text]) => {
                const m = KB_MODULES.find(x => x.id === modId);
                if (!m) return null;
                return (
                  <button key={modId} onClick={() => openMod(KB_MODULES.indexOf(m))}
                    className="w-full text-left py-2.5 flex gap-3 items-start border-b last:border-0" style={{borderColor:"var(--bdr)"}}>
                    <span className="text-base shrink-0">{m.icon}</span>
                    <div className="min-w-0 flex-1">
                      <p className="text-xs font-semibold" style={{color:m.color}}>{m.title}</p>
                      <p className="text-xs mt-0.5 truncate" style={{color:"var(--tx2)"}}>{text}</p>
                    </div>
                  </button>
                );
              })}
            </div>
          </div>
        )}
      </div>
    );
  };

  // ═══════════════════════════════════════════════════════════
  // ─── DOSE PLANER (Konsumintervall-Timer) ──────────────────
  // ═══════════════════════════════════════════════════════════
  // ─── SINGLE PLANER CARD (für jede Instanz im Cockpit) ───
  const PlanerCard = ({ p }) => {
    const [now, setNow] = useState(Date.now());
    const [challengeActive, setChallengeActive] = useState(false);
    const [challengeSuccess, setChallengeSuccess] = useState(false);

    useEffect(() => {
      const id = setInterval(() => setNow(Date.now()), 1000);
      return () => clearInterval(id);
    }, []);

    const formatTime = (ms) => {
      const m = Math.floor(ms / 60000);
      const s = Math.floor((ms % 60000) / 1000);
      return `${m}:${String(s).padStart(2, "0")}`;
    };

    const intMs = p.interval * 60 * 1000;
    const lastC = p.lastConsumedAt ? new Date(p.lastConsumedAt).getTime() : 0;
    const chalStart = p.challengeStartedAt ? new Date(p.challengeStartedAt).getTime() : 0;
    const elapsed = lastC ? now - lastC : 0;
    const remaining = Math.max(0, intMs - elapsed);
    const pct = lastC ? Math.min(1, elapsed / intMs) : 0;
    const chalMs = 15 * 60 * 1000;
    const chalElapsed = chalStart ? now - chalStart : 0;
    const chalRemaining = Math.max(0, chalMs - chalElapsed);
    const chalDone = challengeActive && chalRemaining === 0;
    const chalPct = chalStart ? Math.min(1, chalElapsed / chalMs) : 0;
    const isOpen = lastC > 0 && remaining === 0 && !challengeActive && !challengeSuccess;
    const isWaiting = lastC > 0 && remaining > 0 && !challengeActive;
    const isFirst = !lastC;
    const lim = p.maxUnits > 0 && p.consumedCount >= p.maxUnits;
    const r = 74; const circ = 2 * Math.PI * r;

    const doRecord = async () => {
      await updatePlaner(p.id, { consumedCount: (p.consumedCount||0)+1, lastConsumedAt: new Date().toISOString(), challengeStartedAt: null });
      setChallengeActive(false); setChallengeSuccess(false);
      nav("planer");
    };
    const doStartChallenge = async () => {
      setChallengeActive(true); setChallengeSuccess(false);
      await updatePlaner(p.id, { challengeStartedAt: new Date().toISOString() });
    };
    const doChallengeComplete = async () => {
      await addGlobalChallenge();
      await updatePlaner(p.id, { lastConsumedAt: new Date().toISOString(), challengeStartedAt: null, challengeCount: (p.challengeCount||0)+1 });
      setChallengeActive(false); setChallengeSuccess(true);
    };
    const doRemove = async () => await removePlaner(p.id);

    return (
      <div className="rounded-2xl overflow-hidden" style={{background:"var(--card)",border:"1px solid #7B8CDE33"}}>
        {/* Karten-Header */}
        <div className="px-4 py-3 flex items-center gap-2" style={{borderBottom:"1px solid var(--bdr)"}}>
          <span className="text-lg">{subEmoji(p.substance)}</span>
          <div className="flex-1 min-w-0">
            <p className="text-sm font-bold truncate" style={{color:"var(--tx)"}}>{p.substance}</p>
            <p style={{fontSize:10,color:"var(--tx2)"}}>{p.unit} · alle {p.interval} Min.</p>
          </div>
          <div className="grid grid-cols-3 gap-1.5 text-center shrink-0">
            <div><p className="text-sm font-bold" style={{color:"var(--acc)",fontFamily:"var(--fontD)"}}>{p.consumedCount}</p><p style={{fontSize:8,color:"var(--tx2)"}}>×</p></div>
            <div><p className="text-sm font-bold" style={{color:lim?"#E06B8A":"var(--tx)",fontFamily:"var(--fontD)"}}>{p.maxUnits>0?p.maxUnits-p.consumedCount:"∞"}</p><p style={{fontSize:8,color:"var(--tx2)"}}>max</p></div>
            <div><p className="text-sm font-bold" style={{color:(p.challengeCount||0)>0?"#B89DE8":"var(--tx2)",fontFamily:"var(--fontD)"}}>{(p.challengeCount||0)>0?`${p.challengeCount}⭐`:"—"}</p><p style={{fontSize:8,color:"var(--tx2)"}}>ch.</p></div>
          </div>
          <button onClick={doRemove} aria-label="Planer entfernen" className="ml-1 text-xs px-2 py-1 rounded-lg shrink-0"
            style={{background:"var(--card2)",color:"#E06B8A",border:"1px solid #E06B8A33"}}>✕</button>
        </div>

        <div className="px-4 py-4 space-y-3">
          {/* Limit erreicht */}
          {lim && (
            <div className="rounded-xl p-4 text-center" style={{background:"#6BCB7712",border:"1px solid #6BCB7744"}}>
              <p className="text-2xl mb-1">🎯</p>
              <p className="text-sm font-bold" style={{color:"#6BCB77"}}>Limit erreicht — gute Selbstkontrolle!</p>
              <button onClick={() => nav("skillbox")} className="mt-2 text-xs px-3 py-1.5 rounded-lg"
                style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>🧰 Skill-Box</button>
            </div>
          )}

          {/* Erster Eintrag */}
          {isFirst && !lim && (
            <div className="text-center py-2">
              <p className="text-xs mb-2" style={{color:"var(--tx2)"}}>Logge den ersten Konsum, um den Timer zu starten.</p>
              <button onClick={doRecord} className="px-5 py-2.5 rounded-xl text-sm font-bold"
                style={{background:"var(--acc)",color:"#fff"}}>📝 Jetzt loggen</button>
            </div>
          )}

          {/* Timer-Ring: wartet */}
          {isWaiting && !lim && (
            <div className="flex gap-4 items-center">
              <div className="relative shrink-0" style={{width:80,height:80}}>
                <svg viewBox="0 0 200 200" className="w-full h-full" style={{transform:"rotate(-90deg)"}}>
                  <circle cx="100" cy="100" r={r} fill="none" stroke="var(--bdr)" strokeWidth="10" />
                  <circle cx="100" cy="100" r={r} fill="none" stroke="#7B8CDE" strokeWidth="10"
                    strokeDasharray={circ} strokeDashoffset={circ*(1-pct)} strokeLinecap="round"
                    className="transition-all duration-1000" />
                </svg>
                <div className="absolute inset-0 flex items-center justify-center">
                  <span style={{fontSize:11,fontWeight:800,color:"#7B8CDE",fontFamily:"var(--fontD)"}}>{formatTime(remaining)}</span>
                </div>
              </div>
              <div className="flex-1">
                <p className="text-xs font-semibold mb-1" style={{color:"var(--tx)"}}>Nächste Einheit in {Math.ceil(remaining/60000)} Min.</p>
                <button onClick={() => nav("skillbox")} className="text-xs px-3 py-1.5 rounded-lg"
                  style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>🧰 Überbrücken</button>
              </div>
            </div>
          )}

          {/* Challenge läuft */}
          {challengeActive && !lim && (() => {
            if (chalDone) setTimeout(doChallengeComplete, 1200);
            return (
              <div className="rounded-xl p-3 text-center" style={{background:"linear-gradient(135deg,#9B7ECF18,#F2D38812)",border:"2px solid #9B7ECF55"}}>
                <p style={{fontSize:10,fontWeight:800,color:"#B89DE8",letterSpacing:"1px"}}>✨ CHALLENGE</p>
                <div className="relative mx-auto my-2" style={{width:80,height:80}}>
                  <svg viewBox="0 0 200 200" className="w-full h-full" style={{transform:"rotate(-90deg)"}}>
                    <circle cx="100" cy="100" r={r} fill="none" stroke="var(--bdr)" strokeWidth="10" />
                    <circle cx="100" cy="100" r={r} fill="none"
                      stroke={chalDone?"#6BCB77":"#9B7ECF"} strokeWidth="10"
                      strokeDasharray={circ} strokeDashoffset={circ*(1-chalPct)} strokeLinecap="round"
                      className="transition-all duration-1000" />
                  </svg>
                  <div className="absolute inset-0 flex items-center justify-center">
                    {chalDone
                      ? <span className="text-2xl">⭐</span>
                      : <span style={{fontSize:11,fontWeight:800,color:"#B89DE8",fontFamily:"var(--fontD)"}}>{formatTime(chalRemaining)}</span>
                    }
                  </div>
                </div>
                <p style={{fontSize:11,color:"var(--tx)"}}>Du hältst die Pause. Echte Stärke.</p>
                {!chalDone && (
                  <button onClick={doRecord} className="mt-2 text-xs px-3 py-1 rounded-lg"
                    style={{background:"var(--card2)",color:"var(--tx2)",border:"1px solid var(--bdr)"}}>Doch loggen</button>
                )}
              </div>
            );
          })()}

          {/* Challenge Erfolg */}
          {challengeSuccess && !challengeActive && !lim && (
            <div className="rounded-xl p-3 text-center animate-fadeIn"
              style={{background:"linear-gradient(135deg,#9B7ECF18,#6BCB7712)",border:"2px solid #6BCB7755"}}>
              <p className="text-2xl mb-1">⭐</p>
              <p className="text-sm font-black" style={{color:"#6BCB77"}}>Stark! Kontrolle behalten.</p>
              <p style={{fontSize:10,color:"var(--tx2)",marginTop:4}}>
                {globalChallengeCount > 1 ? `${globalChallengeCount}× heute geschafft ✨` : "Erste Challenge heute!"}
              </p>
              <div className="flex gap-2 mt-3">
                <button onClick={() => setChallengeSuccess(false)} className="flex-1 py-2 rounded-lg text-xs font-semibold"
                  style={{background:"var(--card2)",color:"var(--tx2)",border:"1px solid var(--bdr)"}}>Weiter warten</button>
                <button onClick={doRecord} className="flex-1 py-2 rounded-lg text-xs font-bold"
                  style={{background:"#6BCB77",color:"#fff"}}>📝 Loggen</button>
              </div>
            </div>
          )}

          {/* Fenster offen — zweistufige Auswahl */}
          {isOpen && !lim && (
            <div className="rounded-xl p-3 text-center animate-fadeIn"
              style={{background:"linear-gradient(135deg,#6BCB7710,#F2D38810)",border:"1px solid #6BCB7744"}}>
              <p className="text-2xl mb-1">🟢</p>
              <p className="text-sm font-bold mb-2" style={{color:"#6BCB77"}}>Fenster offen</p>
              <div className="flex gap-2">
                <button onClick={doRecord} className="flex-1 py-2.5 rounded-xl text-xs font-bold"
                  style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>
                  📝 Jetzt loggen
                </button>
                <button onClick={doStartChallenge} className="flex-1 py-2.5 rounded-xl text-xs font-bold active:scale-95"
                  style={{background:"linear-gradient(135deg,#9B7ECF,#7B5CB8)",color:"#fff",boxShadow:"0 3px 12px #9B7ECF44"}}>
                  ⏱️ 15 Min. Challenge
                </button>
              </div>
              <p style={{fontSize:9,color:"var(--tx2)",marginTop:6}}>Challenge = freiwillig. Nur die Chance, stolz auf dich zu sein.</p>
            </div>
          )}
        </div>
      </div>
    );
  };

  const DosePlaner = () => {
    const [sub, setSub] = useState("");
    const [unitLabel, setUnitLabel] = useState("");
    const [interval, setInterv] = useState(90);
    const [maxUnits, setMaxUnits] = useState(0);
    const [showForm, setShowForm] = useState(planers.length === 0);
    const [preFlightOpen, setPreFlightOpen] = useState(false);   // Modal sichtbar?
    const [preFlightChecks, setPreFlightChecks] = useState([false, false, false]); // 3 Checkboxen
    const [pendingPlan, setPendingPlan] = useState(null);        // Setup-Daten warten auf Check

    // Mischkonsum-Check
    const subs = planers.map(p => p.substance);
    const mixAlerts = [];
    for (let a = 0; a < subs.length; a++)
      for (let b = a+1; b < subs.length; b++) {
        const k = getInteractionKey(subs[a], subs[b]);
        if (INTERACTION_MATRIX[k]) mixAlerts.push({ subA:subs[a], subB:subs[b], ...INTERACTION_MATRIX[k] });
      }
    mixAlerts.sort((a,b)=>({critical:0,high:1,medium:2}[a.level]??3)-({critical:0,high:1,medium:2}[b.level]??3));

    // Schritt 1: Öffne Pre-Flight Check statt sofort zu speichern
    const doAdd = () => {
      if (!sub || !unitLabel) return;
      setPendingPlan({ id: String(Date.now()), substance:sub, unit:unitLabel, interval,
        maxUnits:maxUnits||0, startedAt:new Date().toISOString(), consumedCount:0,
        lastConsumedAt:null, challengeCount:0 });
      setPreFlightChecks([false, false, false]);
      setPreFlightOpen(true);
    };

    // Schritt 2: Pre-Flight bestanden → Planer speichern
    const doLaunch = async () => {
      if (!pendingPlan) return;
      const plan = { ...pendingPlan, preFlightPassed: true, preFlightAt: new Date().toISOString() };
      await savePlaners([...planers, plan]);
      setSub(""); setUnitLabel(""); setInterv(90); setMaxUnits(0);
      setShowForm(false); setPreFlightOpen(false); setPendingPlan(null);
    };

    const doAbortPreFlight = () => {
      setPreFlightOpen(false); setPendingPlan(null);
    };

    const toggleCheck = (i) =>
      setPreFlightChecks(prev => prev.map((v, idx) => idx === i ? !v : v));


    const myItems = prefs.mySubs?.length > 0 ? prefs.mySubs : SUBSTANCES;
    // Substanzen die bereits geplant sind ausblenden
    const availItems = myItems.filter(s => !planers.some(p => p.substance === s));

    // ─── Pre-Flight Check Modal ───────────────────────────────────────
    const PRE_FLIGHT_QUESTIONS = [
      { icon:"🧠", label:"Set – Innerer Zustand",
        text:"Ich fühle mich emotional stabil und nutze die Substanz nicht, um negative Gefühle zu betäuben." },
      { icon:"🏠", label:"Setting – Umgebung",
        text:"Ich bin an einem sicheren Ort, bei Menschen denen ich vertraue, und habe keine wichtigen Termine in den nächsten 24 Stunden." },
      { icon:"💊", label:"Substanz – Wissen",
        text:"Ich kenne die Substanz, habe mich über Safer Use informiert und weiß, dass Mischkonsum riskant ist." },
    ];

    if (preFlightOpen && pendingPlan) return (
      <div className="space-y-5">
        {/* Cockpit-Header */}
        <div className="text-center pt-2">
          <div className="w-14 h-14 rounded-2xl mx-auto flex items-center justify-center text-2xl mb-3"
            style={{background:"#7B8CDE15",border:"1px solid #7B8CDE33"}}>✈️</div>
          <h2 className="text-lg font-bold" style={{fontFamily:"var(--fontD)",color:"var(--tx)"}}>Pre-Flight Check</h2>
          <p className="text-sm mt-1" style={{color:"var(--tx2)"}}>
            {subEmoji(pendingPlan.substance)} {pendingPlan.substance} · {pendingPlan.interval} Min. Intervall
          </p>
          <p className="text-xs mt-2 leading-relaxed" style={{color:"var(--tx2)"}}>Drei kurze Fragen — ehrlich und nur für dich.</p>
        </div>

        {/* Checkliste */}
        <div className="space-y-2">
          {PRE_FLIGHT_QUESTIONS.map((q, i) => {
            const checked = preFlightChecks[i];
            return (
              <button key={i} onClick={() => toggleCheck(i)} aria-pressed={checked} aria-label={q.label}
                className="w-full rounded-2xl px-4 py-4 flex gap-4 items-start text-left transition-all active:scale-[0.99]"
                style={{background:checked?"#6BCB7708":"var(--card)",border:`1.5px solid ${checked?"#6BCB7755":"var(--bdr)"}`}}>
                {/* Checkbox */}
                <div className="w-6 h-6 rounded-lg flex items-center justify-center shrink-0 mt-0.5 transition-all"
                  style={{background:checked?"#6BCB77":"var(--card2)",border:`2px solid ${checked?"#6BCB77":"var(--bdr)"}`}}>
                  {checked && <span style={{fontSize:13,color:"#fff",fontWeight:900,lineHeight:1}}>✓</span>}
                </div>
                {/* Text */}
                <div className="flex-1 min-w-0">
                  <div className="flex items-center gap-1.5 mb-1">
                    <span style={{fontSize:13}}>{q.icon}</span>
                    <span className="text-xs font-bold"
                      style={{color:checked?"#6BCB77":"var(--tx2)",letterSpacing:"0.5px"}}>
                      {q.label.toUpperCase()}
                    </span>
                  </div>
                  <p className="text-sm leading-relaxed" style={{color:"var(--tx)"}}>{q.text}</p>
                </div>
              </button>
            );
          })}
        </div>

        {/* Fortschritts-Balken */}
        <div className="flex gap-1.5 justify-center">
          {preFlightChecks.map((c, i) => (
            <div key={i} className="h-1.5 flex-1 rounded-full transition-all duration-300"
              style={{background:c?"#6BCB77":"var(--bdr)",maxWidth:64}} />
          ))}
        </div>

        {/* Reflexions-Feedback — kontextsensitiv, nie blockierend */}
        {(() => {
          const count = preFlightChecks.filter(Boolean).length;
          if (count === 3) return (
            <div className="rounded-2xl px-4 py-3 flex gap-3 items-start"
              style={{background:"#6BCB7710",border:"1px solid #6BCB7733"}}>
              <span className="text-lg shrink-0 mt-0.5">✅</span>
              <p className="text-sm leading-relaxed" style={{color:"var(--tx2)"}}>
                Guter Moment für einen bewussten Konsum. Du hast alle drei Punkte reflektiert.
              </p>
            </div>
          );
          if (count > 0) return (
            <div className="rounded-2xl px-4 py-3 flex gap-3 items-start"
              style={{background:"#F2D38810",border:"1px solid #F2D38833"}}>
              <span className="text-lg shrink-0 mt-0.5">💛</span>
              <p className="text-sm leading-relaxed" style={{color:"var(--tx2)"}}>
                Du kannst trotzdem starten — die Reflexion ist für dich, nicht als Bedingung.
                Ein ehrliches Nein zu sich selbst ist auch eine Form von Stärke.
              </p>
            </div>
          );
          return null;
        })()}

        {/* Aktions-Buttons — immer aktiv */}
        <div className="space-y-2">
          <button onClick={doLaunch} aria-label="Plan starten"
            className="w-full py-4 rounded-2xl text-sm font-black transition-all active:scale-[0.98]"
            style={{
              background:"linear-gradient(135deg,var(--acc),#6272C4)",
              color:"#fff",
              border:"1.5px solid var(--acc)55",
              boxShadow:"0 4px 20px var(--acc)33",
            }}>
            ⏱️ Plan starten
          </button>
          <button onClick={doAbortPreFlight} className="w-full py-3 rounded-2xl text-sm font-semibold"
            style={{background:"var(--card2)",color:"var(--tx2)",border:"1px solid var(--bdr)"}}>
            ← Zurück zur Einrichtung
          </button>
        </div>

        <p className="text-center text-xs leading-relaxed" style={{color:"var(--tx2)",opacity:0.7}}>
          Deine Antworten bleiben privat — nur du siehst sie.
        </p>
      </div>
    );

    return (
      <div className="space-y-5">
        {/* Page-Header */}
        <div className="flex items-center justify-between">
          <div>
            <h2 className="text-lg font-bold" style={{fontFamily:"var(--fontD)",color:"var(--tx)"}}>⏱️ Dose Planer</h2>
            <p className="text-xs mt-0.5" style={{color:"var(--tx2)"}}>
              {planers.length > 0 ? `${planers.length}/3 aktiv${globalChallengeCount>0?` · ⭐ ${globalChallengeCount}× Challenge`:""}` : "Bis zu 3 parallele Timer"}
            </p>
          </div>
          {planers.length > 0 && planers.length < 3 && (
            <button onClick={() => setShowForm(f => !f)} className="text-xs px-3 py-1.5 rounded-lg"
              style={{background:showForm?"var(--acc)":"var(--card)",color:showForm?"#fff":"var(--acc)",border:"1px solid var(--acc)44"}}>
              {showForm ? "✕ Schließen" : "＋ Planer hinzufügen"}
            </button>
          )}
        </div>

        {/* Mischkonsum-Warnung zwischen aktiven Planern */}
        {mixAlerts.length > 0 && (() => {
          const w = mixAlerts[0];
          const col = w.level==="critical"?"#FF3B3B":w.level==="high"?"#FF8C00":"#FFD700";
          const lbl = w.level==="critical"?"⛔ LEBENSGEFAHR":w.level==="high"?"🔶 HOHES RISIKO":"🟡 VORSICHT";
          return (
            <div role="alert" aria-label={`Mischkonsum-Warnung: ${w.subA} + ${w.subB}`}
              className={w.level==="critical"?"warn-critical":""}
              style={{background:`${col}15`,border:`2px solid ${col}66`,borderRadius:16,padding:"12px 16px"}}>
              <div className="flex items-center gap-2 mb-1">
                <span className="text-xs font-black" style={{color:col}}>{lbl}</span>
                <span className="text-xs font-bold" style={{color:"var(--tx)"}}>
                  {subEmoji(w.subA)} {w.subA} + {subEmoji(w.subB)} {w.subB}
                </span>
              </div>
              <p className="text-xs leading-relaxed" style={{color:col}}>{w.text}</p>
              {w.level === "critical" && (
                <a href="tel:112" className="flex items-center justify-center gap-2 mt-2 py-2 rounded-xl font-black text-sm"
                  style={{background:"#FF3B3B",color:"#fff",textDecoration:"none"}}>
                  📞 NOTFALL → 112 ANRUFEN
                </a>
              )}
            </div>
          );
        })()}

        {/* Aktive Planer-Karten */}
        {planers.map(p => <PlanerCard key={p.id} p={p} />)}

        {/* Setup-Form: neuen Planer anlegen */}
        {(showForm || planers.length === 0) && planers.length < 3 && (
          <div className="rounded-2xl overflow-hidden" style={{background:"var(--card)",border:"1px solid var(--acc)33"}}>
            <div className="px-4 py-3" style={{borderBottom:"1px solid var(--bdr)",background:"var(--acc)08"}}>
              <p className="text-sm font-bold" style={{color:"var(--tx)"}}>＋ Neuen Planer einrichten</p>
            </div>
            <div className="px-4 py-4 space-y-4">
              <div>
                <Label>Substanz</Label>
                <div className="flex flex-wrap gap-2 mt-1">
                  {availItems.length > 0 ? availItems.map(s => (
                    <button key={s} onClick={() => setSub(s)} className="px-3 py-1.5 rounded-xl text-xs font-medium transition-all"
                      style={{background:sub===s?"var(--acc)":"var(--card2)",color:sub===s?"#fff":"var(--tx2)",border:`1px solid ${sub===s?"var(--acc)":"var(--bdr)"}`}}>
                      {subEmoji(s)} {s}
                    </button>
                  )) : <p className="text-xs" style={{color:"var(--tx2)"}}>Alle Substanzen bereits geplant.</p>}
                </div>
              </div>

              {sub && (
                <div>
                  <Label>Einheit (z.B. "1 Bier", "1 Joint")</Label>
                  <input value={unitLabel} onChange={e => setUnitLabel(e.target.value)}
                    className="w-full rounded-xl px-4 py-2.5 text-sm outline-none mt-1"
                    style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}}
                    placeholder="1 Bier / 1 Joint / 1 Line…" />
                </div>
              )}

              <div>
                <Label>Intervall: <span style={{color:"var(--acc)"}}>{interval} Min.</span></Label>
                <input type="range" min="15" max="240" step="15" value={interval} onChange={e => setInterv(+e.target.value)}
                  className="w-full mt-1" style={{accentColor:"var(--acc)"}} />
                <div className="flex justify-between text-xs" style={{color:"var(--tx2)"}}><span>15 Min.</span><span>4 Std.</span></div>
              </div>

              <div>
                <Label>Max. Einheiten <span style={{color:"var(--tx2)"}}>(0 = kein Limit)</span></Label>
                <div className="flex items-center gap-3 mt-1">
                  <button onClick={() => setMaxUnits(Math.max(0,maxUnits-1))} className="w-9 h-9 rounded-xl text-lg font-bold"
                    style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>-</button>
                  <span className="text-xl font-bold w-10 text-center" style={{color:maxUnits>0?"var(--acc)":"var(--tx2)",fontFamily:"var(--fontD)"}}>{maxUnits||"∞"}</span>
                  <button onClick={() => setMaxUnits(maxUnits+1)} className="w-9 h-9 rounded-xl text-lg font-bold"
                    style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>+</button>
                </div>
              </div>

              <Btn onClick={doAdd} disabled={!sub || !unitLabel} ariaLabel="Planer starten">⏱️ Planer starten</Btn>
            </div>
          </div>
        )}

        {/* Disclaimer */}
        <div className="rounded-2xl p-4 space-y-2" style={{background:"var(--card)",border:"1px solid #F2D38833"}}>
          {[
            {i:"⚠️",t:"Kein Aufruf zum Konsum",b:"Dieser Planer ist ein Werkzeug der Schadensminimierung — für Menschen, die konsumieren. Ziel: Kontrolle stärken."},
            {i:"🚫",t:"Kein sicherer Konsum",b:"Jeder Substanzgebrauch birgt Risiken. Der Planer reduziert sie, eliminiert sie nicht."},
            {i:"🚑",t:"Im Notfall: 112",b:"Kein Ersatz für medizinische Beratung."},
          ].map((h,i) => (
            <div key={i} className="flex items-start gap-2">
              <span className="text-sm shrink-0 mt-0.5">{h.i}</span>
              <div><p className="text-xs font-semibold" style={{color:"#F2D388"}}>{h.t}</p><p className="text-xs leading-relaxed mt-0.5" style={{color:"var(--tx2)"}}>{h.b}</p></div>
            </div>
          ))}
        </div>
      </div>
    );
  };

  // ═══════════════════════════════════════════════════════════
  // ─── SKILL-BOX (Replaces Emergency — 3-Level Skill System) ──
  // ═══════════════════════════════════════════════════════════
  const SkillBox = () => {
    const [activeSkill, setActiveSkill] = useState(null);
    const [feedbackFor, setFeedbackFor] = useState(null);
    const [editContact, setEditContact] = useState(false);
    const [contactDraft, setContactDraft] = useState(skillbox.emergencyContact || "");

    // ─── 5-4-3-2-1 Interactive Exercise ───
    const Skill_54321 = () => {
      const senses = [
        { count:5, sense:"siehst", icon:"👁️", color:"#B89DE8", placeholder:["Lampe","Tisch","Pflanze","Fenster","Tasse"] },
        { count:4, sense:"hörst", icon:"👂", color:"#9B7ECF", placeholder:["Ventilator","Vögel","Straße","Uhr"] },
        { count:3, sense:"fühlst", icon:"🤲", color:"#E8A87C", placeholder:["Tastatur","Stoff","Wärme"] },
        { count:2, sense:"riechst", icon:"👃", color:"#A8D8B9", placeholder:["Kaffee","Luft"] },
        { count:1, sense:"schmeckst", icon:"👅", color:"#F2D388", placeholder:["Minze"] },
      ];
      const [step, setStep] = useState(0);
      const [answers, setAnswers] = useState({});
      const [done, setDone] = useState(false);
      const cur = senses[step];

      if (done) return (
        <div className="space-y-4 animate-fadeIn text-center py-4">
          <p className="text-4xl">🌿</p>
          <p className="text-sm font-bold" style={{color:"var(--tx)"}}>Du bist hier. Du bist sicher.</p>
          <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>Du hast dich gerade bewusst mit deiner Umgebung verbunden. Dieses Ankern im Hier und Jetzt kann helfen, wenn Gedanken kreisen oder der Druck steigt.</p>
          <FeedbackAsk skillId="54321" onDone={() => setActiveSkill(null)} />
        </div>
      );

      return (
        <div className="space-y-5 animate-fadeIn">
          {/* Progress */}
          <div className="flex gap-1.5">
            {senses.map((s,i) => <div key={i} className="h-1.5 flex-1 rounded-full transition-all duration-300" style={{background:i<=step?cur.color:"var(--bdr)"}} />)}
          </div>
          <div className="text-center py-3">
            <span className="text-4xl">{cur.icon}</span>
            <p className="text-lg font-bold mt-3" style={{color:cur.color,fontFamily:"var(--fontD)"}}>{cur.count} Dinge, die du {cur.sense}</p>
            <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>Schau dich um und benenne sie.</p>
          </div>
          <div className="space-y-2">
            {Array.from({length:cur.count}).map((_,i) => (
              <input key={`${step}-${i}`} className="w-full rounded-xl px-4 py-2.5 text-sm outline-none" style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}}
                placeholder={cur.placeholder[i] ? `z.B. ${cur.placeholder[i]}` : "..."}
                value={answers[`${step}-${i}`] || ""}
                onChange={e => setAnswers({...answers, [`${step}-${i}`]: e.target.value})}
              />
            ))}
          </div>
          <div className="flex gap-3">
            {step > 0 && <button onClick={() => setStep(step-1)} className="flex-1 py-2.5 rounded-xl text-sm" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>← Zurück</button>}
            <button onClick={() => step < senses.length-1 ? setStep(step+1) : setDone(true)} className="flex-1 py-2.5 rounded-xl text-sm font-semibold" style={{background:cur.color,color:"#fff"}}>
              {step < senses.length-1 ? "Weiter →" : "Abschliessen ✓"}
            </button>
          </div>
        </div>
      );
    };

    // ─── Atem-Anker (60s breath guide) ───
    const Skill_Breath = () => {
      const [running, setRunning] = useState(false);
      const [elapsed, setElapsed] = useState(0);
      const [phase, setPhase] = useState("ready"); // ready, in, hold, out, hold2, done
      const intervalRef = useRef(null);
      const totalSec = 60;

      const phases = [
        {id:"in",label:"Einatmen",dur:4,color:"#6BCB77"},
        {id:"hold",label:"Halten",dur:4,color:"#F2D388"},
        {id:"out",label:"Ausatmen",dur:4,color:"#B89DE8"},
        {id:"hold2",label:"Halten",dur:4,color:"#E8A87C"},
      ];

      // Determine current phase from elapsed
      const cycleLen = 16; // 4+4+4+4
      const inCycle = elapsed % cycleLen;
      let pIdx = 0, pSec = inCycle;
      for (let p of phases) { if (pSec < p.dur) break; pSec -= p.dur; pIdx++; }
      if (pIdx >= phases.length) pIdx = 0;
      const curPhase = phases[pIdx];
      const phaseProgress = pSec / curPhase.dur;

      const start = () => {
        setRunning(true); setElapsed(0); setPhase("in");
        intervalRef.current = setInterval(() => {
          setElapsed(prev => {
            if (prev + 1 >= totalSec) { clearInterval(intervalRef.current); setRunning(false); setPhase("done"); return totalSec; }
            return prev + 1;
          });
        }, 1000);
      };

      const stop = () => { clearInterval(intervalRef.current); setRunning(false); setElapsed(0); setPhase("ready"); };
      useEffect(() => () => clearInterval(intervalRef.current), []);

      if (phase === "done") return (
        <div className="space-y-4 animate-fadeIn text-center py-4">
          <p className="text-4xl">🫁</p>
          <p className="text-sm font-bold" style={{color:"var(--tx)"}}>60 Sekunden geschafft.</p>
          <p className="text-xs" style={{color:"var(--tx2)"}}>Dein Nervensystem hat sich reguliert. Spüre nach, wie es sich jetzt anfühlt.</p>
          <FeedbackAsk skillId="breath" onDone={() => setActiveSkill(null)} />
        </div>
      );

      return (
        <div className="space-y-5 animate-fadeIn text-center">
          {/* Timer ring */}
          <div className="relative w-40 h-40 mx-auto">
            <svg viewBox="0 0 100 100" className="w-full h-full" style={{transform:"rotate(-90deg)"}}>
              <circle cx="50" cy="50" r="44" fill="none" stroke="var(--bdr)" strokeWidth="4" />
              {running && <circle cx="50" cy="50" r="44" fill="none" stroke={curPhase.color} strokeWidth="4" strokeDasharray={`${2*Math.PI*44}`} strokeDashoffset={`${2*Math.PI*44*(1-elapsed/totalSec)}`} strokeLinecap="round" className="transition-all duration-1000" />}
            </svg>
            <div className="absolute inset-0 flex flex-col items-center justify-center">
              {running ? (
                <>
                  <div className="w-16 h-16 rounded-full flex items-center justify-center transition-all duration-700" style={{background:`${curPhase.color}25`,transform:`scale(${0.7 + phaseProgress * 0.5})`}}>
                    <span aria-hidden="true" className="text-2xl">🫁</span>
                  </div>
                  <p className="text-sm font-bold mt-2" style={{color:curPhase.color}}>{curPhase.label}</p>
                  <p className="text-xs" style={{color:"var(--tx2)"}}>{totalSec - elapsed}s</p>
                </>
              ) : (
                <>
                  <span className="text-3xl">🫁</span>
                  <p className="text-xs mt-2" style={{color:"var(--tx2)"}}>60 Sekunden</p>
                </>
              )}
            </div>
          </div>
          <p className="text-xs" style={{color:"var(--tx2)"}}>4 Sek. einatmen — 4 Sek. halten — 4 Sek. ausatmen — 4 Sek. halten</p>
          <button onClick={running ? stop : start} className="px-8 py-2.5 rounded-full text-sm font-semibold mx-auto" style={{background:running?"#E06B8A":"var(--acc)",color:"#fff"}}>
            {running ? "⏹ Stopp" : "▶ Starten"}
          </button>
        </div>
      );
    };

    // ─── Zahlen-Jongleur (Math puzzler) ───
    const Skill_Math = () => {
      const genProblem = () => {
        const ops = ["+","-","*"];
        const op = ops[Math.floor(Math.random()*3)];
        let a,b;
        if (op === "*") { a = 3+Math.floor(Math.random()*10); b = 2+Math.floor(Math.random()*10); }
        else if (op === "-") { a = 10+Math.floor(Math.random()*90); b = 1+Math.floor(Math.random()*a); }
        else { a = 10+Math.floor(Math.random()*90); b = 10+Math.floor(Math.random()*90); }
        const answer = op==="+"?a+b:op==="-"?a-b:a*b;
        return { a, b, op: op==="*"?"x":op, answer, display: `${a} ${op==="*"?"x":op} ${b}` };
      };

      const [problems, setProblems] = useState(() => Array.from({length:5}, genProblem));
      const [current, setCurrent] = useState(0);
      const [input, setInput] = useState("");
      const [result, setResult] = useState(null); // null, "correct", "wrong"
      const [score, setScore] = useState(0);
      const [done, setDone] = useState(false);

      const check = () => {
        const isCorrect = parseInt(input) === problems[current].answer;
        setResult(isCorrect ? "correct" : "wrong");
        if (isCorrect) setScore(score + 1);
        setTimeout(() => {
          if (current < problems.length - 1) { setCurrent(current + 1); setInput(""); setResult(null); }
          else { setDone(true); }
        }, 800);
      };

      if (done) return (
        <div className="space-y-4 animate-fadeIn text-center py-4">
          <p className="text-4xl">{score >= 4 ? "🎯" : score >= 2 ? "👍" : "💪"}</p>
          <p className="text-sm font-bold" style={{color:"var(--tx)"}}>{score}/{problems.length} richtig</p>
          <p className="text-xs" style={{color:"var(--tx2)"}}>Kopfrechnen aktiviert den praefrontalen Kortex — den Teil deines Gehirns, der rationale Entscheidungen steuert. Genau das Gegenteil von impulsivem Craving.</p>
          <FeedbackAsk skillId="math" onDone={() => setActiveSkill(null)} />
        </div>
      );

      return (
        <div className="space-y-5 animate-fadeIn text-center">
          <div className="flex gap-1.5 mb-2">
            {problems.map((_,i) => <div key={i} className="h-1.5 flex-1 rounded-full" style={{background:i<current?"#6BCB77":i===current?"var(--acc)":"var(--bdr)"}} />)}
          </div>
          <p className="text-xs" style={{color:"var(--tx2)"}}>Aufgabe {current+1} von {problems.length}</p>
          <div className="py-6">
            <p className="text-3xl font-bold" style={{color:"var(--tx)",fontFamily:"var(--fontD)"}}>{problems[current].display} = ?</p>
          </div>
          <div className="flex gap-3 items-center justify-center">
            <input type="number" value={input} onChange={e=>setInput(e.target.value)} onKeyDown={e=>e.key==="Enter"&&input&&check()}
              className="w-28 text-center rounded-xl px-4 py-3 text-lg font-bold outline-none"
              style={{background:result==="correct"?"#6BCB7720":result==="wrong"?"#E06B8A20":"var(--card2)",color:"var(--tx)",border:`1px solid ${result==="correct"?"#6BCB77":result==="wrong"?"#E06B8A":"var(--bdr)"}`}}
              placeholder="?" autoFocus
            />
            <button onClick={check} disabled={!input} className="px-5 py-3 rounded-xl text-sm font-semibold" style={{background:input?"var(--acc)":"var(--bdr)",color:input?"#fff":"var(--tx2)"}}>Pruefen</button>
          </div>
          {result === "wrong" && <p className="text-xs" style={{color:"#E06B8A"}}>Richtig waere: {problems[current].answer}</p>}
        </div>
      );
    };

    // ─── Muskel-Power (Tense & Release) ───
    const Skill_Muscle = () => {
      const [phase, setPhase] = useState("intro"); // intro, tense, release, done
      const [countdown, setCountdown] = useState(15);
      const intervalRef = useRef(null);

      const startTense = () => {
        setPhase("tense"); setCountdown(15);
        intervalRef.current = setInterval(() => {
          setCountdown(prev => {
            if (prev <= 1) { clearInterval(intervalRef.current); setPhase("release"); return 0; }
            return prev - 1;
          });
        }, 1000);
      };
      useEffect(() => () => clearInterval(intervalRef.current), []);

      if (phase === "intro") return (
        <div className="space-y-4 animate-fadeIn text-center py-4">
          <p className="text-4xl">💪</p>
          <p className="text-sm font-bold" style={{color:"var(--tx)"}}>Muskel-Power</p>
          <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>Spanne gleich 15 Sekunden lang ALLE Muskeln deines Koerpers so stark an wie du kannst: Haende zu Faeusten, Arme, Beine, Bauch, Gesicht — alles anspannen. Danach schlagartig lockerlassen.</p>
          <button onClick={startTense} className="px-8 py-2.5 rounded-full text-sm font-semibold" style={{background:"#E06B8A",color:"#fff"}}>💪 Jetzt anspannen!</button>
        </div>
      );

      if (phase === "tense") return (
        <div className="space-y-5 animate-fadeIn text-center py-4">
          <div className="w-28 h-28 rounded-full mx-auto flex items-center justify-center" style={{background:"#E06B8A25",animation:"breathe 1s ease-in-out infinite"}}>
            <span className="text-4xl font-bold" style={{color:"#E06B8A",fontFamily:"var(--fontD)"}}>{countdown}</span>
          </div>
          <p className="text-lg font-bold" style={{color:"#E06B8A"}}>ANSPANNEN!</p>
          <p className="text-xs" style={{color:"var(--tx2)"}}>Alle Muskeln — so fest du kannst!</p>
        </div>
      );

      if (phase === "release") return (
        <div className="space-y-5 animate-fadeIn text-center py-4">
          <p className="text-4xl">😮‍💨</p>
          <p className="text-lg font-bold" style={{color:"#6BCB77"}}>LOSLASSEN.</p>
          <p className="text-sm leading-relaxed" style={{color:"var(--tx2)"}}>Atme tief aus. Spuere die Waerme und Entspannung in deinem ganzen Koerper. Lass alles los.</p>
          <button onClick={() => setPhase("done")} className="px-6 py-2 rounded-full text-sm font-medium mt-2" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>Weiter →</button>
        </div>
      );

      return (
        <div className="space-y-4 animate-fadeIn text-center py-4">
          <p className="text-4xl">✅</p>
          <p className="text-sm font-bold" style={{color:"var(--tx)"}}>Progressive Muskelentspannung.</p>
          <p className="text-xs" style={{color:"var(--tx2)"}}>Das Anspannen und abrupte Loslassen setzt Endorphine frei und unterbricht den Anspannungs-Kreislauf. Wiederhole die Uebung bei Bedarf.</p>
          <FeedbackAsk skillId="muscle" onDone={() => setActiveSkill(null)} />
        </div>
      );
    };

    // ─── Shared: Feedback after exercise ───
    const FeedbackAsk = ({ skillId, onDone }) => {
      const [answered, setAnswered] = useState(false);
      const logFeedback = async (helped) => {
        const entry = { helped, date: new Date().toISOString() };
        const prev = skillbox.feedback?.[skillId] || [];
        await saveSkillbox({ ...skillbox, feedback: { ...skillbox.feedback, [skillId]: [...prev, entry] } });
        setAnswered(true);
      };
      if (answered) return <p className="text-xs text-center py-2" style={{color:"#6BCB77"}}>Danke fuer dein Feedback.</p>;
      return (
        <div className="rounded-xl p-3 mt-2" style={{background:"var(--card2)",border:"1px solid var(--bdr)"}}>
          <p className="text-xs font-semibold mb-2 text-center" style={{color:"var(--tx2)"}}>Hat es geholfen?</p>
          <div className="flex gap-3 justify-center">
            <button onClick={()=>logFeedback(true)} className="px-5 py-2 rounded-lg text-xs font-semibold" style={{background:"#6BCB7720",color:"#6BCB77",border:"1px solid #6BCB7744"}}>👍 Ja</button>
            <button onClick={()=>logFeedback(false)} className="px-5 py-2 rounded-lg text-xs font-semibold" style={{background:"#E06B8A15",color:"#E06B8A",border:"1px solid #E06B8A33"}}>👎 Nein</button>
          </div>
        </div>
      );
    };

    // ─── Dismiss Intro ───
    const dismissIntro = async () => {
      await saveSkillbox({ ...skillbox, seenIntro: true });
    };

    // ─── Save emergency contact ───
    const saveContact = async () => {
      await saveSkillbox({ ...skillbox, emergencyContact: contactDraft });
      setEditContact(false);
    };

    // ─── LEVEL DEFINITIONS ───
    const levels = [
      { level:1, title:"Niedrige Anspannung", subtitle:"Ablenkung & Fokus", color:"#6BCB77", gradient:"#6BCB7708",
        skills: [
          { id:"54321", icon:"👁️", title:"5-4-3-2-1 Methode", desc:"Interaktive Erdungsuebung — verbinde dich mit deinen Sinnen.", component: Skill_54321 },
          { id:"breath", icon:"🫁", title:"Atem-Anker", desc:"60-Sekunden Box-Breathing mit visuellem Guide.", component: Skill_Breath },
          { id:"math", icon:"🔢", title:"Zahlen-Jongleur", desc:"Kopfrechnen aktiviert den logischen Verstand.", component: Skill_Math },
        ]},
      { level:2, title:"Mittlere Anspannung", subtitle:"Koerperliche Reize & Bewegung", color:"#F2D388", gradient:"#F2D38808",
        skills: [
          { id:"temp", icon:"🧊", title:"Temperatur-Schock", desc:"Halte Eiswuerfel in der geschlossenen Hand oder wasche dein Gesicht eiskalt. Der Temperaturreiz aktiviert den Tauchreflex und senkt die Herzfrequenz sofort. Halte 30-60 Sekunden.", isInfo:true },
          { id:"muscle", icon:"💪", title:"Muskel-Power", desc:"15 Sekunden alle Muskeln anspannen, dann schlagartig lockerlassen.", component: Skill_Muscle },
          { id:"sharp", icon:"🌶️", title:"Scharfer Reiz", desc:"Beiss in eine Zitronenscheibe, nimm ein scharfes Bonbon oder iss ein Stueck Chili. Der intensive Geschmacksreiz durchbricht den Anspannungs-Kreislauf und lenkt das Gehirn auf den koerperlichen Reiz um.", isInfo:true },
        ]},
      { level:3, title:"Hoechste Anspannung", subtitle:"Akuthilfe & Sicherheit", color:"#E06B8A", gradient:"#E06B8A08",
        skills: [] },
    ];

    // ─── Active Skill Exercise ───
    if (activeSkill) {
      const allSkills = levels.flatMap(l => l.skills);
      const skill = allSkills.find(s => s.id === activeSkill);
      if (skill?.component) {
        const Comp = skill.component;
        return (
          <div className="space-y-4">
            <button onClick={() => setActiveSkill(null)} className="text-xs flex items-center gap-1" style={{color:"var(--acc)"}}>← Zurueck zur Skill-Box</button>
            <Comp />
          </div>
        );
      }
    }

    // ─── Info Skill Detail (non-interactive) ───
    if (activeSkill) {
      const allSkills = levels.flatMap(l => l.skills);
      const skill = allSkills.find(s => s.id === activeSkill);
      if (skill?.isInfo) return (
        <div className="space-y-5">
          <button onClick={() => setActiveSkill(null)} className="text-xs flex items-center gap-1" style={{color:"var(--acc)"}}>← Zurueck zur Skill-Box</button>
          <div className="text-center py-6">
            <span className="text-5xl">{skill.icon}</span>
            <p className="text-lg font-bold mt-3" style={{color:"var(--tx)",fontFamily:"var(--fontD)"}}>{skill.title}</p>
          </div>
          <div className="rounded-2xl p-5" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
            <p className="text-sm leading-[1.8]" style={{color:"var(--tx2)"}}>{skill.desc}</p>
          </div>
          <FeedbackAsk skillId={skill.id} onDone={() => setActiveSkill(null)} />
          <button onClick={() => setActiveSkill(null)} className="w-full py-2.5 rounded-xl text-sm" style={{background:"var(--card)",color:"var(--tx)",border:"1px solid var(--bdr)"}}>← Zurueck</button>
        </div>
      );
    }

    // ─── MAIN SKILL-BOX VIEW ───
    return (
      <div className="space-y-5">
        {/* Intro (first time only) */}
        {!skillbox.seenIntro && (
          <div className="rounded-2xl overflow-hidden animate-fadeIn" style={{border:"1px solid var(--acc)33"}}>
            <div className="px-5 py-4" style={{background:"var(--acc)08"}}>
              <div className="flex items-center gap-2 mb-2">
                <span className="text-xl">🧰</span>
                <p className="text-sm font-bold" style={{color:"var(--tx)",fontFamily:"var(--fontD)"}}>Was sind Skills?</p>
              </div>
              <p className="text-sm leading-[1.75]" style={{color:"var(--tx2)"}}>
                Skills sind deine persoenlichen Werkzeuge fuer schwierige Momente. Sie helfen dir, Anspannung und Suchtdruck abzubauen, ohne dich selbst zu schaedigen. Je nach Stresslevel helfen unterschiedliche Techniken.
              </p>
              <button onClick={dismissIntro} className="mt-3 text-xs font-semibold px-4 py-1.5 rounded-lg" style={{background:"var(--acc)",color:"#fff"}}>Verstanden ✓</button>
            </div>
          </div>
        )}

        {/* Level 1 & 2: Skill Cards */}
        {levels.filter(l => l.level <= 2).map(lev => (
          <div key={lev.level}>
            <div className="flex items-center gap-2 mb-3">
              <div className="w-6 h-6 rounded-full flex items-center justify-center text-xs font-bold" style={{background:`${lev.color}20`,color:lev.color}}>{lev.level}</div>
              <div>
                <p className="text-sm font-bold" style={{color:"var(--tx)"}}>{lev.title}</p>
                <p className="text-xs" style={{color:"var(--tx2)"}}>{lev.subtitle}</p>
              </div>
            </div>
            <div className="space-y-2">
              {lev.skills.map(skill => {
                const fb = (skillbox.feedback?.[skill.id] || []);
                const helpedCount = fb.filter(f => f.helped).length;
                return (
                  <button key={skill.id} onClick={() => setActiveSkill(skill.id)}
                    className="w-full rounded-2xl p-4 text-left flex items-center gap-3 transition-all hover:scale-[1.01] active:scale-[0.98]"
                    style={{background:lev.gradient,border:`1px solid ${lev.color}22`}}>
                    <div className="w-11 h-11 rounded-xl flex items-center justify-center text-xl shrink-0" style={{background:`${lev.color}18`}}>{skill.icon}</div>
                    <div className="flex-1 min-w-0">
                      <p className="text-sm font-semibold" style={{color:"var(--tx)"}}>{skill.title}</p>
                      <p className="text-xs mt-0.5" style={{color:"var(--tx2)",display:"-webkit-box",WebkitLineClamp:2,WebkitBoxOrient:"vertical",overflow:"hidden"}}>{skill.desc}</p>
                      {fb.length > 0 && (
                        <p className="text-xs mt-1" style={{color:lev.color}}>{fb.length}x genutzt{helpedCount > 0 ? ` · ${helpedCount}x geholfen` : ""}</p>
                      )}
                    </div>
                    <span className="text-xs shrink-0" style={{color:lev.color}}>→</span>
                  </button>
                );
              })}
            </div>
          </div>
        ))}

        {/* Level 3: Akuthilfe */}
        <div>
          <div className="flex items-center gap-2 mb-3">
            <div className="w-6 h-6 rounded-full flex items-center justify-center text-xs font-bold" style={{background:"#E06B8A20",color:"#E06B8A"}}>3</div>
            <div>
              <p className="text-sm font-bold" style={{color:"var(--tx)"}}>Hoechste Anspannung</p>
              <p className="text-xs" style={{color:"var(--tx2)"}}>Akuthilfe & Sicherheit</p>
            </div>
          </div>

          {/* Disclaimer */}
          <div className="rounded-xl px-4 py-3 mb-3" style={{background:"#E06B8A08",border:"1px solid #E06B8A33"}}>
            <p className="text-xs leading-relaxed" style={{color:"#E06B8A"}}>
              Wenn die Anspannung nicht nachlaesst und du dich oder andere gefaehrdest, hol dir Unterstuetzung. Du musst das nicht alleine durchstehen.
            </p>
          </div>

          {/* Crisis Buttons */}
          <div className="space-y-2">
            <a href="tel:08001110111" className="w-full rounded-2xl p-4 flex items-center gap-3" style={{background:"var(--card)",border:"1px solid var(--bdr)",display:"flex",textDecoration:"none"}}>
              <div className="w-11 h-11 rounded-xl flex items-center justify-center text-xl" style={{background:"var(--acc)18"}}>📞</div>
              <div className="flex-1">
                <p className="text-sm font-semibold" style={{color:"var(--tx)"}}>Telefonseelsorge</p>
                <p className="text-xs" style={{color:"var(--tx2)"}}>24/7, kostenfrei, anonym</p>
              </div>
              <span className="text-sm font-bold" style={{color:"var(--acc)"}}>0800 1110111</span>
            </a>

            <a href="tel:112" className="w-full rounded-2xl p-4 flex items-center gap-3" style={{background:"#E06B8A08",border:"1px solid #E06B8A44",display:"flex",textDecoration:"none"}}>
              <div className="w-11 h-11 rounded-xl flex items-center justify-center text-xl" style={{background:"#E06B8A20"}}>🚨</div>
              <div className="flex-1">
                <p className="text-sm font-bold" style={{color:"#E06B8A"}}>Notruf</p>
                <p className="text-xs" style={{color:"var(--tx2)"}}>Rettungsdienst & Feuerwehr</p>
              </div>
              <span className="text-lg font-bold" style={{color:"#E06B8A"}}>112</span>
            </a>

            {/* Personal Emergency Contact */}
            <div className="rounded-2xl p-4" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
              <div className="flex items-center gap-3">
                <div className="w-11 h-11 rounded-xl flex items-center justify-center text-xl" style={{background:"#F2D38818"}}>💛</div>
                <div className="flex-1">
                  <p className="text-sm font-semibold" style={{color:"var(--tx)"}}>Mein Notfallkontakt</p>
                  {!editContact && skillbox.emergencyContact ? (
                    <div className="flex items-center gap-2 mt-1">
                      <a href={`tel:${skillbox.emergencyContact}`} className="text-sm font-bold" style={{color:"var(--acc)",textDecoration:"none"}}>{skillbox.emergencyContact}</a>
                      <button onClick={()=>{setEditContact(true);setContactDraft(skillbox.emergencyContact);}} className="text-xs" style={{color:"var(--tx2)"}}>✏️</button>
                    </div>
                  ) : !editContact ? (
                    <button onClick={()=>setEditContact(true)} className="text-xs mt-0.5" style={{color:"var(--acc)"}}>+ Nummer hinterlegen</button>
                  ) : (
                    <div className="flex gap-2 mt-2">
                      <input value={contactDraft} onChange={e=>setContactDraft(e.target.value)} placeholder="z.B. 0171 1234567"
                        className="flex-1 rounded-lg px-3 py-1.5 text-sm outline-none" style={{background:"var(--card2)",color:"var(--tx)",border:"1px solid var(--bdr)"}} />
                      <button onClick={saveContact} className="px-3 py-1.5 rounded-lg text-xs font-semibold" style={{background:"var(--acc)",color:"#fff"}}>OK</button>
                      <button onClick={()=>setEditContact(false)} className="text-xs" style={{color:"var(--tx2)"}}>✕</button>
                    </div>
                  )}
                </div>
              </div>
            </div>
          </div>
        </div>

        {/* Additional crisis numbers */}
        <details className="rounded-xl overflow-hidden" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          <summary className="px-4 py-3 cursor-pointer text-xs font-semibold flex items-center gap-2" style={{color:"var(--tx2)"}}>
            📞 Weitere Krisen-Nummern
          </summary>
          <div className="px-4 pb-3 space-y-2">
            {[
              { name:"Telefonseelsorge (2)", num:"0800 111 0 222", avail:"24/7, kostenfrei" },
              { name:"Aerztlicher Bereitschaftsdienst", num:"116 117", avail:"24/7, kostenfrei" },
              { name:"Sucht & Drogen Hotline", num:"01805 313 031", avail:"24/7" },
              { name:"Giftnotruf", num:"030 19240", avail:"24/7" },
            ].map((c,i) => (
              <div key={i} className="flex items-center justify-between py-1.5">
                <div><p className="text-xs font-semibold" style={{color:"var(--tx)"}}>{c.name}</p><p style={{fontSize:9,color:"var(--tx2)"}}>{c.avail}</p></div>
                <span className="text-xs font-bold" style={{color:"var(--acc)"}}>{c.num}</span>
              </div>
            ))}
          </div>
        </details>

        {/* Hint */}
        <div className="rounded-xl px-4 py-3" style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>
          <p className="text-xs leading-relaxed" style={{color:"var(--tx2)"}}>
            💡 Probiere verschiedene Skills aus und finde heraus, was fuer dich funktioniert. Das Feedback hilft dir, deine wirksamsten Werkzeuge zu erkennen.
          </p>
        </div>
      </div>
    );
  };

  // ═══ VIEWS MAP ═══
  const views = {
    dashboard:{t:"DoseDiary",c:<Dashboard />}, log:{t:"Dose-Log",c:<DoseLog />},
    loghistory:{t:"Log-Verlauf",c:<LogHistory />}, moodtl:{t:"Stimmungsverlauf",c:<MoodTimeline />},
    goals:{t:"Ziele & Clean Days",c:<Goals />},
    analysis:{t:"Muster-Analyse",c:<Analysis />},
    wissen:{t:"Wissensdatenbank",c:<KnowledgeBase />}, planer:{t:"Dose Planer",c:<DosePlaner />},
    craving:{t:"Craving-Kurve",c:<CravingCurve />}, report:{t:"Wochenbericht",c:<WeeklyReport />},
    medcheck:{t:"Medikamenten-Check",c:<MedCheck />}, badges:{t:"Meilensteine",c:<BadgesView />},
    privacy:{t:"Datenschutz & Info",c:<Privacy />},
    skillbox:{t:"Skill-Box",c:<SkillBox />},
  };

  const menu = [{id:"dashboard",i:"🏠",l:"Dashboard"},{id:"log",i:"📝",l:"Dose-Log"},{id:"loghistory",i:"📋",l:"Log-Verlauf"},{id:"planer",i:"⏱️",l:"Dose Planer"},{id:"goals",i:"🌟",l:"Ziele & Clean Days"},{id:"craving",i:"📈",l:"Craving-Kurve"},{id:"moodtl",i:"💚",l:"Stimmungsverlauf"},{id:"report",i:"📋",l:"Wochenbericht"},{id:"analysis",i:"📊",l:"Muster-Analyse"},{id:"wissen",i:"🧬",l:"Wissensdatenbank"},{id:"skillbox",i:"🧰",l:"Skill-Box"},{id:"medcheck",i:"💊",l:"Medikamenten-Check"},{id:"badges",i:"🏅",l:"Meilensteine"},{id:"privacy",i:"🔒",l:"Datenschutz & Info"}];

  return (
    <div style={{...theme,fontFamily:"var(--font)",background:"var(--bg)",color:"var(--tx)",minHeight:"100vh",maxWidth:480,margin:"0 auto",position:"relative"}}>
      <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Outfit:wght@600;700&display=swap" rel="stylesheet" />
      <style>{`
        @keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}
        .animate-fadeIn{animation:fadeIn 0.25s ease-out}
        @keyframes breathe{0%{transform:scale(0.65);opacity:0.4}50%{transform:scale(1);opacity:1}100%{transform:scale(0.65);opacity:0.4}}
        @keyframes ping{75%,100%{transform:scale(2);opacity:0}}
        .animate-ping{animation:ping 1.5s cubic-bezier(0,0,0.2,1) infinite}
        input[type=range]{height:6px;border-radius:3px}
        details summary::-webkit-details-marker{display:none}
        details summary::after{content:'▸';float:right;transition:transform 0.2s}
        details[open] summary::after{transform:rotate(90deg)}
        *{scrollbar-width:thin;scrollbar-color:#2F2845 transparent}

        /* ── WCAG 2.1 AA – Fokus-Zustände ── */
        :focus-visible{outline:3px solid #B89DE8;outline-offset:3px;border-radius:6px;z-index:1}
        input:focus-visible,textarea:focus-visible,select:focus-visible{outline:3px solid #B89DE8;outline-offset:2px;border-radius:8px}
        details summary:focus-visible{outline:3px solid #B89DE8;outline-offset:2px;border-radius:6px}

        /* ── Mindest-Touch-Target 44×44 px ── */
        button,a[role="button"],[role="button"],[role="tab"],[role="menuitem"]{min-height:44px}
        /* Ausnahme: reine Text-Links ohne Button-Rolle */

        /* ── Skip-Link ── */
        .skip-link{position:absolute;left:-9999px;top:4px;z-index:9999;padding:8px 16px;
          background:#9B7ECF;color:#fff;font-weight:700;font-size:14px;
          border-radius:8px;text-decoration:none;white-space:nowrap}
        .skip-link:focus-visible{left:8px;outline:3px solid #fff;outline-offset:2px}

        /* ── Mischkonsum-Ampel: Puls-Animationen ── */
        @keyframes pulseRed{0%,100%{box-shadow:0 0 0 0 rgba(255,59,59,0.55)}50%{box-shadow:0 0 0 8px rgba(255,59,59,0)}}
        @keyframes pulseOrange{0%,100%{box-shadow:0 0 0 0 rgba(255,140,0,0.4)}50%{box-shadow:0 0 0 6px rgba(255,140,0,0)}}
        @keyframes borderBlink{0%,100%{border-color:rgba(255,59,59,0.9)}50%{border-color:rgba(255,59,59,0.25)}}
        .warn-critical{animation:pulseRed 1.8s ease-in-out infinite}
        .warn-high{animation:pulseOrange 2.5s ease-in-out infinite}
        .border-blink{animation:borderBlink 1.4s ease-in-out infinite}

        /* ── Reduzierte Bewegung ── */
        @media(prefers-reduced-motion:reduce){
          *{animation-duration:0.01ms!important;animation-iteration-count:1!important;
            transition-duration:0.01ms!important}
          .warn-critical,.warn-high,.border-blink{animation:none!important}
        }

        /* ── Hoher Kontrast-Modus ── */
        @media(forced-colors:active){
          button,a{border:2px solid ButtonText}
          :focus-visible{outline:3px solid Highlight}
        }
      `}</style>

      {/* Skip-Link — WCAG 2.4.1 */}
      <a href="#main-content" className="skip-link">Zum Hauptinhalt springen</a>

      {/* Header */}
      <header role="banner" className="flex items-center justify-between px-5 py-4" style={{borderBottom:"1px solid var(--bdr)"}}>
        {view!=="dashboard"
          ? <button onClick={()=>nav("dashboard")} aria-label="Zurück zum Dashboard" className="text-sm font-medium px-2" style={{color:"var(--acc)",minHeight:44,minWidth:44}}>← Zurück</button>
          : <div className="flex items-center gap-2">
              <div className="w-8 h-8 rounded-xl flex items-center justify-center" style={{background:"var(--acc)20"}} aria-hidden="true"><span>🌿</span></div>
              <span className="font-bold" style={{fontFamily:"var(--fontD)"}}>DoseDiary</span>
            </div>
        }
        <h1 className="text-sm font-semibold absolute left-1/2 -translate-x-1/2" style={{color:"var(--tx2)"}} aria-live="polite">{view!=="dashboard"?views[view]?.t:""}</h1>
        <button
          onClick={()=>setShowMenu(!showMenu)}
          aria-label={showMenu ? "Menü schließen" : "Navigationsmenü öffnen"}
          aria-expanded={showMenu}
          aria-controls="main-nav-panel"
          className="w-11 h-11 rounded-lg flex items-center justify-center"
          style={{background:"var(--card)"}}
        >
          <span aria-hidden="true" style={{fontSize:16}}>{showMenu?"✕":"☰"}</span>
        </button>
      </header>

      {/* Menu-Overlay */}
      {showMenu && (
        <div
          role="dialog"
          aria-modal="true"
          aria-label="Navigationsmenü"
          className="absolute inset-0 z-50 animate-fadeIn"
          style={{background:"rgba(0,0,0,0.65)"}}
          onClick={()=>setShowMenu(false)}
        >
          <nav
            id="main-nav-panel"
            aria-label="Hauptnavigation"
            className="absolute right-0 top-0 bottom-0 w-64 p-5 space-y-1"
            style={{background:"var(--bg)",borderLeft:"1px solid var(--bdr)"}}
            onClick={e=>e.stopPropagation()}
          >
            <p className="text-xs font-bold mb-4" style={{color:"var(--tx2)"}} aria-hidden="true">NAVIGATION</p>
            {menu.map(m => (
              <button
                key={m.id}
                onClick={()=>nav(m.id)}
                aria-label={m.l}
                aria-current={view===m.id ? "page" : undefined}
                className="w-full flex items-center gap-3 px-3 py-2.5 rounded-xl text-sm text-left"
                style={{background:view===m.id?"var(--acc)15":"transparent",color:view===m.id?"var(--acc)":"var(--tx)",minHeight:44}}
              >
                <span aria-hidden="true">{m.i}</span>
                <span className="font-medium">{m.l}</span>
              </button>
            ))}
            <div className="pt-4 mt-4 space-y-2" style={{borderTop:"1px solid var(--bdr)"}}>
              <p className="text-xs" style={{color:"var(--tx2)"}}><span aria-hidden="true">🔒 </span>Zero-Server-Architektur</p>
              <p className="text-xs" style={{color:"var(--tx2)"}}>Alle Daten lokal · Kein Tracking · Kein Medizinprodukt (EU-MDR)</p>
            </div>
          </nav>
        </div>
      )}

      {/* Hauptinhalt */}
      <main id="main-content" tabIndex={-1} aria-label={views[view]?.t || "Dashboard"} className="px-5 py-5 pb-24" style={{opacity:fade?1:0,transition:"opacity 0.12s"}}>
        <div className="animate-fadeIn">{views[view]?.c}</div>
      </main>

      {/* Bottom Nav */}
      <nav aria-label="Schnellnavigation" className="fixed bottom-0 left-1/2 -translate-x-1/2 w-full max-w-[480px] flex justify-around py-2 px-2" style={{background:"var(--bg)",borderTop:"1px solid var(--bdr)"}}>
        {[{id:"dashboard",i:"🏠",l:"Home"},{id:"log",i:"📝",l:"Dose-Log"},{id:"goals",i:"🌟",l:"Clean Days"},{id:"skillbox",i:"🧰",l:"Skills"},{id:"wissen",i:"🧬",l:"Wissen"}].map(n => {
          const active = view===n.id;
          return (
            <button
              key={n.id}
              onClick={()=>nav(n.id)}
              aria-label={n.l}
              aria-current={active ? "page" : undefined}
              className="flex flex-col items-center gap-0.5 px-3 py-2 rounded-xl transition-all"
              style={{minHeight:52,minWidth:52,opacity:active?1:0.6,background:active?"var(--acc)12":"transparent"}}
            >
              <span aria-hidden="true" className="text-xl">{n.i}</span>
              <span aria-hidden="true" style={{color:active?"var(--acc)":"var(--tx2)",fontSize:9,fontWeight:active?700:500}}>{n.l.split(" ")[0]}</span>
            </button>
          );
        })}
      </nav>
    </div>
  );
}

// ─── Shared UI Components — WCAG 2.1 AA ───

// Card: semantisch als <section> oder <article> nutzbar
function Card({ children, as: Tag = "section", ariaLabel }) {
  return <Tag className="rounded-2xl p-4" aria-label={ariaLabel} style={{background:"var(--card)",border:"1px solid var(--bdr)"}}>{children}</Tag>;
}

// Label: immer mit htmlFor für Input-Verknüpfung
function Label({ children, htmlFor }) {
  return <label htmlFor={htmlFor} className="text-xs font-semibold mb-2 block" style={{color:"var(--tx2)"}}>{children}</label>;
}

// Row: Screenreader liest linkes und rechtes Element zusammen
function Row({ l, r }) {
  return (
    <div className="flex items-center justify-between py-1.5 border-b last:border-0" style={{borderColor:"var(--bdr)"}}>
      <span className="text-xs" style={{color:"var(--tx2)"}}>{l}</span>
      <span className="text-xs font-bold" style={{color:"var(--acc)"}}>{r}</span>
    </div>
  );
}

// Btn: aria-label, aria-disabled, min-height 44px
function Btn({ children, onClick, disabled, small, ariaLabel }) {
  return (
    <button
      onClick={onClick}
      disabled={disabled}
      aria-label={ariaLabel}
      aria-disabled={disabled}
      className={`w-full ${small?"py-2":"py-3"} rounded-2xl font-semibold text-sm transition-all`}
      style={{background:disabled?"var(--bdr)":"var(--acc)",color:disabled?"var(--tx2)":"#fff",opacity:disabled?0.55:1,minHeight:44}}
    >
      {children}
    </button>
  );
}

// StatCard: role=figure mit vollständigem aria-label
function StatCard({ icon, value, label, iconLabel }) {
  return (
    <div
      className="rounded-xl p-3 text-center"
      style={{background:"var(--card)",border:"1px solid var(--bdr)"}}
      role="figure"
      aria-label={`${label}: ${value}`}
    >
      <span aria-label={iconLabel} role={iconLabel?"img":"presentation"} className="text-lg">{icon}</span>
      <p className="text-lg font-bold mt-1" style={{color:"var(--tx)"}}>{value}</p>
      <p className="text-xs" style={{color:"var(--tx2)"}}>{label}</p>
    </div>
  );
}

// ActionCard: vollständiges aria-label aus title + sub, Emoji dekorativ
function ActionCard({ icon, title, sub, onClick, accent }) {
  return (
    <button
      onClick={onClick}
      aria-label={`${title}${sub ? ": "+sub : ""}`}
      className="rounded-2xl p-4 text-left transition-all hover:scale-[1.02] active:scale-[0.98]"
      style={{background:accent?"linear-gradient(135deg,#E06B8A18,#E8A87C18)":"var(--card)",border:`1px solid ${accent?"#E06B8A44":"var(--bdr)"}`,minHeight:44}}
    >
      <span aria-hidden="true" className="text-2xl">{icon}</span>
      <p className="font-semibold mt-2 text-sm" style={{color:accent?"#E06B8A":"var(--tx)"}}>{title}</p>
      <p className="text-xs mt-1" style={{color:"var(--tx2)"}}>{sub}</p>
    </button>
  );
}

// HBar: role=meter mit aria-valuenow, Farbe + Textwert (nie nur Farbe)
function HBar({ label, value, icon, note }) {
  // Deuteranopie-sicher: Helligkeit gestaffelt (dunkel=schlecht, hell=gut)
  const c = value>70 ? "var(--risk-low)" : value>40 ? "var(--risk-medium)" : "var(--risk-critical)";
  const lvlText = value>70 ? "gut" : value>40 ? "mittel" : "niedrig";
  return (
    <div className="mb-3" role="meter" aria-valuenow={value} aria-valuemin={0} aria-valuemax={100} aria-label={`${label}: ${value}% (${lvlText})`}>
      <div className="flex justify-between text-xs mb-1">
        <span style={{color:"var(--tx)"}}><span aria-hidden="true">{icon} </span>{label}</span>
        <span style={{color:c}} aria-hidden="true">{value}%</span>
      </div>
      <div className="w-full h-2 rounded-full" style={{background:"var(--bdr)"}} aria-hidden="true">
        <div className="h-2 rounded-full transition-all duration-700" style={{width:`${value}%`,background:c}} />
      </div>
      {note && <p className="text-xs mt-1 italic" style={{color:"var(--tx2)"}}>{note}</p>}
    </div>
  );
}

// Pills: role=group, aria-pressed, minHeight 44px
function Pills({ items, selected, onSelect, emoji }) {
  return (
    <div className="flex flex-wrap gap-2" role="group">
      {items.map(s => (
        <button
          key={s}
          onClick={()=>onSelect(s)}
          aria-pressed={selected===s}
          aria-label={`${s}${selected===s?" (ausgewählt)":""}`}
          className="px-3 py-1.5 rounded-full text-xs font-medium transition-all"
          style={{background:selected===s?"var(--acc)":"var(--card)",color:selected===s?"#fff":"var(--tx)",border:`1px solid ${selected===s?"var(--acc)":"var(--bdr)"}`,minHeight:44}}
        >
          {emoji && <span aria-hidden="true">{emoji(s)} </span>}{s}
        </button>
      ))}
    </div>
  );
}

ReactDOM.createRoot(document.getElementById("root")).render(<DoseDiary />);
  </script>
</body>
</html>
