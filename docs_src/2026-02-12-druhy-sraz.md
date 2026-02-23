2026-02-12

**Lektor:**  
Martin Zelený

**Zápis:**  
Patricie Hermanová

---

Na druhém srazu jsme plynule navázali tam, kde jsme minule skončili. Zatímco první setkání bylo hlavně o seznámení s projektem a jeho strukturou, tentokrát jsme se začali více nořit do reálného workflow, práce s repozitářem a samotného kódu.

Postupně se začal odkrývat celý mechanismus fungování projektu – od GitHub issues, přes YAML strukturu kvízu, až po první kontakt s knihovnou Pydantic a asynchronní komunikací.

---

## Ohlédnutí za domácí přípravou a plán do budoucna

Na začátku jsme si shrnuli domácí přípravu, kterou Martin sdílel. Tématem bylo především objektově orientované programování (OOP), které tvoří základ struktury našeho projektu.

Zároveň jsme dostali nástin toho, co nás čeká dál. Klíčovou roli bude hrát knihovna **Pydantic**, která slouží k validaci dat a jejich převodu do objektové struktury. Právě díky ní bude možné bezpečně načítat a kontrolovat data kvízu.

---

## GitHub Projects a práce s issues

Další část setkání byla věnována organizaci práce na GitHubu. Prošli jsme projektovou tabulku s úkoly, kde se ukázalo, že přehled ve formě tabulky je výrazně praktičtější než základní seznam.

Byly udělena pochvala za návrh Issue od účastnice – přidání sloupce „Ideas“, který slouží jako vstupní bod pro nové nápady ještě před jejich zpracováním do konkrétního úkolu.

Ukázalo se také, že mezi stavy „In progress“ a „Done“ dává smysl mít ještě mezistav. Dokončený úkol totiž nemusí být automaticky schválený a mergnutý. Tento krok je důležitý pro zachování kvality a kontroly nad změnami.

Postupně jsme prošli jednotlivé úkoly, zkontrolovali jejich přiřazení a pojmenování, a ujistili se, že má každý jasno, na čem pracuje nebo by pracovat mohl.

---

## Git v praxi: branche, merge, squash a rebase

Velmi cenná byla praktická ukázka práce s Git workflow na konkrétních příkladech.

Ukázali jsme si, co znamená:

- vytvoření vlastní branche pro změny,
- vytvoření Pull Requestu,
- squashnutí commitů pro čistší historii,
- merge změn do hlavní větve,
- a následné smazání již nepotřebné branche (jak na GitHubu, tak lokálně).

Důraz byl kladen také na správné pojmenování větví, ideálně včetně vlastních iniciál, aby bylo vždy jasné, kdo je autorem změny.

Narazili jsme i na situaci, kdy bylo potřeba použít **rebase**, protože změny spolu logicky nesouvisely. I to je součást reálné práce na projektu.

---

## YAML jako formát pro definici kvízu

Poprvé jsme se detailně podívali na strukturu samotného kvízu, který je uložen ve formátu YAML.

YAML je jednoduchý textový formát založený na dvojicích klíč–hodnota. Díky své čitelnosti je ideální pro definici strukturovaných dat, jako jsou otázky, odpovědi nebo metadata kvízu.

Ukázali jsme si například:

- jak YAML reprezentuje data jako slovník,
- proč je důležité dodržovat správnou strukturu,
- a jaké chyby mohou vzniknout například při nesprávném použití dvojtečky.

Do budoucna se počítá s rozšířením o různé typy otázek, například single choice nebo multiple choice.

---

## Jak se kvíz načítá: od souboru k objektu

Velmi zajímavý byl pohled na to, jak se data ze souboru skutečně dostanou do aplikace.

Nejprve se YAML soubor načte a převede na Python slovník. Ten se následně předá do Pydantic modelu:

```python
Quiz(**quiz_data)
```

Operátor `**` zde rozbalí slovník na jednotlivé argumenty. Pydantic pak:

- zkontroluje správnost dat,
- převede je do objektu,
- a zajistí, že mají správnou strukturu.

Výsledkem je plnohodnotný objekt reprezentující celý kvíz.

# Jak se aplikace spouští

Ukázali jsme si také, jak se projekt spouští pomocí skriptů definovaných v souboru `pyproject.toml`.

Tento soubor obsahuje metadata o projektu a mimo jiné definuje tzv. entry point:

```toml
[project.scripts]
quiz-admin = "quiz_admin.__main__:main"
```

Díky tomu lze aplikaci spustit přímo z příkazové řádky bez nutnosti ručního spouštění jednotlivých souborů.

Důležitou roli zde hraje nástroj `uv`, který se stará o správu prostředí a instalaci závislostí.

# První setkání s asynchronním kódem

Na závěr jsme se dostali k jedné z nejpokročilejších částí projektu – asynchronní komunikaci.

Server a klient spolu komunikují pomocí WebSocketů. To umožňuje obousměrnou komunikaci v reálném čase.

Asynchronní funkce jsou definovány pomocí:

```python
async def
```
a volají se pomocí:

```python
await
```

To umožňuje programu obsluhovat více úloh současně, aniž by se navzájem blokovaly.

Například odeslání dat kvízu serveru může vypadat takto:

```python
await ws.send(json.dumps(quiz_data))
```
# Kam směřujeme dál

Druhý sraz byl významným krokem od teorie k praxi. Začali jsme chápat nejen strukturu projektu, ale i principy, na kterých stojí.

Postupně se skládá obraz celé aplikace – od YAML souboru přes validaci dat až po komunikaci mezi klientem a serverem.