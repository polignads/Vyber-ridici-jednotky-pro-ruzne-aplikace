[Co dodělat ]: #
[pojmy ]: #

# Výběr řídící jednotky pro různé aplikace

$${\color{#FFA500}E9 \space \color{#4682B4}A1 }$$

## Cíle

- **Kategorizovat a porovnat** architektury řídicích systémů (MCU, MPU, embedded systémy, PLC, iPC, programovatelná relé) podle výkonu, paměti, determinismu a spolehlivosti.
- **Analyzovat provozní prostředí a vnější vlivy** (krytí IP, teplotní rozsah, EMC rušení, vibrace) a stanovit požadavky na mechanickou a elektrickou odolnost hardware.
- **Sestavit I/O bilanci** a navrhnout optimální řídicí jednotku z reálných katalogů výrobců pro konkrétní průmyslovou či IoT aplikaci včetně projektové rezervy.
- **Vypracovat vícekriteriální rozhodovací matici** a obhájit zvolenou platformu z technického a ekonomického hlediska (pořizovací cena, náročnost vývoje, údržba a spolehlivost).
- **Provést kritický technický audit (troubleshooting)** nevhodného návrhu řízení, identifikovat bezpečnostní a provozní rizika a navrhnout certifikované řešení v souladu s průmyslovými standardy.

## Ověření cílů

Výběr řídící jednotky pro různé aplikace

1. Příklady řídících jednotek
2. Jejich základní vlastnosti z hlediska výpočetního výkonu a velikosti paměťového prostoru
3. A z hlediska odolnosti
4. Příklady použití v praxi (kde se používají MCU, a kde ř. j. s MPU)

<!--
1. Správné vysvětlení pojmů, architektur a zkratek z oblasti řídicích systémů.
2. Schopnost posoudit vliv prostředí na výběr hardwaru a dešifrovat IP kód.
3. Vypracování rozhodovací matice pro volbu vhodné platformy (MCU vs. PLC vs. iPC).
4. Návrh konkrétní konfigurace řídicí jednotky na základě zadané I/O bilance a provozních podmínek.
5. Kritická technická oponentura (audit) nevhodně navrženého řešení.
-->


---

## Úlohy


### 1. Základní pojmy a architektury řídicích jednotek

*Časová dotace: 10–15 minut | Úvodní orientační úloha*

Doplňte do níže uvedené tabulky význam zkratek, základní princip a typický příklad reálného nasazení nebo zástupce:

| Zkratka / Pojem          | Co zkratka znamená (česky / anglicky) | Základní charakteristika (architektura, kde běží program)                                            | Typický zástupce (konkrétní rodina / model) | Příklad reálného nasazení                |
| :----------------------- | :------------------------------------ | :--------------------------------------------------------------------------------------------------- | :------------------------------------------ | :--------------------------------------- |
| **MCU** | Mikrořadič / *Microcontroller Unit* | Integrovaný čip (CPU + RAM + Flash na jednom substrátu), deterministický běh bez OS nebo RTOS | např. ESP32, PIC16LF1xxx, RP2040, STM32, ATmega328P | Termostat, pračka, dálkový ovladač, IoT čidlo, řízení motorku v aku nářadí |
| **MPU** | Mikroprocesor / *Microprocessor Unit* | Samostatný procesor vyžadující externí RAM a úložiště, zpravidla běží plnohodnotný OS (Linux) | ARM Cortex-A: Broadcom BCM2711/2712 (Raspberry Pi), NXP i.MX 8, TI Sitara AM335x | Raspberry Pi, HMI panely, routery, infotainment v autě, set-top boxy |
| **Embedded** | Vestavěný systém / *Embedded system* | Jednoúčelový počítač zabudovaný přímo v zařízení, které řídí. HW i SW je šitý na jednu funkci, uživatel ho často ani nevidí. Může být postaven na MCU i MPU. | Embedded PLC, Embedded PC | Bílá technika, bankomaty, regulace kotlů |
| **PLC** | Programovatelný logický automat / *Programmable Logic Controller* | Průmyslový automat pro cyklické deterministické řízení procesů, vysoká odolnost, modulární/kompaktní | Siemens S7-1200 / S7-1500, Allen-Bradley CompactLogix, Schneider Modicon M221/M241, Omron CP1 | Balicí a montážní linky, dopravníky, lisy, čerpací stanice, výtahy |
| **iPC** | Průmyslové PC / *Industrial PC* | PC architektura (x86/ARM) v odolném provedení: pasivní chlazení, SSD, napájení 24 V DC, montáž na DIN lištu nebo do panelu. Běží Windows/Linux, často i SoftPLC. | Siemens SIMATIC IPC (např. IPC427E), Beckhoff C6030, Advantech UNO/ARK | Strojové vidění, SCADA/HMI, sběr dat pro MES, řízení CNC a robotických buněk |
| **Programovatelné relé** | Programovatelné relé / *Programmable relay, logic module* | Zjednodušené kompaktní PLC pro méně náročné úlohy, nahrazuje časovací relé a stykačové kombinace | Siemens LOGO! 8, Eaton easyE4, Schneider Zelio Logic, Crouzet Millenium | Řízení osvětlení, závory, garážová vrata, zavlažování, větrání, jednoduché čerpadlo |

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **SoC (System on Chip):** Integrovaný obvod sdružující všechny klíčové elektronické obvody a komponenty celého počítače či elektronického systému na jediném křemíkovém čipu.
> 	 Systém na čipu. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-06-07 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Syst%C3%A9m_na_%C4%8Dipu
> - **DSP (Digital Signal Processor):** Specializovaný mikroprocesor architektury Harvard optimalizovaný pro matematické výpočty v reálném čase (rychlá Fourierova transformace FFT, filtrace šumu, digitální vektorové řízení střídavých motorů).
> 	Digitální signálový procesor. In: _Wikipedia: otevřená encyklopedie_ [online]. St. Petersburg (Florida): Wikimedia Foundation, 2006, poslední editace 28. 2. 2026 [cit. 2026-09-14]. Dostupné z: [Digitální signálový procesor – Wikipedie](https://cs.wikipedia.org/wiki/Digit%C3%A1ln%C3%AD_sign%C3%A1lov%C3%BD_procesor)
> - **FPGA (Field-Programmable Gate Array):** Programovatelné logické hradlové pole, jehož vnitřní struktura logických bloků a propojení je konfigurovatelná až u zákazníka. Umožňuje masivní paralelní zpracování s hardwarovou latencí v řádu nanosekund.
> 	Programovatelné hradlové pole. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-01-10 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Programovateln%C3%A9_hradlov%C3%A9_pole


<details>
<summary> :bulb: Tip k doplnění tabulky: </summary>
<p>Zaměřte se na čas náběhu a architekturu: U MCU je kód ve vnitřní paměti Flash procesoru a vykonává se okamžitě po přivedení napájení (řádově milisekundy). U systémů s MPU a iPC musí BIOS/bootloader nejprve zavést jádro operačního systému (OS Linux, Windows) z disku/eMMC/SD karty do operační paměti RAM, což trvá desítky sekund.</p>
</details>

:star2: **Bonusová otázka k úloze 1:**
Proč se u kritických aplikací v letectví (např. systém řízení letu Fly-by-Wire) nebo v jaderné energetice stále upřednostňují jednoduché deterministické mikrořadiče s několika desítkami kilobajtů paměti nebo obvody FPGA před moderními vícejádrovými gigahertzovými procesory s gigabajty RAM?

*Vaše odpověď:*
Jednoduchý deterministický čip má **předvídatelné časování** – nemá cache, spekulativní vykonávání ani jádra, která se přetahují o sběrnici, takže nejhorší dobu výpočtu (WCET) jde spočítat a doložit. Malý kód a jednoduchý HW jde kompletně otestovat a **certifikovat** (letectví DO-178C / DO-254, průmysl a jádro IEC 61508), u OS s miliony řádků to nejde. Méně tranzistorů a paměti = menší šance na překlopení bitu kosmickým zářením (SEU), snazší ochrana ECC a **redundancí** (3 kanály + hlasování). **FPGA** počítá paralelně přímo v hardwaru bez softwaru s odezvou v ns. Jednoduché čipy se navíc vyrábí desítky let – odpovídá to životnosti letadla či elektrárny.

---

### 2. Parametry, paměti a provozní odolnost (IP krytí)

*Časová dotace: max. 15 minut | Mírně náročnější úloha propojující parametry a praxi*

1. **Typy pamětí v řídicích jednotkách:**
   - Doplňte porovnání pamětí z hlediska stálosti dat a rychlosti:
     - **RAM:**
	     - Je volatilní (energeticky závislá)? **Ano**
	     - Rychlost zápisu: **velmi rychlá (ns), neomezený počet zápisů**
	     - K čemu se využívá v PLC/MCU: **běh programu – proměnné, zásobník, obraz vstupů/výstupů (PII/PIQ), mezivýsledky**
     - **Flash (ROM):**
	     - Je volatilní? **Ne**
	     - K čemu se využívá v PLC/MCU: **uložení programu (firmware, uživatelský program), bootloader, OS; v PLC paměťová karta s programem** *(zápis pomalejší, po blocích, cca 10⁴–10⁵ cyklů)*
     - **EEPROM / NVRAM:**
	     - Je volatilní? **Ne**
	     - K čemu se využívá v PLC/MCU: **konfigurace, kalibrační konstanty, remanentní data (čítače, motohodiny)** *(zápis po bajtech, cca 10⁵–10⁶ cyklů)*
   - *Otázka z praxe:* Kam se v průmyslovém PLC ukládají aktuální provozní proměnné (např. čítače vyrobených kusů nebo motohodiny), aby se při nečekaném výpadku napájení neztratily (tzv. remanentní / retain data)?
     - Odpověď: **Do remanentní (retain) paměti** – proměnná se v programu označí jako „retain“ a PLC ji při výpadku uchová buď v SRAM zálohované baterií/superkondenzátorem, nebo zápisem do FRAM/MRAM/EEPROM (S7-1200 ji při výpadku sám zapíše do vnitřní nevolatilní paměti).

2. **Reálný čas a determinismus (Hard vs. Soft Real-Time):**
   - Proč pro reakci na nouzové zastavení lisu (požadavek reakce do 5 ms) použijeme PLC či mikrokontrolér s RTOS, a nikoliv běžné Raspberry Pi s operačním systémem Raspberry Pi OS (standardní Linux)?
     - Odpověď: Běžný Linux **není hard real-time** – plánovač dělí čas CPU mezi stovky procesů a kvůli disku, správě paměti nebo síti může řídicí proces pozdržet o desítky ms (jitter). Odezvu do 5 ms tedy nejde **zaručit**, jen většinou splnit. PLC jede v pevném cyklu s watchdogem a RTOS má garantované priority, takže nejhorší doba odezvy je známá. Raspberry Pi navíc startuje desítky sekund a SD karta se může při výpadku poškodit. (Samotné nouzové zastavení musí být vždy i hardwarově přes bezpečnostní relé – viz úloha 5.)

3. **Odolnost vůči vlivům prostředí a dešifrování kódu IP:**
   - Dešifrujte kód **IP68**:
     - První číslice (6): **prachotěsné – úplná ochrana proti vniknutí prachu i dotyku**
     - Druhá číslice (8): **ochrana při trvalém ponoření do vody (hloubka a doba dle výrobce, více než 1 m)**
   - Jaké minimální krytí IP musí mít rozváděč umístěný ve venkovním nekrytém prostředí, kde na něj přímo dopadá déšť a fouká polétavý prach?
     - Označte správnou volbu: `[ ] IP20` | `[ ] IP44` | `[x] IP65` | `[ ] IP00`
     - Zdůvodnění: 6 = prachotěsné, 5 = odolá tryskající vodě z libovolného směru (déšť hnaný větrem). IP44 chrání jen proti tělesům > 1 mm a stříkající vodě, prach nezastaví; IP20 a IP00 jsou jen do vnitřních prostor.

4. **Konstrukční rozdíly kancelářského PC vs. průmyslového iPC:**
   - Vyberte a doplňte hlavní odlišnosti:
     - *Chlazení:*
	     - Kancelářské PC: aktivní ventilátory – nasávají prach a zanáší se
	     - vs. iPC: pasivní (fanless) – žebrovaná hliníková skříň slouží jako chladič, bez pohyblivých dílů
     - *Napájecí napětí a filtrace:*
	     - Kancelářské PC: 230 V AC přes ATX zdroj, minimální filtrace rušení
	     - vs. iPC: 24 V DC (často 9–36 V), EMC filtry, ochrana proti přepětí a přepólování, galvanické oddělení
     - *Odolnost proti otřesům a vibracím:* PC má HDD a volné karty/konektory, vibrace nesnese. iPC má SSD/eMMC, šroubované konektory, zajištěné karty a je testováno dle IEC 60068-2-6 (vibrace) a IEC 60068-2-27 (rázy).
     - *Způsob montáže:*
	     - Kancelářské PC: na stůl/pod stůl
	     - vs. iPC: na DIN lištu, do panelu (panel PC), do 19" racku nebo na stěnu rozváděče
     - *Provozní teplota (navíc):* PC cca 10–35 °C vs. iPC typicky 0–55 °C, odolné verze −20 až +60 °C

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Determinismus (Real-Time):** Vlastnost systému, která zaručuje, že odezva na vstupní událost proběhne vždy v přesně definovaném a předvídatelném čase (deadline). V *Hard Real-Time* systémech znamená nedodržení časového limitu fatální havárii celého procesu.
> 	Operační systém reálného času. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2024, 2024-05-12 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Opera%C4%8Dn%C3%AD_syst%C3%A9m_re%C3%A1ln%C3%A9ho_%C4%8Dasu
> - **Krytí IP (Ingress Protection):** Mezinárodní standard dle normy **ČSN EN 60529** určující stupeň ochrany krytem před vniknutím pevných cizích těles včetně prachu (1. číslice 0–6) a vniknutím vody (2. číslice 0–9K).
> 	ČESKÝ NORMALIZAČNÍ INSTITUT. *ČSN EN 60529 (33 0330) Stupně ochrany krytem (krytí - IP kód)*. Praha: Český normalizační institut, 1993. Třídící znak 330330.
> - **Remanentní paměť (Retain):** Paměťový prostor v PLC, jehož obsah zůstává zachován i po přerušení napájecího napětí (využívá zálohovací baterii, superkondenzátor nebo zápis do FRAM/MRAM/EEPROM).

<details>
<summary> :bulb: Tip k otázce determinismu: </summary>
<p>Běžný Linux je <b>preemptivní víceúlohový systém</b>, který se snaží spravedlivě rozdělit čas procesoru mezi stovky procesů. Může se stát, že kvůli obsluze disku, správě paměti nebo síťovému provozu se proces řízení pozdrží na desítky milisekund. PLC naproti tomu vykonává cyklus v pevném taktu bez zpoždění vyvolaného aplikacemi na pozadí.</p>
</details>

:star2: **Bonusová otázka k úloze 2:**
Co označuje doplňkové písmeno **K** v kódu krytí **IP69K** a v jakém průmyslovém odvětví je toto krytí bezpodmínečně vyžadováno?

*Vaše odpověď:*
**K** pochází z německé normy DIN 40050-9 (dnes ISO 20653, původně pro silniční vozidla) a znamená odolnost proti **vysokotlakému čištění horkou vodou** (cca 80 °C, 80–100 bar, tryska ze vzdálenosti 10–15 cm). Bezpodmínečně se vyžaduje v **potravinářství** (mlékárny, masný průmysl, nápoje), kde se linky denně sanitují tlakovou vodou a chemií; dále ve farmacii a u mycích linek.

---

### 3. Rozhodovací matice platforem (MCU vs. PLC vs. iPC)

*Časová dotace: 20–25 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jste v pozici nezávislého konzultanta automatizace. Tři různí zákazníci požadují navrhnout optimální kategorii řízení.

#### Příklad aplikace (vzorové řešení):
- **Vzorová aplikace 0 – Automatická vjezdová závora na parkoviště:** Jednoduchý jednoúčelový systém s indukční detekční smyčkou vozidla, bezpečnostní optozávorou, koncovými spínači polohy ramene, motorem závory (vpřed/vzad) a výstražným semaforem (červená/zelená). Požadavek na jednoduchou správu správcem objektu a spolehlivý chod v rozváděči u vjezdu.

#### Popis zadaných aplikací pro studenty:
1. **Aplikace A – Chytrý pokojový termostat (IoT):** Bateriově napájený přístroj měřící teplotu a vlhkost v místnosti, zobrazující údaje na e-ink displeji a odesílající data přes protokol ZigBee/Wi-Fi do domácí brány. Plánovaná sériová výroba: 10 000 kusů ročně.
2. **Aplikace B – Automatická balicí linka:** Průmyslová linka ve výrobní hale. Obsahuje 28 optických snímačů, 14 pneumatických válců, 3 dopravníkové pásy s asynchronními motory a bezpečnostní světelnou závoru. Vyžaduje se nepřetržitý provoz 24/7 a snadná údržba podnikovým elektrikářem.
3. **Aplikace C – Kontrolní stanice optické jakosti svarů:** Pracoviště se 2 vysokorychlostními průmyslovými GigE kamerami snímajícími svary na karoserii automobilu. Snímky v rozlišení 4K jsou analyzovány neuronovou sítí v reálném čase, vady jsou označeny a ukládány do podnikové relační databáze (SQL / MES).

#### Váš úkol:
Vyplňte rozhodovací matici. Jako vzor poslouží vyplněný sloupec pro **Vzorovou aplikaci 0**. Přiřaďte každé aplikaci nejvhodnější platformu (**MCU / Embedded SoC**, **Kompaktní/modulární PLC**, **Průmyslové PC – iPC**) a doplňte multikriteriální posouzení:

| Kritérium hodnocení                                                                                   | **Vzorová aplikace 0 (Vjezdová závora - VZOR)**                                                                                                                                                                           | Aplikace A (Pokojový termostat) | Aplikace B (Balicí linka) | Aplikace C (Kamerová kontrola svarů) |
| :---------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------ | :------------------------ | :----------------------------------- |
| **Doporučená platforma** *(MCU / PLC / iPC)*                                                          | **Programovatelné relé / kompaktní PLC** *(např. Siemens LOGO!, Eaton easyE4)*                                                                                                                                            | **MCU / embedded SoC** *(např. ESP32-C6 – Wi-Fi + Zigbee v jednom čipu, nebo Silicon Labs EFR32MG)* | **Modulární PLC** *(např. Siemens S7-1500 F-CPU, nebo S7-1200 + decentrální I/O ET 200SP)* | **iPC s GPU** *(např. SIMATIC IPC s grafickou kartou NVIDIA, nebo průmyslový edge PC s NVIDIA Jetson AGX Orin)* |
| **Pořizovací cena HW na 1 kus** *(nízká < 500 Kč / střední 5–30 tis. Kč / vysoká > 50 tis. Kč)*       | **Střední** *(cca 3 500 – 6 000 Kč)*                                                                                                                                                                                      | **Nízká** *(< 500 Kč; čip desítky Kč, celá deska s e-ink stovky Kč)* | **Střední až vysoká** *(CPU desítky tis. Kč, s I/O moduly a bezpečnostní částí > 50 tis. Kč)* | **Vysoká** *(> 50 tis. Kč; iPC s GPU cca 80–200 tis. Kč)* |
| **Primární programovací jazyk** *(C/C++/MicroPython vs. IEC 61131-3 ST/LAD vs. Python/C#/C++ pod OS)* | **FBD / LAD** *(grafické funkční bloky nebo liniové schéma dle IEC 61131-3)*                                                                                                                                              | **C/C++** *(ESP-IDF, Zephyr; MicroPython jen na prototyp)* | **LAD / FBD** pro údržbu, **SFC** (GRAPH) pro sekvence, **ST** pro výpočty – vše IEC 61131-3 | **Python / C++** pod OS *(OpenCV, PyTorch, TensorRT)*, **C#** pro GUI, **SQL** pro databázi |
| **Klíčový technický argument pro volbu** *(např. spotřeba, determinismus, grafický výkon)*            | Montáž přímo na DIN lištu v rozváděči, integrovaný displej pro nastavení časovačů přímo na místě, robustní reléové výstupy pro motor a semafor, napájení 24 V DC / 230 V AC bez nutnosti vývoje vlastního plošného spoje. | **Spotřeba a sériovost.** V hlubokém spánku odběr jednotky µA, baterie vydrží i roky. Rádio (Wi-Fi/Zigbee) je integrované v čipu. Při 10 000 ks/rok se vývoj vlastní desky rozpustí a každá ušetřená koruna se násobí 10 000. | **Determinismus a údržba.** Pevný cyklus v ms, provoz 24/7, 42+ I/O po modulech, diagnostické LED, výměna modulu za chodu. Údržbář program přečte v LAD. Světelná závora přes F-CPU nebo bezpečnostní relé (PL d/e), měniče pásů po PROFINETu. | **Výpočetní výkon.** Jeden 4K snímek = 3840 × 2160 px × 3 B ≈ 25 MB. Neuronová síť potřebuje GPU a GB RAM. OS dává ovladače GigE Vision (2 síťové karty), SQL klienta a napojení na MES (OPC UA). |
| **Hlavní riziko při volbě špatné platformy** *(proč by neuspěly ostatní dvě varianty)*                | **MCU:** Nutnost vývoje vlastní desky, nízká odolnost vůči venkovnímu rušení a obtížný servis údržbou.<br>**iPC:** Zbytečně extrémní cena (> 30 tis. Kč), dlouhý start po výpadku napájení a vysoká spotřeba.             | **PLC:** z baterie ho nenapájíš (spotřeba W), cena tisíce Kč × 10 000 ks, velikost, nemá e-ink ani Zigbee.<br>**iPC:** spotřeba desítky W, cena desítky tisíc Kč, absurdní rozměr. | **MCU:** vlastní deska bez certifikace, EMC problémy v hale, servis jen původní programátor, bezpečnost nejde doložit.<br>**iPC:** aktualizace či pád Windows, dlouhý start, disk, elektrikář ho neopraví, zbytečně drahé. | **MCU:** kB RAM – jeden 4K snímek se do něj nevejde, nemá GigE.<br>**PLC:** cyklický logický automat bez GPU, neuronovou síť ani databázi neutáhne (zůstane řídit linku, iPC mu posílá výsledek OK/NOK). |

> **Kritéria hodnocení úlohy 3 (bodování a známka):**
> - :star: **Správnost technického přiřazení platforem (30 %):** Stoprocentně logické a obhajitelné přiřazení všech 3 technologií.
> - :star: **Inženýrská a ekonomická argumentace (40 %):** Zohlednění ekonomiky sériovosti (kusová vs. masová výroba), spotřeby energie, náročnosti vývoje a schopností servisního personálu.
> - :star: **Analýza rizik nevhodné platformy (30 %):** Věcné zdůvodnění, proč je v daném případě jiná platforma neefektivní, příliš drahá nebo neschopná úlohu odbavit.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Norma ČSN EN 61131-3:** Mezinárodní standard pro programovací jazyky PLC automatů. Definuje dva textové jazyky (ST – strukturovaný text, IL – seznam instrukcí) a tři grafické jazyky (LD – příčkový diagram / kontaktní schéma, FBD – funkční blokové schéma, SFC – sekvenční funkční schéma).
> 	ČESKÝ NORMALIZAČNÍ INSTITUT. *ČSN EN 61131-3 ed. 3 (18 0080) Programovatelné řídicí jednotky - Část 3: Programovací jazyky*. Praha: Úřad pro technickou normalizaci, metrologii a státní zkušebnictví, 2014. Třídící znak 180080.
> - **GigE Vision:** Komunikační standard rozhraní pro průmyslové kamery využívající gigabitový Ethernet, umožňující přenos nekomprimovaného videa vysokou rychlostí na velké vzdálenosti.

<details>
<summary> :bulb: Tip pro Aplikaci A vs. B vs. C: </summary>
<p>U aplikace A rozhoduje kusová cena a odběr proudu z baterie (PLC ani iPC z baterie nerozběhnete). U aplikace B potřebujete vyměnitelný modul na DIN lištu s diagnostickými LED, který přeprogramuje běžný údržbář v jazyce LAD. U aplikace C potřebujete obrovský výpočetní výkon pro AI a ovladače pro průmyslové kamery, což MCU ani běžné PLC nezvládne.</p>
</details>

:star2: **Bonusová otázka k úloze 3:**
Co je to tzv. **SoftPLC** a jak umožňuje průmyslovému PC (iPC) kombinovat výhody operačního systému Windows/Linux a deterministického řízení reálného času v jediném fyzickém počítači?

*Vaše odpověď:*
**SoftPLC** je PLC runtime jako software běžící na PC. Hypervizor nebo real-time jádro rozdělí procesor: jedno či více jader dostane výhradně PLC program (IEC 61131-3) s deterministickým cyklem, na zbylých jádrech běží Windows/Linux s HMI, databází nebo strojovým viděním. Oba světy si předávají data přes sdílenou paměť; u řešení s hypervizorem PLC běží dál i při pádu Windows. Výhoda: jeden HW, rychlá výměna dat, nižší cena. Příklady: **Beckhoff TwinCAT 3**, **Siemens S7-1500 Software Controller**, **CODESYS Control RTE**.

---

### 4. Návrh a konfigurace řídicí jednotky pro čerpací stanici

*Časová dotace: 25–30 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jste v roli projektanta automatizace. Zákazník poptává zhotovení řízení pro obecní přečerpávací stanici odpadních vod.

#### Zadání technologického procesu a periferií:
- **Snímače a vstupy:**
  - 3× plovákový hladinový spínač (havarijní spodní hladina proti chodu nasucho, zapínací hladina, havarijní přepad) – bezpotenciálový kontakt spínající 24 V DC.
  - 1× hydrostatická ponorná sonda výšky hladiny v jímce – výstupní signál 4–20 mA.
  - 1× termistorové ochranné relé přehřátí motoru čerpadla – poruchový kontakt 24 V DC.
- **Akční členy a výstupy:**
  - 2× stykač pro spouštění motorů hlavního a záložního čerpadla – spínání cívky stykače 230 V AC / 0,5 A.
  - 1× opticko-akustický výstražný maják – napájení 24 V DC / 0,3 A.
  - 1× řízení otáček frekvenčního měniče hlavního čerpadla – analogový signál 0–10 V.
- **Komunikace a přenos dat:**
  - Odesílání údajů o hladině a poruchách na dispečink vodáren (Ethernet / Modbus TCP nebo GSM/LTE modul).
- **Provozní podmínky:**
  - Venkovní nekrytý terén, rozváděč vystavený dešti, prachu a teplotám v rozmezí **-20 °C až +45 °C**.

#### Váš úkol:

1. **Sestavte tabulku I/O bilance** a spočtěte celkový počet signálů. Připočtěte rezervu min. 20 % pro budoucí rozšíření:

| Typ signálu | Požadavek aplikace (kusy) | Popis signálů v aplikaci | Počet po započtení rezervy (+20 %) |
| :--- | :--- | :--- | :--- |
| **Digitální vstup (DI)** | 4 | LS1 min. hladina (chod nasucho), LS2 zapínací hladina, LS3 havarijní přepad, termistorové relé motoru | 4 × 1,2 = 4,8 → **5** |
| **Digitální výstup (DO) – reléový** | 2 | Cívky stykačů K1 (hlavní čerpadlo) a K2 (záložní) – 230 V AC / 0,5 A | 2 × 1,2 = 2,4 → **3** |
| **Digitální výstup (DO) – tranzistorový** | 1 | Opticko-akustický maják – 24 V DC / 0,3 A | 1 × 1,2 = 1,2 → **2** |
| **Analogový vstup (AI)** | 1 | Hydrostatická sonda výšky hladiny – 4–20 mA | 1 × 1,2 = 1,2 → **2** |
| **Analogový výstup (AO)** | 1 | Žádaná hodnota otáček frekvenčního měniče hlavního čerpadla – 0–10 V | 1 × 1,2 = 1,2 → **2** |
| **Celkem** | **9** | | **14** *(zaokrouhleno nahoru u každého typu zvlášť)* |

2. **Výběr konkrétního hardwaru z katalogu výrobce:**
   - Navrhněte konkrétní přístroj z praxe (např. *Siemens LOGO! 24RCE + rozšiřující moduly*, *Siemens S7-1200 CPU 1212C/1214C DC/DC/RLY*, *Schneider Modicon M221*, *Eaton easyE4-UC-12RC1*, *WAGO 750*, případně průmyslový IoT kontrolér typu *UniPi Neuron*).
   - Uveďte:
     - Výrobce a přesný model CPU: **Siemens SIMATIC S7-1200, CPU 1214C DC/DC/RLY** (14 DI 24 V DC, 10 DO relé 2 A, 2 AI 0–10 V, 1× PROFINET)
     - Objednací kód (Part Number / Order Code): **6ES7214-1HG40-0XB0**
     - Rozšiřující moduly (pokud jsou nutné pro AI 4–20 mA nebo AO 0–10 V): **SM 1234 AI4/AQ2 – 6ES7234-4HE32-0XB0** (4 AI ±10 V nebo 0/4–20 mA, 2 AQ ±10 V nebo 0–20 mA; vestavěné AI na CPU umí jen napětí) + **CP 1243-7 LTE EU – 6GK7243-7KX30-0XE0** s venkovní anténou
     - Napájecí napětí zvolené jednotky: **24 V DC** (20,4–28,8 V) z průmyslového zdroje na DIN lištu (např. SITOP / LOGO!Power 24 V / 2,5 A)
     - Jak je vyřešeno odesílání dat na dispečink: Je-li k dispozici kabel – integrovaný Ethernet a **Modbus TCP** (instrukce MB_CLIENT / MB_SERVER v TIA Portalu). Bez kabelu – **CP 1243-7 LTE** po mobilní síti vč. SMS alarmů (Siemens tuto kombinaci nabízí jako RTU pro vodárny a čistírny).
     - Odkaz na technický list (datasheet): https://docs.rs-online.com/c302/0900766b81397278.pdf (CPU 1214C), https://media.automation24.com/datasheet/nl/6ES72344HE320XB0.pdf (SM 1234)
     - Odkazy na další použité zdroje: https://mall.industry.siemens.com/mall/en/ww/Catalog/Product/?mlfb=6ES7214-1HG40-0XB0 , https://www.automation24.com/communication-processor-siemens-cp-1243-7-lte-eu-6gk7243-7kx30-0xe0
     - *Alternativa:* CPU 1214C DC/DC/DC (6ES7214-1AG40-0XB0) s 10 tranzistorovými výstupy 0,5 A – maják na tranzistorový výstup, stykače přes vazební relé. U verze RLY může maják spínat reléový výstup (relé spíná i 24 V DC, 0,3 A < 2 A).

3. **Technické ověření z datasheetu:**
   - Zvládá zvolená jednotka garantovaný provoz při -20 °C? Doložte údaj z datasheetu: **Ano.** Datasheet 6ES7214-1HG40-0XB0 uvádí provozní teplotu okolí **−20 °C až +60 °C** při vodorovné montáži (při svislé −20 °C až +50 °C), relativní vlhkost do 95 % bez kondenzace – proto do skříně patří topení s hygrostatem.
   - Jakým způsobem spínáte cívku stykače 230 V AC (reléový výstup jednotky přímo, nebo přes pomocné mezilehlé relé)? Zdůvodněte: **Přes vazební (mezilehlé) relé** s cívkou 24 V DC. Reléový výstup by to přímo zvládl (2 A > 0,5 A), ale vazební relé zajistí galvanické oddělení 230 V od PLC, chrání výstup před přepětím z indukční cívky (na cívku stykače navíc RC člen / varistor) a při opálení se mění levné relé, ne výstup CPU.

4. **Krytí rozváděče:**
   - Jaké minimální krytí **IP skříně** zvolíte? Jak v rozváděči zajistíte provoz v mrazech -20 °C a v letních vedrech?
     - Zvolené krytí rozváděče: **min. IP65, doporučuji IP66** – polyesterová nebo nerezová UV odolná skříň, kabelové vývodky IP68. *(Navíc: jímka odpadních vod může být prostor s nebezpečím výbuchu – metan, sulfan – proto plováky a sondu v provedení Ex a rozváděč mimo jímku.)*
     - Teplotní management skříně: **Mráz:** PTC topení (desítky W) s termostatem (zapíná pod cca +5 °C) a hygrostatem proti kondenzaci. **Léto:** stříška proti přímému slunci, světlá barva skříně, případně filtrační ventilátor s krytím IP55 dimenzovaný podle ztrátového výkonu přístrojů. K tomu přepěťové ochrany (SPD) na signálech z jímky.

> **Kritéria hodnocení úlohy 4 (bodování a známka):**
> - :star: **Správnost I/O bilance a dimenzování (30 %):** Správný součet všech signálů, korektní rozlišení reléových vs. tranzistorových výstupů a správné započtení rezervy min. 20 %.
> - :star: **Reálnost výběru a kompatibilita HW (40 %):** Zvolený přístroj skutečně existuje na trhu, konfigurace plně pokrývá všechny vstupy/výstupy (včetně analogů 4–20 mA a 0–10 V) a komunikaci.
> - :star: **Posouzení provozních podmínek a instalace (30 %):** Správná volba krytí rozváděče (min. IP65), vyřešení vytápění/ventilace pro mráz a spolehlivé galvanické oddělení výkonových akčních členů.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Proudová smyčka 4–20 mA:** Průmyslový standard pro přenos analogových signálů ze senzorů. Výhodou oproti napěťovému signálu 0–10 V je vysoká odolnost proti elektromagnetickému rušení, nezávislost na odporu dlouhého vedení a detekce přetržení vodiče (pokud je proud roven 0 mA, jde o poruchu vedení – tzv. živá nula / live zero).
> 	Proudová smyčka. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2023, 2023-04-18 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Proudov%C3%A1_smy%C4%8Dka
> - **Galvanické oddělení:** Elektrické oddělení dvou elektrických obvodů (např. pomocí optočlenů nebo relé), které zabraňuje přenosu rušení, rozdílům zemních potenciálů a chrání citlivé vstupy řídicí jednotky před zničením přepětím.
> - **Bezpotenciálový kontakt** (označovaný také jako **dry contact**) je elektrický kontakt, který sám o sobě nemá žádné vlastní napětí ani neposkytuje žádný proud. Funguje čistě jako mechanický nebo elektronický spínač (jako klasický vypínač na zdi), který pouze spojí nebo rozpojí dva vodiče v externím obvodu.

<details>
<summary> :bulb: Tip pro výběr modulů: </summary>
<p>Pozor na analogové vstupy: Základní kompaktní jednotky (např. LOGO! nebo S7-1200) mívají integrované analogové vstupy pouze pro napětí 0–10 V. Vstupní signál 4–20 mA ze sondy vyžaduje buď speciální rozšiřující modul pro proudové signály, nebo zařazení přesného paralelního odporu 500 Ω (převod 4–20 mA na 2–10 V).</p>
</details>

:star2: **Bonusová otázka k úloze 4:**
Proč se u čerpadel v čistírnách odpadních vod a jímkách striktně upřednostňuje měření hladiny pomocí proudového signálu 4–20 mA před napěťovým signálem 0–10 V a proč se do jímky nepoužívá ultrazvukový senzor, pokud v ní vzniká hustá pěna?

*Vaše odpověď:*
**4–20 mA:** proud je v celé smyčce stejný, takže nezáleží na odporu dlouhého kabelu k jímce; signál s nízkou impedancí je odolný proti rušení od motorů a měničů. „Živá nula“ 4 mA – když teče 0 mA, je přerušený vodič a PLC vyhlásí poruchu (u 0–10 V vypadá 0 V stejně jako prázdná jímka). Sondu lze napájet přímo ze smyčky dvěma vodiči.

**Ultrazvuk a pěna:** ultrazvuk měří dobu letu odrazu od hladiny. Hustá pěna zvuk pohltí nebo ho odrazí od svého povrchu, takže čidlo ukáže špatnou výšku nebo nic; škodí i páry a kondenzát na čidle. Hydrostatická sonda měří tlak sloupce kapaliny, a ten pěna neovlivní.

---

### 5. Technický audit a oponentura nevhodného návrhu

*Časová dotace: 20–25 minut | :star: Klasifikovaná inženýrská úloha na známky*

Jako vedoucí inženýr jste převzal projekt po nezkušeném brigádníkovi, který navrhl řízení automatizovaného tvářecího a lisovacího stroje v prašné kovářské dílně následovně:
- **Řídicí deska:** Běžná vývojová deska **Arduino Uno (Rev3)** s mikrokontrolérem ATmega328P.
- **Pouzdro a umístění:** Plastová krabička vytištěná na 3D tiskárně z materiálu **PLA**, přišroubovaná přímo na těleso vibrujícího hydraulického lisu.
- **Napájení:** 5V USB nabíječka na mobilní telefon zapojená do prodlužovacího kabelu 230 V.
- **Spínání zátěže:** 4kanálový hobby reléový modul z čínského e-shopu propojený s Arduinem tenkými nepájenými vodiči (DuPont propojky). Modul přímo spíná 400V ventily hydrauliky.
- **Bezpečnost (Safety):** Nouzové stop tlačítko (E-Stop) je zapojeno přímo do digitálního pinu D2 Arduina jako softwarové přerušení (interrupt), které v kódu nastaví výstupy na `LOW`.

#### Váš úkol:

1. **Zpracujte písemný audit rizik (minimálně 4 fatální technická selhání):**
   Vyplňte protokol o zjištěných vadách a popište konkrétní fyzikální mechanismus, jak daná chyba způsobí havárii stroje či ohrožení lidského života:

| Oblast auditu | Zjištěná vada v amatérském návrhu | Fyzikální mechanismus selhání (proč to selže) | Následek pro stroj nebo obsluhu |
| :--- | :--- | :--- | :--- |
| **Elektromagnetická kompatibilita (EMC)** | Indukční cívky 400V ventilů spínané hobby relé bez odrušení (RC člen, varistor), 5 V logika hned vedle silových vodičů, žádné stínění ani galvanické oddělení | Napěťové špičky z indukční zátěže hydraulických ventilů způsobí restart MCU... Při rozepnutí cívky vznikne indukované napětí u = −L·di/dt v řádu kV, jiskra na kontaktu vyzařuje rušení, které se naindukuje do vodičů a šíří společnou zemí. Napájení ATmega poklesne (brown-out reset), vstupy čtou nesmysly, RAM se může přepsat. | Náhodný restart nebo zamrznutí, ventil zůstane v posledním stavu nebo sám sepne → nečekaný pohyb lisu, zničený čip, ohrožení obsluhy |
| **Mechanická a teplotní odolnost** | PLA plast a montáž na těleso lisu | PLA má skelný přechod kolem 60 °C – hydraulický olej a okolí výhní ho snadno ohřejí, plast změkne a zdeformuje se. Vibrace způsobí únavu materiálu, praskání mezi vrstvami tisku a uvolnění šroubů. PLA není samozhášivé a netěsná krabička pustí dovnitř vodivý kovový prach. | Krabička se zkroutí/rozpadne, odhalí živé části 230/400 V → úraz elektřinou; kovový prach způsobí zkrat na desce, hrozí požár |
| **Konektivita a propojení vodičů** | DuPont propojovací kabely bez aretace | Vibrace způsobí mikropohyby v konektoru, kontakty se oxidují třením (fretting), roste přechodový odpor, až se spoj vysune. Tenké vodiče se lámou, signál přerušovaně mizí a vstup zůstane plovoucí. | Relé náhodně spíná/rozpíná → pohyb lisu bez povelu. Vypadne-li vodič E-Stopu zapojeného jako spínací (NO), tlačítko přestane fungovat a nikdo to nepozná |
| **Funkční bezpečnost (Safety)** | Nouzový stop řešený softwarově v čipu | Software se může zacyklit, zamrznout nebo přetéct zásobník – interrupt pak neproběhne. Svařený kontakt relé software nerozepne. Jeden kanál bez kontroly, přerušení vodiče se nepozná. Nesplňuje ČSN EN ISO 13850 ani ČSN EN ISO 13849-1. | Lis nejde zastavit, když je v něm ruka → rozdrcení končetin, smrtelný úraz; plná odpovědnost provozovatele |
| **Napájení** *(navíc)* | 5V USB nabíječka v prodlužovačce | Není pro průmysl (EN 61204), nemá filtraci ani přepěťovou ochranu, zvlnění a špičky ze sítě pošle rovnou do MCU, dá se omylem vytáhnout | Náhodné resety, zničení desky, výpadek řízení |

2. **Návrh profesionálního nápravného řešení:**
   - Navrhněte, jakými certifikovanými průmyslovými komponenty tento celek nahradíte při zachování minimálního rozpočtu:
     - *Náhrada řídicí jednotky:* **Programovatelné relé Siemens LOGO! 8 (24RCE) nebo Eaton easyE4** na DIN liště v oceloplechovém rozváděči IP54+ mimo lis, na antivibračních úchytech. Ventily přes stykače / vazební relé s odrušením cívek (RC člen, varistor), svorky místo DuPont kabelů, vodiče s dutinkami. *(např. certifikované průmyslové programovatelné relé s montáží na DIN lištu a krytím)*
     - *Náhrada napájecího zdroje:* **Průmyslový stabilizovaný zdroj 24 V DC na DIN lištu** (např. Siemens SITOP / LOGO!Power 24 V, 2,5 A) s ochranou proti zkratu a přepětí, jištěný jističem. *(např. stabilizovaný průmyslový zdroj 24 V DC na DIN lištu s ochranou proti přepětí)*
     - *Způsob zapojení bezpečnostního okruhu (Safety):* Jak musí být podle norem zapojeno tlačítko Emergency Stop (E-Stop)? Smí být spoléháno pouze na software mikrokontroléru? Zdůvodněte: E-Stop (červený hřib na žlutém podkladu, ČSN EN ISO 13850) musí mít **rozpínací (NC) kontakty s nuceným rozepnutím**, zapojené **dvoukanálově** do certifikovaného **bezpečnostního relé** (Pilz PNOZ, Siemens SIRIUS 3SK1, Schneider Preventa). To přes **2 stykače v sérii s nuceně vedenými kontakty** hardwarově odpojí napájení ventilů, se zpětnou kontrolou stykačů (EDM) a ručním resetem. **Na software MCU se spoléhat nesmí** – software může zamrznout a relé se může svařit. NC kontakt je „fail-safe“: přetržený vodič = stop. PLC smí dostat jen informační kontakt.

> **Kritéria hodnocení úlohy 5 (bodování a známka):**
> - :star: **Odborná úroveň identifikace závad (35 %):** Přesná technická terminologie (např. elektromagnetická indukce, absence odrušovacích varistorů, skelný přechod PLA plastu při 60 °C, studené spoje a vyklepání konektorů vibracemi).
> - :star: **Pochopení norem funkční bezpečnosti Safety (35 %):** Znalost základního principu bezpečnosti strojních zařízení – nouzové zastavení musí být řešeno hardwarově přes certifikované bezpečnostní relé s nuceně vedenými kontakty, nikoliv pouhým softwarovým vstupem MCU.
> - :star: **Kvalita a realizovatelnost nápravného řešení (30 %):** Návrh odpovídá robustní průmyslové praxi s montáží do oceloplechového rozváděče na DIN lištu.

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **Funkční bezpečnost (Safety) vs. Kybernetická bezpečnost (Security):** *Safety* (dle ČSN EN ISO 13849-1) zajišťuje, že strojní zařízení nezpůsobí úraz člověku ani při vnitřní poruše řídicího systému (využívá redundantní obvody, bezpečnostní relé, optické závory, kategorii spolehlivosti PL a až PL e / SIL 3). *Security* řeší ochranu dat a systému před úmyslným napadením zvenčí (hackeři, malware).
> - **EMC (Elektromagnetická kompatibilita):** Schopnost zařízení spolehlivě pracovat v prostředí s elektromagnetickým rušením (odolnost / imunita) a současně nezpůsobovat nepřípustné rušení jiným zařízením (emise).
> 	Elektromagnetická kompatibilita. *Wikipedie: Otevřená encyklopedie* [online]. San Francisco (CA): Wikimedia Foundation, 2023, 2023-11-20 [cit. 2026-09-17]. Dostupné z: https://cs.wikipedia.org/wiki/Elektromagnetick%C3%A1_kompatibilita

<details>
<summary> :bulb: Tip k bezpečnostnímu okruhu (Safety): </summary>
<p>Základní pravidlo bezpečnosti: <strong>Software může selhat, zacyklit se nebo zamrznout.</strong> Bezpečnostní okruh nouzového zastavení (červený hřib) musí být vždy dvoukanálový, zapojený do hardwarového bezpečnostního relé (např. Pilz, Schneider Preventa, Siemens SIRIUS), které odpojí silové napájení stykačů ventilů přímo na hardwarové úrovni nezávisle na procesoru!</p>
</details>

:star2: **Bonusová otázka k úloze 5:**
Proč hobby reléové moduly s optočleny určené pro Arduino v průmyslovém rozváděči často shoří nebo způsobí trvalé sepnutí zátěže (tzv. přivaření kontaktů), i když jmenovitý proud relé je 10 A a cívka stykače odebírá jen 0,5 A?

*Vaše odpověď:*
Údaj **10 A platí pro odporovou zátěž (AC-1)**. Pro indukční zátěž (AC-15 / DC-13) je dovolený proud mnohem menší – při rozepínání cívky vzniká elektrický oblouk, který kontakty propaluje a **přivaří** je k sobě (trvalé sepnutí). Při sepnutí cívky stykače teče **záběrový proud** několikanásobně větší než trvalých 0,5 A. Relé jsou dimenzovaná na 250 V AC, ne na 400 V, a malé izolační/povrchové vzdálenosti na levném PCB umožní přeskok mezi silovou a 5 V částí. Optočlen často nic neodděluje (propojka JD-VCC spojí zem), chybí RC člen a levná neoriginální relé mají nadsazené parametry, které se v teplém rozváděči ještě zhorší.

---

### 6. Rozšiřující inženýrská výzva: TCO a životní cyklus v automatizaci

*Časová dotace: 15–20 minut | :star2: Bonusová výzva pro pokročilé studenty*

V průmyslové automatizaci nákupní cena řídicí jednotky (CAPEX) často tvoří méně než 15 % celkových nákladů na životní cyklus zařízení (OPEX / TCO).

Představte si, že management firmy rozhoduje mezi dvěma variantami řízení pro sérii 50 kusů výrobních linek s plánovanou životností 15 let:
- **Varianta 1 (Nízkonákladová na pořízení):** Využití levných embedded mikrokontrolérových desek s vlastním zákaznickým návrhem plošného spoje (cena HW: 2 500 Kč / kus, vývoj firmwaru v C/C++ od externího programátora bez dokumentace).
- **Varianta 2 (Průmyslový standard):** Využití modulárního PLC renomovaného výrobce (Siemens / Rockwell / Schneider) s cenou 22 000 Kč / kus, programováno v normovaném jazyce LAD/ST dle IEC 61131-3.

#### Váš úkol:
1. Srovnejte obě varianty v níže uvedené tabulce a uveďte předpokládaná skrytá rizika a náklady v horizontu 10–15 let:

| Aspekt životního cyklu | Varianta 1 (Custom Embedded MCU) | Varianta 2 (Průmyslové PLC) |
| :--- | :--- | :--- |
| **Dostupnost náhradních dílů za 10 let** | Čip může skončit (EOL) za pár let (viz krize čipů 2021–22). Deska je na zakázku – chybí-li podklady (Gerber, BOM, zdroják), musí se navrhnout znovu. | Výrobce garantuje dostupnost a opravy řadu let i po ukončení výroby (typicky až 10 let), vydává plán životního cyklu a kompatibilního nástupce s migračním návodem. |
| **Servisovatelnost podnikovým elektrikářem** | Prakticky žádná – nutný programátor v C, osciloskop a zdrojový kód. Nedokumentovaný kód umí opravit jen jeden člověk. | Běžný elektrikář: diagnostické LED, online sledování programu v TIA Portalu, LAD vypadá jako elektrické schéma. |
| **Doba odstávky linky při poruše CPU** | Dny až týdny (hledání chyby, výroba nové desky, nahrání firmwaru – pokud ho vůbec někdo má). | Desítky minut: náhradní CPU ze skladu, vložit paměťovou kartu s programem, zapnout. |
| **Cena vývojových nástrojů a licencí IDE** | Překladače často zdarma (GCC, STM32CubeIDE), ale drahá je práce vývojáře, testy a certifikace desky (CE, EMC) – řádově stovky tisíc Kč. | Licence TIA Portal STEP 7 v řádu desítek tisíc Kč + upgrady; stačí jedna pro celý podnik, vývoj je rychlejší a standardizovaný. |
| **Závěrečné doporučení (kterou variantu vybrat a proč)** | **Nedoporučuji.** Úspora CAPEX 50 × (22 000 − 2 500) = 975 000 Kč zmizí po necelých 10 h odstávky při 100 000 Kč/h; hrozí vendor lock-in na jednoho programátora. | **Doporučuji.** Nižší TCO za 15 let: krátké odstávky, servis vlastními lidmi, dostupné díly, norma IEC 61131-3. |

> :key: **Vysvětlení pojmů a odborné zdroje:**
> - **CAPEX (Capital Expenditure)**: Zjednodušeně jde o jednorázové kapitálové výdaje na pořízení samotného zařízení (hardware, licence).
> - **OPEX (Operating Expense)**: Zjednodušeně jde o průběžné provozní náklady nutné k udržení zařízení v chodu (energie, servis, podpora).
> - **TCO (Total Cost of Ownership):** Finanční odhad celkových přímých i nepřímých nákladů spojených s pořízením, provozem, servisem, údržbou a likvidací produktu po celou dobu jeho životnosti. Zjednodušeně je to součet CAPEX + OPEX za celou dobu životnosti zařízení.
> 	Total cost of ownership. *Wikipedia: The Free Encyclopedia* [online]. St. Petersburg (Florida): Wikimedia Foundation, 2024, 2024-08-14 [cit. 2026-09-17]. Dostupné z: https://en.wikipedia.org/wiki/Total_cost_of_ownership
> - **Vendor Lock-in:** Stav závislosti zákazníka na konkrétním dodavateli produktů nebo služeb, kdy je přechod k jiné platformě spojen s neúměrně vysokými finančními i časovými náklady.

<details>
<summary> :bulb: Tip k úvaze o TCO: </summary>
<p>Když za 7 let odejde custom deska z Varianty 1 a původní vývojář již ve firmě nepracuje a čip se nevyrábí, musí firma vyvinout celou řídicí elektroniku znovu od nuly. Hodina odstávky automobilové linky přitom stojí desítky až stovky tisíc korun.</p>
</details>

:star2: **Bonusová otázka k úloze 6:**
Co znamená pojem **MTBF (Mean Time Between Failures)** v datasheetech průmyslových řídicích jednotek a jaký vliv má okolní teplota v rozváděči na tuto hodnotu (tzv. Arrheniovo pravidlo)?

*Vaše odpověď:*
**MTBF** (Mean Time Between Failures) je střední doba mezi poruchami v hodinách – **statistika velkého souboru, ne životnost jednoho kusu**. MTBF 1 000 000 h neznamená, že PLC vydrží 114 let, ale že z velkého souboru ročně selže cca 8 760 / 1 000 000 ≈ 0,9 % kusů. Počítá se dle SN 29500, MIL-HDBK-217F nebo Telcordia, vždy pro určitou teplotu (často 40 °C).

**Arrheniovo pravidlo:** rychlost chemického stárnutí součástek (hlavně elektrolytických kondenzátorů) roste s teplotou exponenciálně – prakticky **+10 °C ≈ poloviční životnost** (40 °C = 100 %, 50 °C = 50 %, 60 °C = 25 %). Proto se rozváděče chladí a hlídá se v nich teplota.
