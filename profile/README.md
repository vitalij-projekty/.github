# Vitalij Ljubačivskyj – projekty

Přehled mých projektů: co je hotové, co ve vývoji a co rozpracované. Většinu jsem vyvíjel **ve spolupráci s AI
(Claude)** – u větších projektů jako vedoucí produktu dvou koordinovaných AI agentů, kteří spolu komunikují přes git.
Zdrojový kód soukromých projektů rád zpřístupním na požádání.

*Aktualizováno: 15. 11. 2026*

## Přehled

| Projekt | O čem | Technologie | Stav | Odkaz |
|---|---|---|---|---|
| **WristRadar Watch** | skupinový lokátor na hodinkách: šipka a vzdálenost k přátelům | Swift/SwiftUI, Kotlin/Compose, Firebase | ✅ **vydáno** v App Store (26. 10. 2026); Wear OS v uzavřeném testu na Google Play | [ukázka](https://github.com/Fredy1989/wristradar-showcase) |
| **WristRadar Phone** | telefonní verze WristRadaru, společné skupiny s hodinkami | Swift, Kotlin (sdílené jádro s hodinkami) | 🛠️ **vývoj** – testovací verze iPhone i Android hotové, smíšená skupina telefon ↔ hodinky ověřena na reálných zařízeních | [ukázka](https://github.com/Fredy1989/wristradar-showcase) |
| **Driver Alert** | trenér bdělosti řidiče: riziko únavy ze spánku a času jízdy, hlasové kontroly, vibrace na hodinkách | Swift, Kotlin, Apple Zdraví / Health Connect | 🛠️ **vývoj** od 15. 11. 2026 – jádro (model rizika na iOS i Androidu, detekce jízdy) a první verze appky pro iPhone | [níže](#driver-alert) |
| **Smart Parking** | hlasový parkovací asistent pro Prahu: zóna, cena, max. doba, připomenutí na hodinkách | Swift, Kotlin, otevřená data Golemio | 📋 **analýza a specifikace** hotové | [níže](#smart-parking) |
| **Sportka** | stahování výsledků loterie, statistická analýza, generátor tiketů a backtest | Python | ✅ **v provozu** od 3. 6. 2026, denní automatický běh | [repo](https://github.com/vitalij-projekty/sportka) |
| **Trading bot** | boty nad MetaTrader 5 pro prop-firmu FTMO, dashboard, série backtestů | Python, MT5, pandas | ⏸️ **pozastaveno** – výzkum uzavřen (17 hypotéz, ~290 konfigurací, bez ověřitelné hrany) | [repo](https://github.com/vitalij-projekty/trading-bot) |
| **Databáze investorů** | úloha k pohovoru: návrh spolehlivé databáze investorů, pilot 43 investorů v ČR, měření přesnosti | AI rešerše, Excel/CSV | ✅ **hotovo** (10/2026) | [repo](https://github.com/Fredy1989/investor-db) |

## WristRadar
Jedna aplikace pro Apple Watch i Wear OS se společným real-time backendem, od nápadu po vydání v App Store zhruba
za 5 týdnů. Zajímavé výzvy: watchOS na reálných hodinkách blokuje WebSocket, takže verze pro Apple Watch mluví
s Firebase přes REST a Server-Sent Events; bezpečnost bez vlastního serveru (pravidla databáze ověřená testy);
GDPR; 6 jazyků. Podrobnosti, snímky a architektura: [wristradar-showcase](https://github.com/Fredy1989/wristradar-showcase).

## Driver Alert
Asistent proti únavě za volantem pro jakékoli auto. Místo nespolehlivého „detektoru mikrospánku“ (hodinky dnes
nemají dostatečnou přesnost) jde o transparentní model rizika ze spánku, doby bdění, denní doby a času za volantem,
doplněný hlasovými kontrolními otázkami s měřením reakce a vibracemi na hodinkách.
- **Milníky:** analýza trhu a technologií 14. 11. 2026 · specifikace schválena 15. 11. 2026 · jádro (model rizika)
  hotové a otestované 15. 11. 2026 · nezávislé specifikace obou AI agentů porovnány a sloučeny 15. 11. 2026 ·
  první verze appky pro iPhone (simulátor) 15. 11. 2026 · MVP plánováno na leden 2027.
- **Zajímavé:** stejná pravidla na dvou platformách hlídají sdílené testovací vektory (JSON), které musí projít iOS
  i Android; důraz na právo (žádná zdravotní tvrzení, GDPR – údaje o zdraví jen v zařízení) a bezpečnost za jízdy.

## Smart Parking
Po zaparkování v Praze appka sama pozná zónu placeného stání, řekne cenu a maximální dobu, zapamatuje si polohu
auta a před koncem zaplaceného času upozorní na telefonu i hodinkách. Placení předává do existujících appek.
- **Milníky:** analýza 14. 11. 2026 · specifikace a testovací vektory 15. 11. 2026 · vývoj po Driver Alertu.
- **Zajímavé:** analýza ukázala, že placení vlastní appkou vyžaduje smlouvu s městem → záměrně menší, ale
  realizovatelný produkt; data zón z otevřených dat Golemio přes vlastní noční převod (API klíč nesmí být v appce).

## Jak pracuji s AI
- Já: produkt, rozhodnutí, testování na reálných zařízeních, komunikace s obchody (App Store, Google Play).
- Dva AI agenti (Claude na Macu pro Apple, Claude na Windows pro Android) pracují paralelně a koordinují se přes
  sdílený git repozitář: deník rozhodnutí, schránka úkolů, specifikace a testovací vektory jako společný zdroj pravdy.
