# Utvärdering av AI-granskningen

Fyll i efter varje PR. En rad per punkt i AI-kommentaren. **Träff** = rätt och värt att åtgärda · **Miss** = fel, eller rätt men oviktigt (brus) · **Oavgjord** = kräver kunskap modellen inte har (domänen, servern, vad som är testdata) – en människa måste avgöra.

Läs diffen själva först och skriv ner vad *ni* hade anmärkt på. Det ni hittade men modellen missade hör hemma i sista kolumnen.

| PR | Punkt (citat ur kommentaren, kort) | Träff / miss / oavgjord | Varför | Det modellen missade |
|---|---|---|---|---|
|A – Visa kundnummer och senaste faktura:  PR#2 34 s | Det ställer till problem med v-html, eftersom användare kan skriva in kod. | | | |
| B – Snabbare fakturalista: PR#3 40s | | | | div i stället för knapp (InvoicesView.vue). “Visa alla” är en div med @click. Den går inte att nå med Tab eller trycka på med Enter, och en skärmläsare säger inte att det är en knapp. KButton är redan importerad men används inte. Hela lodash importeras (import _ from 'lodash'). Bara orderBy och take används, men hela biblioteket följer med i bundlen. Det tog vi bort i Kraftly minns jag. PR:en säger att det ska gå snabbare men lodash gör sidan tyngre att ladda. Så sidan blir kanske snarare långsammare? |
| C – Städa testdata | | | | |

## Summering

| | Antal |
|---|---|
| Punkter totalt | |
| Träff | |
| Miss | |
| Oavgjord | |

## Prompten (steg 5)

Regeln vi ändrade i systemprompten:

Blev den falska positiven i PR C kvar efter ändringen? Vad sa modellen nu?

## Vår regel

När litar vi på kommentaren, och vad gör vi när vi inte håller med?
