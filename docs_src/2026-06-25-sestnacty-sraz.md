# Šestnáctý sraz: Předprázdninový - typy kvízových otázek, CI a úklid modelů

**Datum:** 25. června 2026  
**Lektor:** Martin Zelený  
**Zápis:** Pavlína Váňová

---

Sraz jsme věnovali Martinovým návrhům issues na prázdninovou práci - co by bylo potřeba přes léto dodělat a na čem se dá dále pracovat.

---

## Více typů otázek

Chceme podporovat víc typů otázek a k tomu je potřeba oddělit **Pydantic modely** pro single-choice a multi-choice. Zatím se odpověď odesílá na server hned; u multi-choice bude potřeba počkat, než hráč dokončí výběr. Přibýt má i **ordering question** - otázka na správné pořadí.

---

## Sjednocení GitHub Actions

Před implementací kódu běží akce, která kontroluje **type check**, **ruff** a základní linter (jestli v kódu není něco podezřelého). Teď je ale rozkopírovaná do všech repozitářů - lepší by bylo mít globální „shromaždiště" GitHub Actions, nejspíš samostatné repo. Jak přesně to udělat, je potřeba nastudovat.

---

## Continuous Integration (CI): spuštění pytestu v GitHub Actions

Navazuje spuštění **pytestu** přímo v CI. Když issue zasahuje do víc repozitářů, je potřeba pojmenovat svoji větev ve všech repech stejně - CI si pak tyto větve stáhne ze všech míst. Pokud větev někde chybí (třeba na serveru), vezme si místo ní `main`. Důležité je pořadí: nejdřív pushnout všechny větve a teprve pak otevřít pull request.

---

## Vyřešený bug s neodpojováním klientů

Janča D. rozlouskla minulý záhadný bug, kdy se klienti neodpojovali - řešením přes metodu `copy`. Při testování cizí větve se hodí `git fetch`: díky němu se váš git dozví, že existuje jiná větev, na kterou se pak můžete přepnout.

---

## Třída Message a oddělení vrstev

Měla by vzniknout třída **`Message`** (bude to Pydantic model). Server běží celý na **FastAPI**, takže nejčistší by bylo oddělit logické vrstvy - tzv. **hexagonal architecture** s porty a adaptéry. Core business logika by měla být oddělená od adaptérů, například přes třídu `Game`, která by sdružovala další třídy. Kámen úrazu může být `app.state`, kam se ukládá websocket (`app.state.admin = ws`).

---

## Úklid modelů

Martin nadhodil pár možností zjednodušení:

- **`class Player`** je teď BaseModel, ale Pydantic model tu moc nedává smysl. (U dat, která přijdou po síti, ale validaci přes Pydantic potřebujeme vždycky.)
- **`class Results`** je slovník; lepší by byl seznam, protože sem budeme ukládat log odpovědí, ze kterého pak snadno vygenerujeme výsledky.
- **`ClassVar`** (proměnná patřící třídě) se AI při revizi kódu moc nezamlouvala - mrknout na to, možná se jí zbavíme.

---

## Pozvánka na závěr

V létě se sice nebudeme scházet v učebně, ale čeká nás dvakrát grilovací **Pyvo**, tradičně poslední čtvrtek v červenci a srpnu.