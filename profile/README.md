# Vitalij Ljubačivskyj – projekty

Přehled mých projektů: co je hotové, co ve vývoji a co rozpracované. Většinu jsem vyvíjel **ve spolupráci s AI
(Claude)** – u větších projektů jako vedoucí produktu dvou koordinovaných AI agentů, kteří spolu komunikují přes git.
Zdrojový kód soukromých projektů rád zpřístupním na požádání.

*Aktualizováno: 16. 11. 2026*

## Přehled

| Projekt | O čem | Technologie | Stav | Odkaz |
|---|---|---|---|---|
| **WristRadar Watch** | skupinový lokátor na hodinkách: šipka a vzdálenost k přátelům | Swift/SwiftUI, Kotlin/Compose, Firebase | ✅ **vydáno** v App Store (26. 10. 2026); Wear OS v uzavřeném testu na Google Play | [ukázka](https://github.com/Fredy1989/wristradar-showcase) |
| **WristRadar Phone** | telefonní verze WristRadaru, společné skupiny s hodinkami | Swift, Kotlin (sdílené jádro s hodinkami) | 🛠️ **vývoj** – testovací verze iPhone i Android hotové, smíšená skupina telefon ↔ hodinky ověřena na reálných zařízeních | [ukázka](https://github.com/Fredy1989/wristradar-showcase) |
| **Driver Alert** | trenér bdělosti řidiče: riziko únavy ze spánku a času jízdy, hlasové kontroly, vibrace na hodinkách | Swift, Kotlin, Apple Zdraví / Health Connect | 🛠️ **vývoj** od 15. 11. 2026 – jádro (model rizika a detekce jízdy na iOS i Androidu), první verze appky pro iPhone a pro Android (sledování jízdy z GPS, ověřeno na emulátoru) | [níže](#driver-alert) |
| **CarKeeper** *(pracovní název)* | péče o auto: hlídá STK, servis a přezutí, nabídky servisů v okolí s odhadem ceny a rezervací; AI hlasový agent domluví termín za řidiče | mobilní appka + cloud, hlasová AI (výběr dodavatele probíhá) | 📋 **analýza** hotová (15. 11. 2026) | [níže](#carkeeper) |
| **Sportka** | stahování výsledků loterie, statistická analýza, generátor tiketů a backtest | Python | ✅ **v provozu** od 3. 6. 2026, denní automatický běh | [repo](https://github.com/vitalij-projekty/sportka) |
| **Trading bot** | boty nad MetaTrader 5 pro prop-firmu FTMO, dashboard, série backtestů | Python, MT5, pandas | ⏸️ **pozastaveno** – výzkum uzavřen (17 hypotéz, ~290 konfigurací, bez ověřitelné hrany) | [repo](https://github.com/vitalij-projekty/trading-bot) |
| **ScamCatcher** *(pracovní název)* | ochrana před telefonními podvody: přepis příchozích i odchozích hovorů v reálném čase, AI průběžně hodnotí riziko podvodu a pozná i volajícího AI agenta nebo napodobený hlas | mobilní appka, přepis řeči, LLM (výběr technologie proběhne v analýze) | 💡 **nápad** – ve zpracování, příprava analýzy (od 15. 11. 2026) | [níže](#scamcatcher) |
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
  první verze appky pro iPhone (simulátor) 15. 11. 2026 · Android: služba za jízdy s GPS, rozpoznáním jízdy
  a ukládáním jízd, ověřeno na emulátoru Androidu 16, 15. 11. 2026 · MVP plánováno na leden 2027.
- **Zajímavé:** stejná pravidla na dvou platformách hlídají sdílené testovací vektory (JSON), které musí projít iOS
  i Android; důraz na právo (žádná zdravotní tvrzení, GDPR – údaje o zdraví jen v zařízení) a bezpečnost za jízdy.

## CarKeeper
Aplikace hlídá termíny auta (STK, servis, přezutí, pojištění), z historie a kilometrů vyhodnotí, co je potřeba,
a nabídne servisy v okolí s termínem a odhadem ceny. Servisům bez online rezervace zavolá AI hlasový agent a termín
domluví za řidiče; přepis a shrnutí hovorů i faktury tvoří kompletní historii auta.
- **Milníky:** analýza chytrého parkování 14.–15. 11. 2026 → změna směru · analýza CarKeeper 15. 11. 2026.
- **Zajímavé:** analýza parkování ukázala obsazený trh plateb a fyzické bariéry (závory, turnikety, přístupové
  karty) → záměrný přechod na produkt bez hardwaru; data o STK podle VIN stát volně neposkytuje, proto zadání auta
  fotkou technického průkazu a faktur.

## ScamCatcher
Aplikace poslouchá hovor (s výslovným souhlasem uživatele), přepisuje ho a AI bot průběžně hledá znaky podvodu:
„bezpečný účet“, časový tlak, žádost o PIN nebo kód z SMS, instalaci aplikace pro vzdálený přístup, vydávání se
za banku, policii nebo příbuzného. Druhým cílem je poznat, že volá jiný AI agent nebo napodobený hlas blízké osoby.
Při podezření nenápadně upozorní uživatele, navrhne kontrolní otázku a volitelně dá vědět rodině.
- **Milníky:** nápad 15. 11. 2026 · analýza v přípravě.
- **Hlavní otázky pro analýzu:** přístup ke zvuku hovoru (iOS ho běžným aplikacím nedává, Android nahrávání hovorů
  omezuje), souhlas s nahráváním a GDPR, zpracování přímo v telefonu kvůli soukromí.

## Jak pracuji s AI
- Já: produkt, rozhodnutí, testování na reálných zařízeních, komunikace s obchody (App Store, Google Play).
- Dva AI agenti (Claude na Macu pro Apple, Claude na Windows pro Android) pracují paralelně a koordinují se přes
  sdílený git repozitář: deník rozhodnutí, schránka úkolů, specifikace a testovací vektory jako společný zdroj pravdy.
