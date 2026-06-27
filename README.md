# XAF Raw Export Tool

Een standalone HTML-tool die XAF-auditfiles (XML Auditfile Financieel) inleest en exporteert naar Excel. Geen installatie, geen server — gewoon het HTML-bestand openen in een browser.

## Gebruik

1. Open `xaf_export.html` in een moderne browser (Chrome, Edge, Firefox)
2. Klik op het dropgebied en selecteer een `.xaf` of `.xml` bestand
3. Wacht tot de voortgangsbalk klaar is
4. Klik **Download Excel**

## Output (tabbladen)

| Tabblad | Inhoud |
|---|---|
| Bedrijfsgegevens | Naam, KvK, BTW, boekjaar, software, XAF-versie |
| Grootboekrekeningen | accID, omschrijving, type, RGScode (4.0) / leadCode (3.2) |
| BTW-codes | vatID, omschrijving, rekeningen |
| Beginsaldi | Openingssaldi per grootboekrekening |
| Deb_Cred | Debiteur/crediteur stamgegevens (indien aanwezig) |
| Mutaties | Alle journaalregels met dagboek, transactie en BTW-info |

Bij meer dan 1.000.000 mutatieregels wordt het Mutaties-tabblad automatisch gesplitst.

## Grote bestanden

De tool is geoptimaliseerd voor bestanden van 700 MB en groter:

- Verwerking draait in een **Web Worker** (UI blijft responsief)
- XML wordt **per dagboek** geparsed — nooit het volledige bestand als één DOM
- Voortgangsbalk toont dagboeken verwerkt en aantal mutatieregels

## XAF-versies

Ondersteunt zowel **XAF 3.2** als **XAF 4.0** (verplicht vanaf 1 januari 2026). De gedetecteerde versie wordt getoond in het Bedrijfsgegevens-tabblad.

## Technisch

- Puur client-side: geen data wordt verstuurd naar een server
- Afhankelijkheid: [SheetJS (xlsx)](https://sheetjs.com/) via CDN
- Compatibel met Chrome, Edge en Firefox (niet IE)
