# Dvacátý první sraz

2026-10-08

**Lektor:**  
Martin Zelený

**Zápis:**  
Dagmar Vodáková

---  

Na dalším srazu jsme se věnovali sjednocení GitHub Actions, což je momentálně prioritní Issue. 

Velkou část setkání jsme strávili diskusí o návrhu a refaktoringu kódu. Domluvili jsme se, že před tím ještě přidáme poslední featury a dokončíme tak rozdělaná Issues: [Issue #23 Count of correct answers per user](https://github.com/quiz-cli/quiz-server/issues/23) a [Issue #36 Support for showing right answers after each question](https://github.com/quiz-cli/quiz-server/issues/36). 

Ujasnili jsme si práci s testy a správu větví.

---

## GitHub Actions

Olga dostala velikou pochvalu za dokončení [Issue #55 GitHub action unification](https://github.com/quiz-cli/quiz-cli.github.io/issues/55), zaměřeného na sjednocení GitHub Actions do společného repozitáře [`.github`](https://github.com/quiz-cli/.github), který slouží jako globální repozitář projektu. Vysvětlila nám, jak automatizované akce fungují. Navíc si vzala na starost další související úkol: [Issue #58 Linter (ruff) config unification](https://github.com/quiz-cli/quiz-cli.github.io/issues/58), doplnění kontroly pomocí `pytest` do workflow jobs. Cílem je, aby se automaticky spouštěly unit testy napříč všemi repozitáři odpovídajícími názvu aktuální branche. Bude potřeba promyslet a otestovat práci s proměnnými ve workflow, například pro předávání názvu branche mezi jednotlivými kroky.

V rámci kontroly posledních běhů Actions jsme si všimli také upozornění na novější verze používaných akcí. Aktuálně používáme například `ruff` ve verzi `v3`, kterou bychom měli aktualizovat na `v4` a následně ověřit, že vše funguje správně. To bude další úkol k vyřešení.

Protože Olga nové GitHub Actions sloučila do hlavní větve, u již vytvořených PR je potřeba znovu spustit workflow, aby se změny správně ověřily.

## Testy

Jana doplnila testy k [Issue #16 Handle duplicate player names](https://github.com/quiz-cli/quiz-server/issues/16).
Martin její práci zkontroloval, otestoval kód lokálně na serveru a schválil příslušné PR. Testy byly následně sloučeny do hlavní větve.

**Unit testy** nebudeme automaticky přidávat ke každé drobné funkci. Zaměříme se především na složitější funkce, u kterých přinesou skutečnou hodnotu a pomohou nám zachytit případné chyby.

## Git: rebase a úklid větví

Připomněli jsme si několik důležitých pravidel pro práci s Gitem.

- Po sloučení PR vždy smažeme příslušnou větev. Pomáhá nám to udržovat repozitáře přehledné.
- Pokud máme rozpracovanou větev založenou na starší verzi `main`, měli bychom ji aktualizovat pomocí rebase.
- Po změnách v hlavní větvi je důležité ověřit, že naše rozpracovaná práce stále vychází z aktuálního základu.

Základní postup pro aktualizaci vlastní větve:

```
git switch main
git pull
git branch -vv
git switch nazev-vetve
git rebase origin/main
git push --force
```

Příkaz `git branch -vv` nám pomůže zkontrolovat lokální větve a jejich návaznost na vzdálené větve. Po rebase je potřeba aktualizovat vzdálenou větev pomocí `git push --force`. Tento příkaz používáme pouze u vlastní rozpracované větve, kde víme, že nepřepisujeme práci ostatních.

## Diskuse o návrhu odpovědí a budoucím refaktoringu

Martin upozornil na problém v současném návrhu funkce `check_answers`. Nelíbí se mu současný způsob předávání písmen odpovědí.

Potřebujeme pro to vytvořit issue a následně navrhnout refaktoring, ve kterém se budou výsledky odpovědí reprezentovány seznamem čtyř hodnot `True` a `False`, tedy informací o správnosti každé odpovědi.

Tato část setkání se nakonec proměnila v delší diskusi o možných řešeních. Probírali jsme, jak nám může pomoci AI při návrhu, a řešili jsme také potřebu vhodné datové struktury, se kterou bude možné výsledky dále měnit a zpracovávat. Ve hře je seznam, slovník nebo vlastní objekt.

## Co nás čeká dál?

Nejprve potřebujeme zkontrolovat a sloučit poslední připravené feature PR. Poté nás čeká společná diskuse o architektuře projektu a větší refaktoring kódu.

Cílem bude sjednotit návrh jednotlivých částí aplikace tak, aby se nám projekt dobře rozšiřoval a udržoval.

## Pozvánka na další workshopy

Martin nás upozornil na plánované workshopy zaměřené na SQL a Git, které budou příležitostí procvičit si základní práci s databází a pokročilejší práci s verzovacím systémem.
