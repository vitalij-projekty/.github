# Vitalij Ljubačivskyj – projekty

Přehled mých projektů: co je hotové, co ve vývoji a co rozpracované. Většinu jsem vyvíjel **ve spolupráci s AI
(Claude)** – u větších projektů jako vedoucí produktu dvou koordinovaných AI agentů, kteří spolu komunikují přes git.
Zdrojový kód soukromých projektů rád zpřístupním na požádání.

*Aktualizováno: 19. 11. 2026*

## Přehled

| Projekt | O čem | Technologie | Stav | Odkaz |
|---|---|---|---|---|
| **WristRadar Watch** | skupinový lokátor na hodinkách: šipka a vzdálenost k přátelům | Swift/SwiftUI, Kotlin/Compose, Firebase | ✅ **vydáno** v App Store (26. 10. 2026); Wear OS v uzavřeném testu na Google Play | [ukázka](https://github.com/Fredy1989/wristradar-showcase) |
| **WristRadar Phone** | telefonní verze WristRadaru, společné skupiny s hodinkami | Swift, Kotlin (sdílené jádro s hodinkami) | 🛠️ **vývoj** – testovací verze iPhone i Android hotové, smíšená skupina telefon ↔ hodinky ověřena na reálných zařízeních | [ukázka](https://github.com/Fredy1989/wristradar-showcase) |
| **Driver Alert** | trenér bdělosti řidiče: riziko únavy ze spánku a času jízdy, hlasové kontroly, vibrace na hodinkách | Swift, Kotlin, Apple Zdraví / Health Connect | 🛠️ **vývoj** od 15. 11. 2026 – jádro (model rizika a detekce jízdy na iOS i Androidu), první verze appky pro iPhone a pro Android (sledování jízdy z GPS, ověřeno na emulátoru) | [níže](#driver-alert) |
| **CarKeeper** *(pracovní název)* | péče o auto: hlídá STK, servis a přezutí, nabídky servisů v okolí s odhadem ceny a rezervací; AI hlasový agent domluví termín za řidiče | mobilní appka + cloud, hlasová AI (výběr dodavatele probíhá) | 📋 **analýza** hotová (15. 11. 2026) | [níže](#carkeeper) |
| **Sportka** | stahování výsledků loterie, statistická analýza, generátor tiketů a backtest | Python | ✅ **v provozu** od 3. 6. 2026, denní automatický běh | [níže](#sportka) |
| **Trading bot** | boty nad MetaTrader 5 pro prop-firmu FTMO, dashboard, série backtestů | Python, MT5, pandas | ⏸️ **pozastaveno** – výzkum uzavřen (17 hypotéz, ~290 konfigurací, bez ověřitelné hrany) | [níže](#trading-bot) |
| **ScamCatcher** | ochrana seniorů před telefonními podvody: neznámý hovor přijme AI asistent, přepíše ho a ohodnotí riziko podvodu 0–100; podezřelé hovory rozhoduje člen rodiny (správce) | Python (FastAPI, Claude API), Firebase, Kotlin/Compose, Swift/SwiftUI, přepis řeči, telefonie | 🛠️ **vývoj** – ve vývoji od 16. 11. 2026; server na Firebase, appky iOS a Android, Android v interním testu Google Play | [níže](#scamcatcher) |
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
Neznámý hovor seniora převezme AI asistent (přes přesměrování u operátora), zeptá se, kdo volá a proč, rozhovor
přepíše a jazykový model ohodnotí riziko podvodu 0–100 s důvody („bezpečný účet“, kód z SMS, vzdálený přístup,
vydávání se za banku či příbuzného). Hovory od nastaveného prahu dostane člen rodiny (správce) a rozhodne:
bezpečné / podvod / ověřím. Zvuk zpracovává server, ne telefon, takže služba funguje stejně na iOS i Androidu.
- **Milníky:** nápad 15. 11. 2026 · název rezervován v App Store (16. 11.) i Google Play (17. 11.) · ve vývoji od
  16. 11. 2026 · server a iOS napojené na Firebase, ověřeno end-to-end včetně push (18. 11.) · appka Android
  v interním testu Google Play a ověřená na telefonu (18. 11.) · bezpečnostní revize z pohledu útočníka (18. 11.).
- **Zajímavé výzvy:** ochrana hodnocení proti prompt injection od volajícího, převzetí rodiny přes pozvánku
  (schvalování nových správců), soukromí a souhlas seniora (GDPR, AI Act).

## Sportka
Osobní nástroj v Pythonu: sám stahuje výsledky loterie Sportka, vede jejich archiv, statisticky je analyzuje
(četnosti, dvojice, součty, poměry lichých/sudých), generuje sloupce na tiket a každý vygenerovaný sloupec zpětně
vyhodnocuje proti skutečným tažením (backtest).
- **Milníky:** v provozu od 3. 6. 2026 · denní automatický běh přes Plánovač úloh (stažení, generování, backtest,
  commit a push změněných dat) · k 13. 11. 2026 archiv 436 tažení a 506 vygenerovaných sloupců.
- **Zajímavé:** backtest poctivě ukázal, že frekvenční strategie nepřekonává náhodu (úspěšnost sloupce 1,4 %
  proti teoretickým 1,86 % v rámci šumu) → přechod na „nepopulární kombinace“, které šanci nemění, ale při výhře
  zvyšují výplatu, protože se dělí s méně lidmi.

## Trading bot
Automatizovaný a poloautomatický forex trading v Pythonu nad MetaTrader 5 pro prop-firmu FTMO: autonomní bot,
execution tool se „stínovými pozicemi“, risk management podle pravidel FTMO, lokální webový dashboard, ovládání
přes Telegram, watchdog na VPS a notifikace na Discord.
- **Milníky:** autonomní bot nasazen na VPS 13. 7. 2026 · série backtestů 20.–24. 7. 2026 · ostré obchody na FTMO
  účtu 28.–31. 7. 2026 · výzkum uzavřen, bot od 31. 7. 2026 neobchoduje.
- **Zajímavé:** 17 hypotéz, ~290 konfigurací, až 26 let dat, vždy s rozdělením in-sample / out-of-sample a cenou
  po spreadu a komisi. validací neprošel žádný z 29 out-of-sample segmentů; kontrolní test s uměle vloženou hranou prošel,
  takže metodika efekty umí najít – závěr „žádná ověřitelná hrana“ je výsledek, ne slepota testu.

## Jak pracuji s AI
- Já: produkt, rozhodnutí, testování na reálných zařízeních, komunikace s obchody (App Store, Google Play).
- Dva AI agenti (Claude na Macu pro Apple, Claude na Windows pro Android) pracují paralelně a koordinují se přes
  sdílený git repozitář: deník rozhodnutí, schránka úkolů, specifikace a testovací vektory jako společný zdroj pravdy.
