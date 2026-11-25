# cnl-marketing-agents

Claude Code-project voor het marketingteam van Compassion Nederland: een PM-rol die acht gespecialiseerde
sub-agents aanstuurt, met marketing-skills aangepast aan onze context. Pilot: campagne *Groter dan…*.

## Inhoud
| Pad | Wat |
|---|---|
| `CLAUDE.md` | Werkregels, dataregels, phase-gate. Wordt elke sessie automatisch gelezen. |
| `.agents/product-marketing.md` | Compassion-context die alle marketing-skills eerst lezen (TODO's invullen). |
| `context/` | Vertaling SaaS → Compassion, merk en waardigheid, meetplan. |
| `.claude/skills/` | 33 geselecteerde skills uit coreyhaines31/marketingskills (MIT) + `cnl-review`. |
| `.claude/agents/` | strategist, paid-media, content-social, email, web-cro, measurement, seo-geo, reviewer. |
| `.claude/commands/` | `/pm <campagne> <fase>` en `/new-campaign <slug>`. |
| `campaigns/` | Sjabloon en de pilot `groter-dan/`. |

## Starten
1. Open deze map in de Code-tab van de Claude desktop-app.
2. Kopieer je ContentSkippy-skill naar `.claude/skills/contentskippy/` (map met `SKILL.md`).
3. Vraag: "Lees CLAUDE.md en vat de werkregels samen." – controle dat de basis werkt.
4. Vul `.agents/product-marketing.md` aan: "Gebruik de skill product-marketing om de TODO's met mij in te vullen."
5. Start de pilot: `/pm groter-dan brief`.

## Bewust weggelaten
- `tools/` en de scripts in de hoofdmap van de oorspronkelijke repo (externe integraties zoals Composio en AIsa).
- Skills voor SaaS/B2B (aso, paywalls, pricing, prospecting, cold-email, directory-submissions, revops,
  sales-enablement, launch, programmatic-seo, onboarding, competitors e.a.). Later toe te voegen indien nodig.
- Map `evals/` per skill.

## Let op bij scripts in skills
- `conversion-tracking/scripts/` voegt lokaal GTM-recepten samen; draait alleen op je eigen machine.
- `reverse-engineer-marketing/scripts/teardown.mjs` raadpleegt openbare bronnen (Wayback, ad-bibliotheken)
  over een ándere organisatie. Gebruik het niet met Compassion-data en vul geen API-keys in zonder AI-register.
- Bash staat in `.claude/settings.json` op "vragen", zodat je elk script eerst ziet.

Bron skills: https://github.com/coreyhaines31/marketingskills (MIT-licentie, zie `.claude/skills/LICENSE-marketingskills`).
