# Meetplan (samenvatting) – nieuwe website

Bron van waarheid: Docmost-wiki (Web Analytics Measurement Plan). Dit is een samenvatting voor agents;
bij twijfel geldt Docmost. TODO: link naar de Docmost-pagina.

## Stack
Next.js (frontend), NestJS (backend), Prepr (CMS), Salesforce (CRM), Converse (betalingen: iDEAL, Wero, SEPA),
Clearcookie (CMP), GTM web + server-side (Stape), GA4, Looker Studio + Supermetrics. Nieuwe website live 11 januari 2027.

## Conversies
- Primair: sponsoring (vast maandbedrag), eenmalige en periodieke giften aan fondsen/projecten.
- Secundair: partnercontactformulier. NL en BE in één valuta.

## Vastgelegde besluiten (niet heropenen zonder gate)
- Purchase vuurt server-side via payment-webhook (iDEAL/Wero sturen bezoekers off-site).
- client_id en session_id worden bij begin_checkout vastgelegd en op het donatierecord bewaard.
- Eenmalige omzet (€) en terugkerende waarde (€/maand) worden nooit opgeteld.
- begin_checkout is geen key event; key-eventstatus staat in de eventcatalogus.
- Standaard GA4 e-commerceparameters eerst, pas daarna custom item-scoped dimensies.
- iDEAL-mandaatbetaling van €0,01 telt niet als omzet; de toegezegde maandwaarde wel.
- Item-ID's = Salesforce destination-ID's.
- CPA/ROAS zijn KPI's in de rapportagelaag.
- GA4 data-driven attributie voor giften; Salesforce (scode) is eigenaar van attributie van sponsorwerving.
- Conversieratio's zijn sessie-gebaseerd.

## Campagnelinks en attributie
- UTM's via Campagnelinks (vervanger van de UTM-Excel). `utm_campaign` is niet per se een Salesforce-campagne.
- `scode` is optioneel en dient voor sponsorattributie in Salesforce.
- Campagnelinks (campagnelinks.vercel.app, inloggen met teamcode) is de bron van waarheid voor links, korte links (cmpsn.nl), QR-codes en de vaste lijsten hieronder. Maak links alleen daar. Agents nemen waarden uit de tool over en verzinnen geen nieuwe; een nieuwe waarde vraag je aan bij de beheerder.

### Naamconventie (Campagnelinks, gelezen 2026-11-25)
Alle waarden in kleine letters, woorden gescheiden door `-`, geen spaties.
| Parameter | Regel | Voorbeeld |
|---|---|---|
| `utm_campaign` | `<categoriecode>-<campagnenaam>`. De campagne wordt één keer aangemaakt in Campagnelinks (met optionele scode) en daarna overal gekozen. | `mar-cdsp-een-betere-toekomst`, `krk-mz-261101-mozaiek-online`, `xmas-fw-xmas-fy27` |
| `utm_medium` | Vaste lijst van tien: `email`, `social`, `paid-social`, `display`, `video`, `referral`, `paid-referral`, `offline`, `affiliate`, `cpc` | `paid-social` |
| `utm_source` | Vaste lijst (113 waarden): platform, titel, partner, kerk of event. Details zoals editie, artiest of vestiging gaan in `utm_content`. | `facebook`, `instagram`, `nieuwsbrief-sc`, `nd`, `flyer` |
| `utm_content` | Optioneel: variant of plaatsing | `post-1`, `story`, `qr-code`, `header-banner` |
| `utm_term` | Optioneel: zoekwoord | |
| `scode` | Optioneel, hoort bij de campagne; voor sponsorattributie in Salesforce | `NLSC21751` |

**Categoriecodes** (komen vooraan in `utm_campaign`; een code wordt niet gewijzigd, alleen inactief gezet):
| Code | Categorie |
|---|---|
| MAR | Marketing |
| KRK | Kerken |
| SCH | Scholen |
| ZAK | Zakelijk |
| NAL | Nalatenschappen |
| AE | Events & Artiesten |
| CORP | Corporate |
| MBM | Moeder & Babymaand |
| XMAS | Kerst |
| SOC | Social |
| CTSE | Cross-team Supporter Experience |
| MUSK | Muskathlon |

### Afkortingen in campagnenamen van advertentieplatforms (bevestigd 2026-11-25)
Google Ads (auto-tagging) en Meta (dynamische parameters) gebruiken de campagnenaam uit het platform, niet uit Campagnelinks. Daar komen deze afkortingen voor, in de vorm `AFK [FY] | onderdeel | onderdeel`. FY = boekjaar juli–juni (FY27 = jul 2026–jun 2027).
| Afkorting | Betekenis |
|---|---|
| CDSP | Child Development Sponsorship Program (werving kindsponsoring); in Campagnelinks onder MAR |
| INFL | Influencers; in Campagnelinks onder MAR |
| BA | Brand Awareness |
| MA | Marketing Automation (journeys in Marketing Cloud) |
| TM | Tomorrowmen, digital marketing agency; Google Ads-campagnes die zij bouwen |
| AO | Always On |
| BEA | Boek een Artiest (oude campagne, niet meer gebruiken) |

- Meta-campagnes van CDSP gebruiken funnelfases op de tweede plek: Attention, Empathy, Trust, Belief.
- Oude Google Ads-namen zonder prefix (zoals `Search | Branding | NL`, `Performance Max | Algemeen | NL`) worden uitgefaseerd ten gunste van `TM | …`.

## Advertentieplatforms
Google Ads (los van Google Grants), Meta, Microsoft Ads, TikTok, Pinterest; LinkedIn actief.
Meta, LinkedIn en Pinterest: pixel + server-side CAPI met event_id-deduplicatie. Microsoft en TikTok: alleen browser.

## Open punten (agents mogen signaleren, niet oplossen in productie)
- Web-container mist server_container_url.
- Cookiebot-restanten naast Clearcookie.
- Herontwerp purchase-webhook (NestJS of Salesforce/Converse) wacht op afstemming.
- Fouten in de dataLayer-documentatie van fase 3.
- Key events rationaliseren (dwell_time, session_duration_5, visited_3_pages, waarschijnlijk file_download degraderen).
- Google Ads betaald scheiden van Google Grants.

### UTM-afwijkingen in GA4 (compassion.nl, 90 dagen tot 2026-11-24, sessies)
- Spaties in waarden (`paid social`) splitsen campagnes in gecodeerde varianten (`CDSP+FY26+|+...`).
- Schrijfwijze van medium door elkaar: `paid social`, `PaidSocial`, `paid-social`; `cpc` en `Cpc`. Ook hoofdletters in campagnenamen (`Sponsormail Oktober` naast `oktober`).
- E-mail uit Marketing Cloud: de mailingnaam staat in `utm_source` in plaats van een bron uit de Campagnelinks-lijst (bijv. `nieuwsbrief-sc`); slechts 41 sessies met source `sfmc`.
- Offline: eventnaam staat in `utm_source`. Medium `offline` valt in GA4 standaard onder Unassigned; eigen kanaalgroep nodig.
- Pinterest: campagne-ID (bijv. `626757580169`) in plaats van naam.
- Meta-macro `{{site_source_name}}` niet ingevuld in een advertentie (16 sessies).
- Enkele e-mail- en Muskathlon-campagnenamen zijn onleesbaar (letters door elkaar).
- 2.355 sessies met source en medium `(not set)`.
- Campagnenamen uit Google Ads en Meta (`TM | …`, `CDSP FY26 | …`) volgen een andere opzet dan Campagnelinks (`mar-cdsp-…`). Daardoor sluiten rapportages per campagne niet op elkaar aan. Besluit nodig: platformnamen gelijktrekken of mappen in de rapportagelaag.- Self-referrals en intern verkeer nemen krediet over: `compassion-nl.my.salesforce-sites.com` (1.191 sessies), `compassion-nl-staging.vercel.app`, `compassion-nl.lightning.force.com`, `compassionnl.sharepoint.com`, Teams, Marketing Cloud-contentdomein. Kandidaten voor ongewenste verwijzingen of intern-verkeerfilter.
