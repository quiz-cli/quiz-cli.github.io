# Jedenáctý sraz

**Datum:** 2026-04-23  
**Lektor:** Martin Zelený  
**Zápis:** Hana Štamberková

---

Desátý sraz začal pozvánkou na jednodenní kurz Micropythonu. Díky tomu nám rovnou Martin ukázal jak vypadá pull request od Borise, když chce přidat právě tento nový kruz na stránky Pyladies.
Potom jsme se podívali na pár issue, které jsou aktuálně otevřené.

V průběhu kurzu nám Martin připoměl pár užitečných příkazů v gitu a také zdůraznil, že když někdo zapíše nové issue, není nutné, že ho musí také dělat a když někdo pracuje na issue a zjistí,
že na něm již nechce pracovat, tak například může sepsat na co zatím přišel a předat issue někomu dalšímu.

---

## Issue #10 - Server tries send message about player's disconnection when admin connection is closed
- bug se projevuje tak, že server spadne, když se zavře adminovo sojení během běžící hry
- máme stavovou proměnou (flag), která říká, jestli kvíz běží - True během hry, False po ukončení
- informace o tom, jestli se hráč odpojil se odesílá pouze, když kvíz běží
- informace o tom, zda se hráč připojil/odpojil se tisknou přímo do okna admina (možná časem rozodneme,zda tyto informace nebudeme ukládat do souboru)
- Martin prošel Ninin Pull Request od Niny, spustil testy, které prošly, PR byl schválen

## Issue #3 Correct answer 
- přesun metody correct answer z klienta na server


## Issue #4 - responze sanitization 
- Client má na server odeslat normalizovaný řetězec. Všechny přebytečné symboly (mezery, interpunkční znaménka) by měly být odstraněny, písmena by měla být zmenšena.
- na tom pracuje Jana
- tento úkol je komplexní, asi bude lepší řešit v několika krocíc, není potřeba řešit v jednom kroku
- budeme rozdělovat úkol do více menší issues?
- Martin navrhl možnost zavést class Message - ta zasáhne do všech repozitářů
- Nina udělá issue pro rozdělení tasku (přepis, Message class)

## Issue #15 - Use Message for all..
- navazuje přímo na Issue #4 - cílem je centralizovat práci se zprávami do třídy Message
- změna se dotkne client / server / admin / commons

## Issue #5 Refactoring 
- jedná se o čistý refactoring bez změny chování - není potřeba na něj psát testy, pouze je potřeba, aby testy prošlo

## Nová issue, která je potřeba vytvořit
- je potřeba issue, které se postará, aby každý účastník dostal po skončení kvízu právě své výsledky testu
- class Results - aktuálně je to slovník, lépe plochá struktura, například seznam slovníků, který si bude zapisovat do seznamu hráče a otázku a ty budou obsahovat slovníky výsledků - díky tomu lze snadno vyfiltrovat výsledky jednotlivých hráčů pomocí list comprihension a poslat je jednotlivým hráčům

alice  0  [True,   False,  False,  False] <br>
bob    0  [False,  True,   True,   True] <br>
bob    1  [False,  False,  True,   True]  <br>
alice  0  [True,   False,  False,  False]  <br>
alice  2  [False,  True,   False,  False]  <br>
bob    3  [False,  True,   True,   False]  <br>

- Issue: Chceme po konci kvizu reportovat vysledky klientum (kazdy klient dostane pouze sve vysledky). Nyni admin dostane po konci kvizu vse.
class Option(BaseModel):
    """Single answer option for a question.

    {"answer": "Paris", "correct": true}
    {"answer": 22, "correct": True} --> {"answer": "22", "correct": true}

    option["answer"] --> option.answer

    """

- je potřeba rozlišit hráče se stejným jménem - budou dostávat error message, že jméno je obsazené?
- v budoucnu také žebříček výsledků
- Issue: deduplikovat funkci print_question a umistit do quiz-common
- Issue: test na vyhodnoceni vysledku - admin aktualne dostava na konci report s vysledky a my ho porovname s ocekavanym vysledkem
- Potom refaktor na tridu Message zmena vyhodnocovani vysledku: https://github.com/quiz-cli/quiz-client/issues/4#issuecomment-4246852287

Uz bude test, na vyhodnoceni vysledku, tak je refaktor usnadnen.
GitHub
Response sanitization · Issue #4 · quiz-cli/quiz-client
Client should send clean string to the server. All extra symbols (spaces, punctuation signs) should be removed, letters lowered.

## Nový Issue status - queue
- status queue slouží pro issue, které ještě nemůže být zpracováno, protože čeká ve frontě na dokončení jiného issue


## Připomenutí Git příkazů 

`git reset -- h` - tvrdý reset hlavní větve z větve na gitu

`git restore nazev_souboru` - lokálně upravený soubor vrátí na verzi ze serveru

`git fetch --prune` - přidá nové commity a branche ze serveru, řípadně aktualizuje existující, pokud commitnutá branch byla smazaná na serveru, smaže ji i na lokalu


## Poznámky:
- neplacený Codex lze dát do VS Code
- Martin se bude ptát co dělá pull-request, nemělo by sklouznout do vibe-codingu, kdy nevíme, co kód dělá


