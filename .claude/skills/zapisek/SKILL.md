---
name: zapisek
description: Zpracuje fotky ručně psaných poznámek z nové session Curse of Strahd do zápisku a navazujících dokumentů wiki. Použij, když uživatel dodá fotky poznámek, řekne "zápisek", "zpracuj poznámky ze session" nebo spustí /zapisek.
---

# Zápisek ze session z ručních poznámek

Poznámky jsou zkratkovité a většina kontextu je jen v hlavě uživatele. Proces je proto rozhovor, ne překlad: nejdřív ověřit čtení, pak vyzpovídat uživatele scénu po scéně až ke sdílenému porozumění, teprve potom psát. Pravidla obsahu a stylu jsou v `CLAUDE.md` (sekce *Zápisky ze session* a *Aktualizace dokumentů po session*); tento skill popisuje jen postup.

## Zásady platné v celém procesu

- **Nedomýšlet.** Cokoliv nejednoznačného (nečitelné slovo, zkratka, autorská poznámka typu „(Q: …)“, chybějící adresát, počet, místo odpočinku) se do souborů nezapisuje ani „opatrnou“ vlastní formulací. Zeptat se přesně na to slovo či frázi, s citací kontextu z poznámek.
- **Kandidát na odpověď jen ze zdroje.** Vlastní domněnku nenabízet jako „doporučenou“ možnost, aby uživatele nekotvila. Nabídnout kandidáta lze, když pochází z repozitáře (grep hit), a uvést, odkud je.
- **Odpověď uživatele platí doslova.** Nepřekládat ji zpět na nabídnuté možnosti a nedomýšlet její význam. Když je i odpověď nejasná, doptat se znovu.
- **Ne každá odpověď je materiál do zápisku.** Uživatel při vysvětlování zmíní i procedurální detaily; do zápisku jde jen to, co má narativní váhu.
- **Jen lokální soubory.** Žádný internet, žádné znalosti oficiálního modulu z trénovacích dat. Platí i pro subagenta.
- **Soubory se mohou měnit pod rukama.** Uživatel často edituje během práce. Před každou úpravou souboru ho znovu načíst a stavět na aktuálním stavu, nikdy nepřepisovat cizí změny.
- **Git nechat uživateli.** Skill nestaguje ani necommituje. Na konci jen vypíše změněné soubory.
- **Ostrá zpětná vazba („píšeš blbosti“) = stop.** Přestat psát a přejít na explicitní otázky ke každému spornému bodu, dokud není vyjasněn.

## Fáze 1: Vstup a přepis

1. Cesty k fotkám jsou v argumentech. Bez argumentů použít `~/Stažené/notes_*.jpg`; vypsat nalezené soubory a nechat uživatele potvrdit, než se čtou.
2. Přečíst všechny fotky a zjistit číslo nové session z `index.md` (poslední + 1).
3. Vypsat **doslovný přepis** celých poznámek:
   - řádek po řádku, v pořadí a členění originálu
   - nejistá čtení označit `???` přímo v textu, u každého uvést, co písmena naznačují, pokud něco naznačují
   - přeškrtnutý text zachovat jako přeškrtnutý, kresby a symboly popsat slovy v hranatých závorkách
   - **nic neinterpretovat**, ani zkratky, ani jména; zkomolené jméno zůstane zkomolené
4. Pod přepis napsat, kde poznámky končí (useknutý řádek, zda se zdá, že pokračují na další straně).
5. Počkat na opravy čtení. Uživatel odpovídá volným textem. Přepis opravit a pokračovat, až uživatel čtení potvrdí.

## Fáze 2: Rešerše v repozitáři

Spustit **jednoho** Explore subagenta až po potvrzení čtení. Dostane celý opravený přepis a pevně ohraničené zadání, aby neběžel hodinu:

- pro každé jméno, místo, předmět a nezvyklý pojem z přepisu: existuje v repu, nebo ne; pokud ano, soubor a sekce a jedna věta, co o něm repo říká
- z posledních dvou zápisků: aktuální herní datum, kde skupina je, otevřené nitky, které by poznámky mohly navazovat
- z `index.md`: aktivní úkoly, kterých se poznámky mohou týkat
- z `Úkoly/`: soubory, kterých se přepis dotýká, včetně deníkových úkolů postav (přípona 🧑🏻)
- z `Časová osa.md`: záznam aktuálního data a nejbližších dní
- jen grep a čtení výřezů, nikdy celé velké soubory; žádný internet, žádné znalosti oficiálního modulu; jedna zpráva s výsledkem

Souběžně sám přečíst poslední zápisek celý, kvůli návaznosti a tónu. Pokud přepis naznačuje zvláštní situaci (noc a hlídky, rituál, identifikace předmětů), otevřít jeden až dva starší zápisky s podobnou situací a převzít, jak jsou zapsané.

Výsledky rešerše slouží ke dvěma věcem: otázky, které repo zodpoví, se nepokládají, a kandidáti pro rozhovor mají zdroj.

## Fáze 3: Rozhovor scénu po scéně

Styl grill-me: vyptávat se, dokud není každá scéna srozumitelná natolik, aby se dala napsat bez domýšlení. Není limit na počet otázek celkem.

- Projít přepis v pořadí, scénu po scéně. Na jeden tah `AskUserQuestion` s 1 až 3 souvisejícími otázkami k jedné scéně.
- Když odpověď otevře další nejasnost, doptat se v dalším tahu, než se přejde k další scéně.
- Otázky formulovat konkrétně, s citací z poznámek: *„U řádku ‚S dal papíry‘: komu je dal?“*, ne *„Kdo dostal papíry?“*.
- Nabídnuté možnosti jen tam, kde mají zdroj (repo). Jinak otevřená otázka.

Typické díry v poznámkách, které je třeba aktivně hledat (seznam není a nemůže být úplný):

- jak scéna skončila, když poznámky končí uprostřed (boj, sázka, jednání)
- přesné počty (kolik nepřátel, kolik duchů), kdykoliv je v poznámkách plurál
- kdo co udělal a kdo co dostal; zkratky jedním písmenem (S, Z, N) a chybějící adresát
- co postavy přímo viděly či slyšely versus co si domyslely
- zda rozhovor s NPC byl vyptávání (otázka a odpověď), nebo souvislá řeč
- co je IC znalost postav a co OOC znalost hráčů
- co přesně se porovnává u slov „obojí“, „oba“, „stejné“, „různé“
- zda technická poznámka („3 třetiny“) je herní mechanika, nebo fakt do wiki
- kde a kdy skupina odpočívala; pokud noc, přesné rozdělení, co bylo před půlnocí a co po ní
- nová jména a jejich správný pravopis; zda je nová entita opravdu nová, nebo jde o zkomolené existující jméno
- nakreslené symboly a kdo si daný předmět vzal
- výsledky identifikace předmětů a kouzel
- herní datum a čas na konci session, a zda poznámky někde pokračují

## Fáze 4: Shrnutí a název

Po poslední scéně vypsat **shrnutí porozumění scénu po scéně**, plain text:

- co se stalo, s rozlišením přímo pozorovaného a domyšleného
- kdo má jaké předměty, kdo koho potkal, co se dozvěděli
- herní den každé scény (a rozdělení přes půlnoc, pokud nastalo)
- které fakty půjdou do kterého dokumentu

Zároveň nabídnout **3 až 5 názvů** zápisku podle pravidel v `CLAUDE.md`, s jednou větou, k čemu název odkazuje. Počkat na schválení shrnutí a volbu názvu. Opravy zapracovat do shrnutí a znovu potvrdit, pokud byly věcné.

## Fáze 5: Zápisek

Napsat jen `Zápisky/<číslo> <název>.md` podle `CLAUDE.md`. Zobrazit uživateli a počkat na OK nebo úpravy. Dál se pokračuje až po schválení, aby se případná chyba neroznesla do dalších souborů.

Před další fází zápisek znovu načíst z disku; uživatel ho mohl mezitím upravit.

## Fáze 6: Dokumenty

Rozdistribuovat fakta podle sekce *Aktualizace dokumentů po session* v `CLAUDE.md`. Pro každý fakt určit domovský dokument, každý soubor před úpravou znovu načíst. Sporné údaje proti dřívějším zápisům nahlásit, ne tiše sjednotit.

Na konci vypsat seznam změněných souborů s jednou větou, co v každém přibylo. Připomenout, že po ručních úpravách stačí říct **„prošel jsem to“** a spustí se poslední fáze.

## Fáze 7: Zpětná vazba z ručních úprav

Spouští se na pokyn uživatele po jeho úpravách zápisku.

1. Zobrazit `git diff` zápisku (případně porovnat s verzí, kterou skill zapsal) a projít rozdíly.
2. Věcné opravy významu (jiné entity, jiné počty, jiné umístění) promítnout do dotčených dokumentů.
3. Z úprav stylu a struktury vytáhnout ponaučení. Každé nabídnout jako jednořádkový návrh doplnění `CLAUDE.md` nebo úpravy tohoto skillu. Zapsat jen ta, která uživatel schválí.
