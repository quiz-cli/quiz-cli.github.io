# Osmnáctý sraz

**Datum:** 10.09.2026  
**Lektor:** Martin Zelený  
**Zápis:** Nina Belyavskaya

Holky se pomalu vracejí z prázdnin. Na srazu nás už bylo víc a také jsme přivítali novou účastnici Zuzku.

## Organizační voprosy. 

Domluvili jsme se, že na začátku každé schůzky si projdeme, kdo na čem pracuje. Zkontrolujeme seznam otevřených PR a buď je posuneme, nebo zavřeme s vysvětlením.

Dagy navrhla zavřít issue [Implement Unified Labeling System](https://github.com/quiz-cli/quiz-server/issues/18), protože je pro nás příliš komplikované, a souhlasili jsme s tím. 
Ale ještě nevíme, jak v [projektové tabulce](https://github.com/orgs/quiz-cli/projects/1/views/1) zviditelnit sloupec **Priority**.

Martin navrhl konkrétní **formát pro pojmenování branchí**, který by nám měl pomoct se orientovat a testovat:

```text
<initialy>_<cislo_feature>_<kratky_popis>
```

Například:

- `jd_6_print_method`  
- `mz_14_log_answers`  
- `nb_5_bug_github_actions`

Tahle konvence má dvě výhody:
1. Můžeme videt **kdo** a **co** na branchi dělá.
2. Stejně pojmenované branche z různých repozitářů, týkající se jednoho issue, bude možné využít v GitHub Actions při automatickém testování.

Probrali jsme otazku o **lohovaní**. 
Dagy navrhovala, že klient po každé otazce bude dostavat spravnou odpoved' a vlastný vysledek, a to bude u sebe ukladat v log.

Martin doplnil že spojení u klienta nebo admina se může zrušit. Proto ideální by bylo, kdyby se logy pravidelně psali na disk na serveru a klijenty s adminem měli vlastní logi a zachranili by tam asi něco.

Olga nabídla zeptát koučů PyLadies a udělat business analytiku.

Martin vytvořil issues pro **Github Actions**. Ted' máme stejné GA v každém repozitaře a musíme každý upravit když se něco změní. Napřiklad po vychodu nové verse **ruff** máme upravit `pyproject.toml`.  

Martin chce udělat testovaní pro repy v GA. Je to důležitý ukol, kdýž ho splním můžeme pokračovat s rozvojem dalších features atd.

## Připoměnutí

Na srazu se objevila nová učastnice Zuzka. Pro ní a pro my všichní Martin vysvětlil co děla náš projekt. Ukazal chod hry, řekl že my chceme ovladat modernímí způsobami vývoje softwaru. Napřiklad použivamé nastroje z realné praxi:

- **uv** – manager pro správu Python projektů a virtuálních prostředí.  
- **JSON** – formát, ve kterém kommunikuje server a klienty.  
- **Pydantic** – knihovna pro validaci a práci s datovými modely v Pythonu.
- **Github Actions** – nástroj pro CI/CD, může automaticky spustit testy a kontrolu kódu pro pull requesty.

## Tipy

Martin nám ukazal další užitečné věci

Github renderuje **mermaid schemy** z textu, můžeme použivat v ussues, review atd. 

Terminál umí něco mazat a měnit. Můžeme to mít jako stretch goal – například vylepšit výpis tak, aby na obrazovce nezůstávalo příliš mnoho zbytečných řádků.