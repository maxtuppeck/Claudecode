# Morning News Briefing – Skill Definition
# Datei: CLAUDE.md (oder .claude/skills/morning-news.md in deinem Repository)

---

## Skill: morning-news-briefing

### Zweck
Dieser Skill definiert, wie Claude das tägliche Morgen-Briefing recherchiert, 
bewertet und formatiert. Er verbessert Konsistenz, Qualität und Relevanz 
der täglichen News-Ausgabe.

---

## Quellen-Hierarchie (Vertrauenswürdigkeit)

Bevorzuge Quellen in dieser Reihenfolge:
1. **Tier 1 – Primärquellen**: Reuters, AP News, dpa, ARD, ZDF, BBC News, Der Spiegel, FAZ, SZ
2. **Tier 2 – Qualitätsmedien**: Zeit Online, Handelsblatt, Financial Times, Guardian, NZZ
3. **Tier 3 – Ergänzend**: Tech-spezifisch: The Verge, Ars Technica, Heise Online

**Vermeide**: Social Media als Primärquelle, Boulevardmedien, unverifizierten Content

---

## Relevanz-Filter: Was ist "wichtig"?

Eine Nachricht ist briefing-würdig wenn MINDESTENS eines zutrifft:
- Betrifft mehr als 1 Million Menschen direkt
- Hat Auswirkungen auf Deutschland oder die EU
- Ist ein Wendepunkt in einem laufenden Konflikt/Prozess
- Hat wirtschaftliche Relevanz für europäische Märkte
- Ist ein wissenschaftlicher Durchbruch (peer-reviewed oder Expertenbestätigung)
- War das meistdiskutierte Thema in seriösen Medien

**Nicht ins Briefing**: Celebrity-News, regionale Kriminalfälle ohne überregionale Bedeutung, 
Gerüchte ohne Bestätigung, Clickbait-Themen

---

## Ton & Stil

- **Neutral und sachlich**: Keine Wertung, außer bei wissenschaftlichem Konsens (z.B. Klimawandel)
- **Aktiv formuliert**: "Der Bundestag beschloss..." statt "Es wurde beschlossen..."  
- **Einordnung geben**: Immer erklären, warum eine Meldung wichtig ist
- **Leserniveau**: Gebildeter Laie – Fachbegriffe erklären, aber nicht vereinfachen
- **Zeitform**: Präteritum für Ereignisse, Präsens für anhaltende Situationen

---

## Wirtschaftsdaten – Pflichtformat

Immer diese Daten recherchieren und einfügen:
```
DAX: [Punkte] ([+/-]%) | S&P 500: [Punkte] ([+/-]%) | 
EUR/USD: [Kurs] | Brent Öl: [$/Barrel]
```
Quelle: Immer den Stand vom Vortagesschluss oder aktuellen Vorbörsenwert angeben.

---

## Fehlerbehandlung

Wenn eine Kategorie keine relevante Neuigkeit hat:
→ Schreibe: "*Keine neuen Entwicklungen in dieser Kategorie.*"
→ Kürze die Gesamtlänge entsprechend

Wenn Web Search nicht verfügbar:
→ Erstelle Briefing aus bekanntem Wissensstand
→ Füge deutlichen Hinweis ein: "⚠️ Hinweis: Web Search nicht verfügbar – Daten könnten veraltet sein."

Bei Breaking News (Naturkatastrophe, Anschlag, Regierungscrash):
→ Breaking News immer ZUERST, unabhängig der Kategorie
→ Format: `🚨 BREAKING: [Headline]`

---

## Ausgabe-Checkliste (vor Abschluss prüfen)

- [ ] Datum und Uhrzeit korrekt eingetragen
- [ ] Mindestens 3 Kategorien mit je 1-3 Meldungen befüllt
- [ ] Wirtschaftsdaten vorhanden
- [ ] Eine positive Meldung am Schluss
- [ ] Gesamtlänge unter 700 Wörter
- [ ] Keine unbelegten Behauptungen
- [ ] Alle Schlagzeilen auf Deutsch

---

## Beispiel-Output (Referenz-Qualität)

```markdown
# 🌅 Morgen-Briefing – Dienstag, 5. Mai 2026
*Guten Morgen! Hier sind die wichtigsten Nachrichten des Tages.*

## 🌍 Weltpolitik
- **G7-Gipfel einigt sich auf neue Russland-Sanktionen**: Die G7-Staaten 
  beschlossen ein weiteres Sanktionspaket, das den russischen Energiesektor 
  stärker einschränkt. Deutschland und Frankreich hatten zuvor auf Nachverhandlungen 
  gedrängt – der Kompromiss sieht eine 18-monatige Übergangsfrist vor.

## 💹 Wirtschaft & Märkte  
- **EZB-Protokoll deutet auf Zinspause hin**: Laut gestern veröffentlichtem 
  Sitzungsprotokoll sprachen sich mehrere Ratsmitglieder gegen weitere Senkungen 
  aus. Für die Eurozone könnte dies bedeuten, dass die Leitzinsen bis Herbst stabil bleiben.
- DAX: 23.412 (+0,4%) | S&P 500: 5.891 (-0,1%) | EUR/USD: 1,0823 | Brent: 71,40 $/Barrel

## 🤖 Tech & KI
- **EU-KI-Gesetz tritt in ersten Teilen in Kraft**: Ab heute gelten Transparenzpflichten 
  für KI-Systeme, die mit Bürgern interagieren. Unternehmen müssen kennzeichnen, 
  wenn Nutzer mit einem KI-System kommunizieren.

## 🔬 Wissenschaft & Klima
- **Neue Studie: Arktis-Eis schmilzt schneller als erwartet**: Forscher des Alfred-Wegener-Instituts 
  veröffentlichten Daten, die zeigen, dass das arktische Meereis 30% schneller schwindet 
  als Modelle von 2020 vorhergesagt hatten.

## ✨ Die gute Nachricht
- **Deutschland knackt Rekord bei Solarstrom**: Am gestrigen Montag wurde erstmals 
  mehr als 60% des deutschen Strombedarfs durch Solarenergie gedeckt – ein neuer Rekord.

---
*Briefing automatisch erstellt um 07:03 Uhr. Quellen: Reuters, ARD, Handelsblatt, dpa.*
```

---

## Repository-Integration (CLAUDE.md Platzierung)

Lege diese Datei hier ab:
```
dein-repo/
├── CLAUDE.md              ← Diese Datei (oder)
├── .claude/
│   └── skills/
│       └── morning-news.md  ← Alternative Platzierung
└── README.md
```

## SessionStart Hook (für Cloud Routines)

Füge in deine Routine-Einstellungen unter "Setup Script" ein:
```bash
# Installiert den Skill beim Start jeder Cloud-Session
[ ! -d ~/.claude/skills ] && mkdir -p ~/.claude/skills
cp ./CLAUDE.md ~/.claude/skills/morning-news.md
echo "✓ Morning News Skill geladen"
```
