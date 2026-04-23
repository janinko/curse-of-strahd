# Curse of Strahd — pokyny pro Claude

## Mapa dokumentů

| Soubor                          | Obsah                                                                                                                 |
| ------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `index.md`                      | Rozcestník: poslední zápisky + přehled úkolů (aktivní, probíhající, splněné)                                          |
| `Osoby a skupiny.md`            | Všechny postavy a skupiny (NPC), abecedně — vlastnosti, motivace, vztahy; hlavní reference pro cokoliv ohledně postav |
| `Hráčské postavy.md`            | Profily hráčských postav (Abukai, Aurelius, Malakai, Nethar, Rheya) — původ a zázemí                                  |
| `Strád von Zarovič.md`          | Dedikovaný profil Stráda — vzhled, pozorování ze setkání, zvěsti, rodina                                              |
| `Místa.md`                      | Přehled domén hrůzy a dalších míst ve světě; rozcestník pro ostatní soubory `Místa - *`                               |
| `Místa - Barovie.md`            | Lokace v Barovii (vesnice, Vallaki, Krezk, Ravenloft, vinařství, jezera…) — hlavní reference pro místa kampaně        |
| `Místa - Materiální pláň.md`    | Lokace mimo Barovii (Liamova tvrz, Bowshot…) — kde kampaň začala                                                      |
| `Místa - panství Dorstových.md` | Detailní popis panství Dorstových po místnostech                                                                      |
| `Časová osa.md`                 | Chronologický přehled dějin Barovie od 3. stol. do současnosti (rok ~735)                                             |
| `Zápisky/`                      | Zápisky ze sessions — narrativní tok kampaně, chronologicky                                                           |
| `Úkoly/`                        | Aktivní, probíhající a splněné questy s detaily a progress checklisty                                                 |
| `Události/`                     | Historické události ve světě (dobývání Barovie, útoky, slavnosti) — lore mimo sessions                                |
| `Texty/`                        | In-game texty nalezené ve světě: dopisy, deníky, smlouvy, legendy                                                     |

## Zápisky ze session

### Obecná zásada: zápisky = děj, dokumenty = fakta

Fakta (vlastnosti postav, popis lokací, zjištěné informace) patří do příslušných dokumentů (`Osoby a skupiny.md`, `Místa - Barovie.md` atd.). Zápisky (soubory ve složce `Zápisky`) zachycují **děj a narrativní tok** session — co se stalo a proč to bylo důležité. Překryv obou je v pořádku, ale zápisky by neměly být faktografickým výpisem.

### Struktura zápisků

- **První úroveň odrážek = scény** (nebo důležité podscény). Pište je jako úvod do scény, ne jako výčet faktů.
  - Příklad: *"Vydali jsme se k elfům, požádat Kazimíra, aby nám dělal průvodce"* — říká co, proč a nastavuje kontext.
- Sub-odrážky rozvádí klíčové momenty scény.
- Méně důležité scény dostanou méně prostoru — stačí jedna odrážka s odkazem.

### Co patří do zápisků

- Rozhodnutí skupiny a jejich kontext (i konflikty mezi postavami)
- Narrative beats — co se stalo, jaký to mělo dopad
- Atmosferické a flavor detaily (`Nethar učil havrana Krabana říkat slova`)
- Výsledky průzkumu/prozkoumání — jen pokud jsou narativně důležité; jinak stačí zmínka a detaily jdou do dokumentu lokace/postavy

### Co patří do dokumentů, ne zápisků

- Detailní popis lokací a jejich obsahu → `Místa - Barovie.md`
- Vlastnosti, motivace a vztahy postav → `Osoby a skupiny.md`
- Výsledky identifikace předmětů, magie, rituálů → příslušná sekce
- Výsledky průzkumu lokace → sekce té lokace v `Místa - Barovie.md`

### Styl

- Psáno v první osobě množného čísla (*"vydali jsme se"*, *"zastavili jsme se"*)
- Hráčské postavy tučně: **Malakai**, **Nethar**, **Rheya**, **Aurelius**
- Ostatní postavy a místa jako Obsidian odkazy: `[[Osoby a skupiny#Kazimir|Kazimír]]`
- Název souboru: číslo + výstižný název zachycující téma session (ne doslovný popis)
  - Minimálně 2 slova
  - Nesmí být tak obecné, aby sedělo na jakoukoliv session
  - Dobré je, pokud má náznak více významů: více věcí ze session, dva pohledy na totéž, slovní hříčka, nebo reference (na dřívější události v kampani, nebo popkulturní)
  - Příklady dobrých názvů z kampaně: *"A kurva, havran"*, *"In vino somnium"*, *"Smrtební hostina"*
