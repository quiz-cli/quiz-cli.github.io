2026-02-19

**Lektor:**  
Martin Zelený

**Zápis:**  
Patricie Hermanová

---

Třetí sraz začal kontrolou naší nástěnky a krátkým ohlédnutím za tím, co se od minule změnilo. Super byl moment, kdy jsme si ukázali náš Quiz CLI blog — konečně běží. Po všech bojích s MkDocs, větvemi a GitHub Pages to byl malý, ale důležitý milník. Už to celé není jen cvičení, ale skutečný projekt, který začal veřejně existovat.

---

## Issue, PR, nástěnka a proč na pořadí záleží

Martin se krátce vrátil k tomu, jak správně vytvářet změny v projektu.

Správný postup je:

1. vytvořit **issue**
2. vytvořit si **branch**
3. udělat změny
4. otevřít **pull request**

Ne naopak.

Tohle byla přesně chyba, kterou jsem udělala u svého „sync fix“ PR — šla jsem rovnou na pull request bez issue. Navíc jsem se pokoušela změnit zdroj pravdy v mainu na GitHubu, velmi dobré poučení.

Mezitím se na nástěnce objevily dvě nové kolonky:

- **Ideas** – místo pro nápady, které ještě nejsou připravené na realizaci  
- **In review** – mezistav mezi „hotovo“ a „merge do main“

Tohle dává mnohem větší smysl. Hotovo totiž neznamená automaticky začleněno.

---

## Merge už není magie

Doteď pro mě byl merge něco, co dělal Martin, nebo kdokoliv jiný. Teď jsme si ale vysvětlili, že merge budeme dělat samy. U blogu to bylo tedy výjimečné, protože bylo potřeba ho rychle dostat online a ověřit, že funguje.

Martin nám ukázal dva typy merge:

**Squash and merge**

- Používá se, když commity patří k sobě. Sloučí je do jednoho. Například:
fix blog formatting + fix typo in blog → vznikne jeden commit.

**Rebase and merge**

- Používá se, když commity mají vlastní význam. Zachovají se oba. Tohle je důležité pro čitelnost historie projektu.

---

## Conventional commits: když commit něco říká

Další věc, kterou jsme si ukazovali, jsou tzv. conventional commits.

Například:
- chore: remove unused library
- docs: improve README formatting


Prefix říká, o jaký typ změny jde. Nejde jen o pořádek. Jde o komunikaci. Když se někdo podívá do historie, okamžitě ví, co se změnilo.

---

## Větve se po merge mažou

Po úspěšném merge je dobrá praxe:

- smazat branch na GitHubu
- smazat branch lokálně

Repozitář tak zůstává přehledný.

Ukázali jsme si i užitečné příkazy, některé známé, jiné nové:

```bash
git branch
git branch -vva
git remote -vv
git fetch --prune
git status
git pull
git log
```

---

## Ideas opravdu fungují

Nový sloupec Ideas byl hned vyzkoušen v praxi. Nápad se vytvořil jako issue, prošel procesem a nakonec skončil jako Done. Je zajímavé sledovat, jak se z pouhé myšlenky stává konkrétní změna v projektu.

---

## Host: Karolína a její povídní o RoboProjektu

Karolína nám představila RoboProjekt, který je inspirací pro naše hraní si na práci. Jde původně o deskovou hrou, tu před pár lety s dalšími účastnicemi Pyladies kurzů převedly do programu.

Jejich projekt, narozdíl od našeho, měl grafické rozhraní vytvořené v Inkscape a mapy uložené v JSON souborech. Pracovaly i trochu jinak než my — používaly forky, ne jeden společný repozitář. Navíc začínaly úplně od nuly, my pracujeme už s hrubou kostrou projektu.

Nejdůležitější skill, který si odnesly?

**Git.**

A taky schopnost:

- číst cizí kód
- přijímat zpětnou vazbu
- ptát se

Karolína zdůraznila jednu důležitou věc:

Je normální nerozumět.  
Důležité je umět se ptát.

Nakonec zůstaly na projektu dvě účastnice. Dnes spolu pracují v Red Hatu.

---

## Gitová historie jako příběh

Další důležitá myšlenka – commity by měly tvořit smysluplný příběh.

- NE: „Udělala jsem tisíc věcí najednou.“
- ANO: jedna změna = jeden commit

Projekt by měl být v každém bodě funkční. To je profesionální přístup.


---

## Závěrem ukázky a nápady

Ukazovali jsme si zajímavé issue, které nám visí na nástěnce. Pydantic automaticky převádí čísla na integer, ale náš kód očekával string. Výsledkem byla chyba. Řešením by mohlo být třeba přetypování, úprava podmínky nebo použití JSON schema.

Důležitá poznámka – program by neměl spoléhat na to, že uživatel udělá vše přesně správně a také by měl být otevřený budoucím změnám.

---

Quiz je definovaný v YAML souboru. Do budoucna tedy může obsahovat další položky, například:

- ID otázky
- bodování
- timer
- typ otázky

---

Projekt začíná být skutečný. Třetí sraz byl zlomový. Git přestává být nepřítel.
