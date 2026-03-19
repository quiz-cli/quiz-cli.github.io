# Otázky, issues a týmová spolupráce

**Datum:** 2026-03-12  
**Lektor:** David Slavíček  
**Zápis:** Pavlína Váňová

---

Dnešní sraz byl kratší než obvykle. Zaměřili jsme se hlavně na otázky a odpovědi k aktuálním issues a celkovému fungování týmové spolupráce na projektu. Na závěr jsme se přesunuli na NePyvo, kde měl Luděk Reif velmi zajímavou přednášku o vibecodingu.

---

## Pull requesty a navrhování změn v kódu

Prošli jsme si, jak se navrhují změny v kódu přímo na GitHubu:

- kliknout na `+` u čísla řádku
- zvolit **Add a comment on line**

---

## Issue #4 – Admin receives a question

Dále jsme si prošli issue, kde admin přijímá otázku:

- do projektu byla přidána knihovna `string` (konkrétně `ascii_letters`) – tato úprava byla převzata a upravena z klienta
- funkce je společná pro klienta i admina, logicky by tedy patřila do repozitáře **commons**
- commons ale zatím obsahuje pouze modely – David navrhuje přidat složku `Functions` (možná jen dočasně), aby se pull request dál neprotahoval

---

## Repozitář Commons

Krátce jsme rozebrali repozitář **commons**.

V souboru `models.py` na řádku 54 (parametr `question`) byla nalezena chybná specifikace typu `dict`. David navrhuje opravu typu – lze ji zadat přímo jako **commit suggestion** v rámci code review.

---

## Kategorizace návrhů při code review

David představil systém, který používá v práci při posuzování návrhů podle závažnosti:

- **Issue** – vážný problém, který je nutné vyřešit
- **Suggestion** – pouze návrh, není povinný
- **Nitpick** – drobný detail, který stojí za zmínku, ale není důležitý

---

## `app.state` ve FastAPI

Padl dotaz, co vlastně je `app.state` ve FastAPI. Téma by mělo být dovysvětleno příště.

---

## Jak se vyhnout merge konfliktům

Prošli jsme si projektovou tabulku (Quiz CLI issues table) a zamýšleli se nad tím, kdy by mělo issue přejít ze stavu **New/Idea** do stavu **Todo**.

- procházíme issues společně, konečné rozhodnutí je na Martinovi jako správci projektu
- issue ve stavu **Todo** si může "přivlastnit" kdokoli a začít na něm pracovat

---

## Víceodpověďové otázky a bodování

Tým se shodl, že je nejprve potřeba rozhodnout o pravidlech, a teprve poté implementovat:

- jakým způsobem se budou počítat body při více správných odpovědích
- jak se budou zaznamenávat otázky s více možnými odpověďmi

Zazněla také základní otázka k povaze aplikace:

> **Je to hra, nebo test?**

- **Hra** – zaznamenává počet bodů a podle toho pořadí hráčů (srovnání: Kahoot)
- **Test** – zaznamenává, kdo na co odpověděl správně nebo špatně, a poskytuje zpětnou vazbu učiteli i studentům
