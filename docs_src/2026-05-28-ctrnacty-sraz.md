# Čtrnáctý sraz: Jak dál se správou projektu, labely a serializace

**Datum:** 28. května 2026  
**Lektor:** Martin Zelený  
**Zápis:** Pavlína Váňová

---

Na dnešním srazu se řešila hlavně tato dvě témata: jak lépe organizovat projekt a jak správně serializovat data směrem ke klientovi.

---

## Organizační schůzka PyLadies

Setkání začalo pozvánkou na organizační schůzku PyLadies, která se koná příští týden. Na programu je plánování dalšího roku a otázky kolem výuky v době AI — má ještě smysl naše odevzdávátko?

---

## Správa projektu

Martin zmiňoval, že administrace projektu (přidávání tagů, přeskupování issues, child issues) začíná být nad jeho síly. V komerčních projektech tuhle úlohu pokrývají nástroje jako **Jira** nebo **Trello** a role jako **project manager** nebo **scrum master**. Někdo podobný by se hodil i nám - najde se dobrovolnice?

---

## PR #7 – schování správné odpovědi před klientem

Jana pracuje na [PR #7 – refactor: added print_question method](https://github.com/quiz-cli/quiz-common/pull/7). Řeší se, aby se při serializaci otázky hráčům nezobrazovalo pole `correct` se správnou hodnotou.

Janino řešení:

```python
"correct": False
```

Nina navrhla alternativní přístup přes Pydantic dekorátor `@field_serializer`, který řídí serializaci konkrétního pole. Martinovi se tento nápad líbí - správnost odpovědi se tu schová automaticky při převodu na JSON, bez ruční manipulace s hodnotou.

---

## PR #1 – CONTRIBUTING.md a labeling systém

Dáša přišla s hotovým pull requestem:

- [PR #1 – Add CONTRIBUTING.md with label guidelines and examples](https://github.com/quiz-cli/quiz-cli/pull/1)

Zavedla **unified labeling system** — sjednocené štítky pro issues napříč projektem, zdokumentované v repozitáři.

Padl nápad na label **„odloženo"** pro issues, které čekají na pozdější zpracování.

Řešila se i otázka child issues v jiných repozitářích — GitHub provázání zachová, ale je potřeba to mít na paměti.

**Martin přidal Dášu jako administrátorku projektu.**

---

## PR #10 – modely pro komunikaci server–hráči

Olga pracuje na [PR #10 – Models for server-players message flow](https://github.com/quiz-cli/quiz-server/pull/10). Cílem je definovat modely pro všechny typy zpráv mezi serverem a hráči.

Použila **Pydantic Type Adapter** pro validaci všech typů zpráv přes jeden vstupní bod. Použití je ukázáno v:

- repozitáři **server**: [Testing the new server-player message flow (#24)](https://github.com/quiz-cli/quiz-server/issues/24)
- repozitáři **client**: analogická ukázka pro klientskou stranu

Modely nebudou součástí produkčního kódu přímo — slouží jako **templát pro lokální testování**. Martin zvažuje zjednodušení; Nina navrhla pomocnou třídu „creator of message". Téma je otevřené.

---

## Rychlá kontrola PR

Pokud chce kdokoli rychle zkontrolovat otevřený PR, nejlepší bude ozvat se na **Discord** a přepnout stav issue na **„In review"** — ostatní pak hned vidí, co se děje.