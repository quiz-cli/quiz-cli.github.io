2026-02-05

**Lektor:**  
Martin Zelený

**Zápis:**  
Patricie Hermanová

---

V PyLadies se letos rozjel nový projekt s pracovním názvem **Quiz CLI**. Následujícího půl roku budeme v týmu vyvíjet kvízovou aplikaci, která poběží na serveru a bude fungovat přes síť – něco jako vlastní, programátorská alternativa ke Kahootu. Cílem není jen napsat kód, ale hlavně si vyzkoušet, jak vypadá práce na reálném projektu v týmu.

Hned na začátku jsme dostaly pozvánky do GitHub repozitářů a řešily klasický onboarding: založení účtů, instalace Gitu, SSH klíče a kontrolu, že všichni zvládneme projekt naklonovat a pushnout změny. Už tohle samo o sobě byla taková malá simulace nástupu do firmy.

Martin na úvod vysvětlil, o co vlastně půjde. Projekt má už delší dobu v hlavě – chtěl si vyzkoušet pokročilejší věci v Pythonu, hlavně FastAPI, asynchronní programování a síťovou komunikaci. Zároveň by z toho mohl vzniknout nástroj, který se jednou reálně použije třeba na výuku, protože Kahoot je prý pro lektory spíš utrpení než radost.

---

## Základní myšlenka kvízu

Základní myšlenka kvízu je vlastně jednoduchá:

> prezentace = hierarchický text, seznam otázek a odpovědí, řetězce a slovníky

To se hezky nabízí ukládat třeba ve formátu **YAML**. Jenže aby mohlo hrát víc lidí najednou, potřebujeme server, který poběží pořád, a klienty, kteří se k němu připojí. Komunikace mezi nimi má probíhat přes **websockety** – něco jako chat, kde spojení zůstává otevřené a zprávy tečou oběma směry v reálném čase.

Projekt už není úplně od nuly. Martin má připravený základ a my ho budeme postupně rozvíjet. Role si rozdělíme tak, aby to připomínalo „nastoupení do rozjetého projektu“.

---

## Architektura projektu

Celé je to rozdělené do několika repozitářů:

### Quiz Admin
Načítá kvíz z YAMLu, kontroluje ho, posílá otázky a vyhodnocuje odpovědi.  
Používá ho „učitel“.

### Quiz Server
Zajišťuje websocketové spojení mezi adminem a klienty.

### Quiz Client
To, co spouští hráči.

---

Nejdřív jsme si všechno naklonovaly, rozběhly server pomocí nástroje **uv** (takový švýcarský nožík ve světě Pythonu) a pak postupně i admina a klienta. Připojovaly jsme se zatím jen lokálně – vlastně samy na sebe.

A pak přišel ten hezký moment:  
na jednom terminálu běží server, na druhém admin, na třetím klient. V adminovi pošlu další otázku, na klientovi se objeví, odpovím… a na serveru vidím log, že to opravdu proteklo sítí. Malý wow efekt, když si člověk uvědomí, že se tam asynchronně děje víc věcí najednou.

---

## Ukázka z praxe

**Admin**
Send 'y' for the next question

**Client**
Question: This question has two correct answers: C and D
Answer: C

**Server**
Client papricie sent: {'answer': 'C'}


---

Fungovalo to skoro všem, jen jedné účastnici se komunikaci nepodařilo rozběhnout, takže celkově velký úspěch.

Do budoucna budeme pracovat i s dalším repozitářem **common**, kde jsou sdílené části kódu, a s knihovnami jako **Pydantic** na modely a validaci dat. Celý projekt je záměrně postavený trochu složitěji, než by bylo nutné – cílem je osahat si věci, které se v běžných tutoriálech moc neřeší: OOP, architekturu, verze, issues na GitHubu, týmovou spolupráci.

Na GitHubu už máme i projektovou tabulku s úkoly (TODO / In progress / Done), takže si opravdu hrajeme na „malý software tým“.

Zatím jsme hlavně rozběhly infrastrukturu. Teď už nás čeká ta zábavnější část: pochopit, jak to celé funguje uvnitř, a postupně z toho udělat skutečný kvíz.

