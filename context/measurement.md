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
- TODO: naamconventie utm_source / utm_medium / utm_campaign invullen.

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
