# Dvanáctý sraz: Když projekt začne být opravdu týmový

**Datum:** 14. května 2026  
**Lektor:** Martin Zelený  
**Zápis:** Patricie Hermanová  

---

Dvanáctý sraz byl hodně o komunikaci mezi repozitáři, pull requestech a o tom, co se začne dít, když na projektu pracuje více lidí najednou.

Poprvé jsme začali opravdu narážet na to, že změna v jedné části systému může ovlivnit několik dalších repozitářů. A že orientace v projektu už není jen o vlastním kódu.

---

## Jak schovat správnou odpověď před klientem

Na začátku jsme řešili issue od Jany:

- https://github.com/quiz-cli/quiz-client/issues/9

Martin nám ukazoval související pull request:

- https://github.com/quiz-cli/quiz-common/pull/8/changes

Nakonec jsme ale zůstali u Janiny verze:

- https://github.com/quiz-cli/quiz-common/pull/7

Řešilo se hlavně to, že klient by neměl dopředu vidět, která odpověď je správná.

V modelu tedy původně existovalo:

```python
"correct": self.correct
```

Jana navrhla změnu:
```python
"correct": False
```
Tím by se správnost odpovědi při serializaci schovala.

Martin pak zmiňoval, že by šlo elegantněji upravit samotnou serializaci přes Pydantic a model_dump().

---

## Pydantic a serializace objektů

Poprvé jsme trochu víc narazili na to, co vlastně Pydantic dělá.

model_dump() převádí objekt na slovník, který se potom odesílá jako JSON.

Tedy například:
```python
quiz_question -> dict -> JSON -> websocket -> klient
```

Padla i důležitá poznámka:

Každá otázka musí mít alespoň jednu odpověď.

Tohle je přesně typ věci, kterou by měl model validovat.
---
## Proč máme tolik repozitářů

Jana se ještě ptala na uv tool install --editable, protože při lokálním vývoji musela použít právě tento příkaz.

To odstartovalo větší debatu o celé architektuře projektu.

Martin vysvětloval, že když Quiz CLI navrhoval, začal klasicky:

- klient
- server

Jenže postupně se ukázalo, že některé části je potřeba sdílet. A tak vznikly další repozitáře.

Dnes máme například:

- client
- server
- common
- tests
- admin
- blog

Opakem tohoto přístupu je tzv. monorepo, kde je všechno v jednom repozitáři.

Výhoda více repozitářů:

- lepší oddělení odpovědností

Nevýhoda:

- změna často znamená upravit více repo najednou

A přesně to jsme začali cítit i my.

---
## I mentor se někdy ztrácí

Postupně jsme narazili na zajímavý moment.

V projektu už začíná být těžší orientace:

- hodně PR
- hodně branchí
- více repozitářů
- různé závislosti

Martin nás uklidňoval, že je normální se v tom občas ztratit.

A upřímně říkal, že někdy nestíhá sledovat, co je v jakém stavu ani on sám.

To bylo docela uklidňující.

V praxi se podobné věci řeší:

- denní komunikací
- standupy
- sprinty
- ticket systémem
- project managerem nebo scrum masterem

---
## HTTPS a bezpečnost

Krátce jsme narazili i na bezpečnost serveru.

Jedno z možných řešení je použití HTTPS, aby komunikace nebyla posílaná otevřeně přes síť.

Zatím je to pro nás spíš téma do budoucna, ale je dobré vědět, že podobné věci existují a řeší se.

---

## Blog už funguje správně

Řešili jsme také poslední blogový zápis.

Martin připomínal důležitou věc:

PR musí být správně propojené s issue.

Díky tomu se změny automaticky propisují do nástěnky projektu.

Ukazovali jsme si i aktualizovaný index.md, díky kterému se články správně načítají v navigaci blogu.

Po všech předchozích bojích s MkDocs a GitHub Pages už to konečně začíná fungovat stabilně.

---
## Testování Dášina PR

Potom jsme přešli na testování Dašiny změny:

- [https://github.com/quiz-cli/server issue #22](https://github.com/quiz-cli/quiz-server/issues/22)
- [https://github.com/quiz-client issue #10](https://github.com/quiz-cli/quiz-client/issues/10)

Funkce zobrazovala hráčům jejich výsledky po dokončení quizu.

Martin při tom ukazoval několik praktických věcí:

- změna branche v jednom terminálu se projeví i v druhém
- uv run automaticky použije správné virtuální prostředí

Také jsme si vysvětlili rozdíl:
```python
uv sync
```
- nastaví prostředí podle uv.lock
```python
uv update
```
- aktualizuje závislosti

---
## Když něco nefunguje… a pak najednou ano

Nejdřív to Martinovi vůbec nefungovalo.

Daša i Nina přitom říkaly, že jim změna funguje správně.

Nakonec se ukázalo, že měl přepnutou špatnou branch.

Po opravě už oba klienti dostali správně své personalizované výsledky.

Velmi realistická ukázka programování.

---
## Async coroutine a posílání zpráv

Pak jsme šli přímo do kódu.

Objevila se nová async coroutine, která rozesílala hráčům jejich výsledky.

Martin vysvětloval, že nejde o klasickou funkci, ale coroutine pro síťovou komunikaci, která běží neblokujícím způsobem, program tedy mezitím může dělat i jiné věci.

---
## Dvě hvězdičky a rozbalování slovníků

Narazili jsme i na známé:
```python
**dictionary
```
To rozbalí slovník na jednotlivé klíče a hodnoty.

Postupně začínám chápat, že podobné zápisy nejsou magie. Jen zkratky pro něco, co by šlo napsat i delším způsobem.

Type hints a proč jsou někdy názvy v uvozovkách

Martin ukazoval situaci, kdy byl typ napsaný jako string:
```python
"Results"
```
Kdyby tam uvozovky nebyly, Python by spadl, protože daný typ ještě v tu chvíli neexistuje.

Type checker ale pochopí, že jde o budoucí typ.

Tohle byl pro mě hodně zajímavý detail.

---
## Testy musí běžet

Martin pak spouštěl testy:
```python
uv run pytest -vv
```
Parametr -vv znamená podrobnější výpis.

Kontrolovali jsme i nově přidané testy a všechno prošlo.

---
## GitHub Actions a automatické kontroly

Na závěr jsme řešili Nininu chybu v GitHub Actions.

Martin nám vysvětloval workflow:

- po otevření PR se automaticky spustí joby
- kontroluje se formátování
- typová kontrola
- kvalita kódu

Viděli jsme například ruff:
```yaml
args: "format --check --diff"
```
A také type-check.

Nina přidala vlastní úpravu s přepisem pyproject.toml.

Martin si ale myslí, že je to zbytečně komplikované řešení a že podobné věci by měly zůstat jen pro lokální vývoj.

---

## Projekt začíná připomínat reálnou práci

Čtvrtý sraz byl zatím asi nejvíc „produkční“.

Méně jednoduchého programování.
Více:

- komunikace mezi repozitáři
- závislostí
- code review
- testování
- workflow
- infrastruktury

A začíná být vidět, že programování není jen psaní kódu.

Je to hlavně práce s ostatními lidmi.
