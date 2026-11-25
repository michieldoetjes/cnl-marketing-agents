# CNL Marketing Agents – werkregels

Dit project helpt het marketingteam van Compassion Nederland met campagnes, metingen en content.
Missie: kinderen bevrijden uit armoede in Jezus' naam. Jezus staat centraal in ons werk.
Bescherm kwetsbare kinderen, respecteer ieders waardigheid en handel integer.

Werktaal: Nederlands. Bestandsnamen, code en technische identifiers: Engels.

## Lees eerst
1. `.agents/product-marketing.md` – wie we zijn, segmenten, doelen, learnings (alle marketing-skills lezen dit).
2. `context/saas-glossary.md` – de skills zijn geschreven voor SaaS; vertaal hun begrippen naar onze situatie.
3. `context/brand-and-tone.md` – merk, toon, beeld en waardigheid.
4. `context/measurement.md` – meetplan, key events, UTM- en scode-afspraken.
5. Bij campagnewerk: `campaigns/<campagne>/brief.md` en `decisions.md`.

## Dataregels (gaan altijd voor)
- Gebruik NOOIT identificeerbare gegevens van kinderen/begunstigden of van sponsors, donateurs en supporters.
  Alleen geanonimiseerde, synthetische of testdata, en informatie die Compassion zelf openbaar heeft gemaakt.
- Geen gevoelige HR-, salaris- of medische gegevens van medewerkers.
- Lees geen `.env`-bestanden, wachtwoorden, API-keys of tokens.
- Stuur geen Compassion-code of -data naar externe diensten of AI-tools zonder expliciete goedkeuring
  (AI-register). De integraties uit de oorspronkelijke repo (`tools/`) zitten bewust niet in dit project.
- Kom je verboden data tegen: stop, gebruik het niet, meld het en stel geanonimiseerde data voor.
- Salesforce, Marketing Cloud, FinDock, GA4, GTM: configuratie, schema's en geaggregeerde cijfers mogen;
  geen productierecords met persoonsgegevens inzien.

## Wat agents wel en niet doen
- Agents maken **concepten** en **adviezen**. Ze publiceren niets, verschuiven geen budget, wijzigen geen
  tracking of productie-instellingen. Dat doet een mens na expliciet akkoord.
- Ontbrekende data wordt gemarkeerd als `MISSING`, nooit geschat of verzonnen.
- Claims (aantallen kinderen, impact, effect van sponsoring) alleen met bron. Geen bron: weglaten of als vraag markeren.

## Werkwijze: phase-gate
Brief → Strategie → Productie → QA → Live → Leren.
- Per gate een besluit (go / no-go / terug) in `campaigns/<campagne>/decisions.md`. Vastgelegde besluiten
  worden niet stilzwijgend heropend; wie iets wil wijzigen, stelt het voor in de volgende gate.
- Sub-agents stemmen af via bestanden: ze lezen `brief.md` en `decisions.md` en schrijven hun output naar
  `handoffs/<fase>-<agent>.md`. De PM (hoofdsessie) bundelt, signaleert tegenstrijdigheden en legt voor.
- Elke output gaat langs de `reviewer` voordat de gate dicht gaat.

## Wetgeving en normen (Nederland/België)
De skills noemen Amerikaanse regels (CAN-SPAM, FTC, TCPA). Toets hier aan: AVG/GDPR,
Telecommunicatiewet (toestemming voor e-mail/sms), Nederlandse Reclame Code, CBF-Erkenningsregeling
en Compassions eigen beleid voor kinderbescherming en beeldgebruik.

## Stijl van werken
- Standaardmodellen eerst (bijv. standaard GA4 e-commerce) vóór maatwerk; voorkom over-engineering.
- Liever aanvullen dan herstructureren bij bestaande deliverables.
- Eén centrale bron van waarheid per onderwerp; dubbele informatie verwijzen, niet kopiëren.
- Digitaal versterkt, maar vervangt geen offline kanalen en relaties.
