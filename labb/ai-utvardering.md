# Utvärdering av AI-granskningen

Fyll i efter varje PR. En rad per punkt i AI-kommentaren. **Träff** = rätt och värt att åtgärda · **Miss** = fel, eller rätt men oviktigt (brus) · **Oavgjord** = kräver kunskap modellen inte har (domänen, servern, vad som är testdata) – en människa måste avgöra.

Läs diffen själva först och skriv ner vad *ni* hade anmärkt på. Det ni hittade men modellen missade hör hemma i sista kolumnen.

| PR | Punkt (citat ur kommentaren, kort) | Träff / miss / oavgjord | Varför | Det modellen missade |
|---|---|---|---|---|
|A – Visa kundnummer och senaste faktura:  PR#2 34 s | Det ställer till problem med v-html, eftersom användare kan skriva in kod. | | | |
| B – Snabbare fakturalista | | | | |
| C – Städa testdata | | | | |

## Summering

| | Antal |
|---|---|
| Punkter totalt | |
| Träff | |
| Miss | |
| Oavgjord | |

## Prompten (steg 5)

**Utan ändring (två körningar):** Inget att anmärka på.

**Regeln före:** `- Högst åtta punkter.`
**Regeln efter:** `- Minst fem punkter.`

**Svaret efter ändringen:** "Inget att anmärka på."

**Bedömning:** Ingen falsk positiv, inte ens när prompten krävde minst fem punkter. Troligen följde modellen regeln "Finns inget att anmärka på, svara bara: Inget att anmärka på." före kravet på antal. De två reglerna krockar, och den mer specifika vann. Modellen hittade alltså inte på problem i testdatan, trots att strängarna ser ut som hemligheter.

## Vår regel

När litar vi på kommentaren, och vad gör vi när vi inte håller med?
