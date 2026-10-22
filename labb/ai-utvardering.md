# Utvärdering av AI-granskningen

Fyll i efter varje PR. En rad per punkt i AI-kommentaren. **Träff** = rätt och värt att åtgärda · **Miss** = fel, eller rätt men oviktigt (brus) · **Oavgjord** = kräver kunskap modellen inte har (domänen, servern, vad som är testdata) – en människa måste avgöra.

Läs diffen själva först och skriv ner vad *ni* hade anmärkt på. Det ni hittade men modellen missade hör hemma i sista kolumnen.

| PR | Punkt (citat ur kommentaren, kort) | Träff / miss / oavgjord | Varför | Det modellen missade |
|---|---|---|---|---|
| A – #2 · 34 s | "Kundnummer från URL:en styr vilken kunds faktura som hämtas" | träff | IDOR (A01), samma hål som vi lagade i M6. Datan ska väljas ur token, inte ur URL:en | – inget utöver modellens punkter |
| A – #2 | "Användarstyrd sträng läggs okodad i sökvägen" | oavgjord | Stämmer, men om `../` kan nå en annan endpoint beror på servern. Backend-teamet vet. Försvinner också när punkt 1 åtgärdas | |
| A – #2 | "`v-html` med osanerad data från API:t" | träff | Text från API:t renderas som HTML, vilket ger risk för XSS | |
| A – #2 | "URL-värdet visas som 'Kundnummer'" | miss | Samma fel som punkt 1, och modellen säger själv att det löses av punkt 1. Brus | |
| A – #2 | "`route.query.customerNo` kan vara en array" | miss | Sant, men försvinner med punkt 1. Ingen skulle ändra koden bara för det | |
| A – #2 | "Fel sväljs tyst" | träff | Kortet försvinner utan felmeddelande eller loggning vid 403/500. Värt att åtgärda | |
| A – #2 | "Fakturan laddas bara vid mount" | miss | Irrelevant om punkt 1 åtgärdas, vilket modellen själv skriver | |
| B – #3 · 40 s | "'Visa alla'-knappen är en `div` med `@click`" | träff | Går inte att nå med tangentbordet. Bör vara KButton, som redan är importerad. Fokus-tipset är också rimligt | ~~div i stället för knapp, KButton importerad men oanvänd~~ · ~~hela lodash importeras~~ · ~~sidan blir tyngre, inte snabbare~~ – inget utöver modellens punkter |
| B – #3 | "`import _ from 'lodash'` drar in hela lodash" | träff | Hela biblioteket i bundlen för två anrop. Motverkar PR:ens syfte | |
| C – #4 · 21 s | "Inget att anmärka på." | (ingen punkt) | Korrekt, ingen falsk positiv på en ofarlig PR | – |

PR A mergades av misstag efter att kommentaren kommit. Bedömningen gäller kommentaren som den skrevs.

## Summering
| | Antal |
|---|---|
| Punkter totalt | 9 (A: 7, B: 2, C: 0) |
| Träff | 5 |
| Miss | 3 |
| Oavgjord | 1 |

Modellen hittade allt vi själva hade sett i A och B. Det som drog ner precisionen var följdpunkter till A1, alltså samma fel beskrivet flera gånger. Precision uträknad: 5/9 ≈ 56 %.

## Prompten (steg 5)

**Utan ändring (två körningar):** Inget att anmärka på.

**Regeln före:** `- Högst åtta punkter.`
**Regeln efter:** `- Minst fem punkter.`

**Svaret efter ändringen:** "Inget att anmärka på."

**Bedömning:** Ingen falsk positiv, inte ens när prompten krävde minst fem punkter. Troligen följde modellen regeln "Finns inget att anmärka på, svara bara: Inget att anmärka på." före kravet på antal. De två reglerna krockar, och den mer specifika vann. Modellen hittade alltså inte på problem i testdatan, trots att strängarna ser ut som hemligheter.

## Vår regel

När litar vi på kommentaren, och vad gör vi när vi inte håller med?
