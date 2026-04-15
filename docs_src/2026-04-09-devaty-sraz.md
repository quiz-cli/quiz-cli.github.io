# Devátý sraz

**Datum:** 2026-04-09  
**Lektor:** Martin Zelený  
**Zápis:** Dragča Kvasničková

---

Dnešní sraz proběhl po 14-ti dnech kvůli velikonočním prázdninám. Vrátili jsme se k PR Patricie, lokálně jsme sbuildili `quiz-common` a otestovali její úpravy, PR byl schválen a uzavřen. Prošli jsme si další PR od Patricie a Niny. 

---

### Simulace bugu

Zreprodukovali jsme bug způsobující nesprávné načítání číselných odpovědí. Tento bug je popsaný v [Issue #2 Linux quiz YAML is not valid](https://github.com/quiz-cli/quiz-admin/issues/2) od Davida. 

V jednom terminálu jsme si spustili `quiz-server`, v druhém `quiz-admin` a načetli kvíz `linux_01`, kde poslední otázka obsahuje číselné odpovědi. YAML parser to naparsuje na `integer`, což neodpovídá modelu. Model očekává `string`, ale místo toho dostal `input value=21` (tedy integer), což vede k chybě.

Ale naše quiz_common knihovna byla spravená díky [PR #2](https://github.com/quiz-cli/quiz-common/pull/2) od Patricie a my si ji jdeme lokálně otestovat.

--- 

### Stažení opravené knihovny lokálně

Martin je v adresáři `quiz-common`, pomocí `git branch -vva`, zkontroloval, že má lokální větev napojenou na vzdálenou branch PR Patricie. Díky `git pull` stáhl lokálně změny ze vzdáleného repozitáře. Nakonec pomocí `git log` ověřil, že historie commitů odpovídá stavu větve na GitHub.

---

### Otestování opravené knihovy lokálně

- jsme stále v adresáři `quiz-common`, v branchi s opravenou knihovnou
- sbuildeni knihovny: `uv build`
- vidíme, že v quiz_common přibyl adresář `dist`, v něm jsou dva soubory- to jsou tzv. artefakty buildění, jeden z nich má příponu `.whl` tedy *wheel*, kde je právě zabalená sbuilděná pythoní knihovna.
- nyní musíme v adresáři `quiz-admin` přidat cestu ke této knihovně: 
`uv add ../quiz-common/dist/quiz_common-0.1.0-py3-none-any.whl`
- `uv` napsalo, že byly nainstalovány 2 balíčky: `quiz-common` a `quiz-admin`. Proč i `quiz-admin`? Protože se změnila jeho závislost, tak `uv` ho taky přebuildil. Odstranil původní verzi `quiz-common`, která se původně brala z internetu a nahradil ji sbuilděným `quiz-common` ze souboru.
- git status nám ukázal, že se změnily `pyproject.toml`, kde je právě adresa ke `quiz_common` a `uv.lock`- zde jsou přesně hashe všech závislostí
-  a to stejné musíme udělat i v adresáři `quiz-server`, i tady musíme přidat cestu ke této knihovně: 
`uv add ../quiz-common/dist/quiz_common-0.1.0-py3-none-any.whl`
- git status nám i zde ukáže změnu v `pyproject.toml` a `uv.lock`.
- teď si spustíme `kvíz linux_01` a hurá, ono nám to funguje!!!. 
- PR byl schválen a zamergován a branch byla smazána na GitHub a musíme si uklidit i u sebe.

### Lokální úklid:
- přepeneme se na main branch `git checkout main`
- `git fetch --prune` vidíme, že branch PR byla na GitHub opravdu smazaná 
- `git branch -vva` nám ukáže tuto branch u nás, a vidíme, že její předloha je pryč, takže teď ji můžeme smazat i u nás. Protože byl PR začleněn pomocí `squash and merge` a některé commity zmizely, git nám ji nepovolí smazat s přepínačem `-d`, ale musíme použít `git branch -D <název-větve>`

---

### Otestování knihovny naostro

- Knihovnu jsme si otestovali lokálně, PR zamergovali, uzavřeli a změny stáhli k sobě pomocí `git pull`. Náš `uv add` při lokálním testování zmodifikoval soubory `pyproject.toml` a `uv.lock`a my ty změny chceme dát pryč a to v `quiz-admin` i v `quiz-server`
- To uděláme pomocí `git restore pyproject.toml uv.lock` 

- pomocí `uv sync` se odstraní lokálně sbuilděná `quiz-common` a přidá se závislost z internetu - je zde i `commit hash`, kterou si můžeme ověřit v adresáři `quiz-common` pomocí `git log`

### Nečekaná chyba

- A tady jsme narazili na chybu, `uv sync` odkazoval na starý commit v `quiz-common` na GitHub. Při spuštění kvízu `linux-01` nám zase vyskočil bug s načítáním číselných odpovědí. Ale proč to tak je?

- pomocí `uv tree` vidíme strom zavislostí  a `uv pip freeze` nám ukáže přesné verze zavislostí a tady je ten důvod, proč nám `uv sync` odkazovalo na starý commit `quiz-common`.

- aby byla v `quiz-admin` i v `quiz-server` závislost na aktuální verzi `quiz-common`, Martin musel v obou repozitářích zadat `uv add <https://github.com/quiz-cli/quiz-common.git>`

- opět se aktualizovali v obou repozitářích závislosti v souborech `pyproject.toml` a `uv.lock`

- tyto aktualizované závislosti v repozitářích `quiz-admin` a `quiz-server` Martin commitnul a pushnul na GitHub, po zamergování si potom k sobě pullneme aktuální závislosti.

---

### Fix: send validated quiz data through websocket instead of raw data

Patricie ještě udělala opravu v repozitáři `quiz_admin`, kterou řeší tento [PR #6 – quiz-admin](https://github.com/quiz-cli/quiz-admin/pull/6).V původní verzi se volala třída `Quiz`, předala se jí data naloadovaná z Yamlu a udělal se model, který  se ale neuložil. Patricie jej uložila do proměnné `validated_quiz`, pomocí `model_dump()` jej poslala přes síť na server a díky tomu, že to prošlo modelem, se uplatnila validační funkce dělající z `int` `str`. I tento PR byl schválen a uzavřen.

---

### Server should evaluate answers#9 

- Toto issue řeší PR od Niny: [PR #9 - quiz-server](https://github.com/quiz-cli/quiz-server/pull/9).
-  zjistíme si branche pomocí `git fetch --prune`  `git branch -vva`, abychom se na ni mohli přepnout a změny otestovat
- přepli jsem se na branch: `git checkout nb_results`
- v terminálech jsme si spustili postupně : `quiz server`, `quiz-admin` a na něm `quiz_example.yaml`, `quiz-client` Bob a `quiz-client` Alice.
-nasimulovali jsme si kvíz se správnými a špatnými odpověďmi, po ukončení kvízu se  adminovi zobrazí vyhodnocené odpovědi klientů. Skvělé, funguje to!
**změny v kódu:**
- Nina definovala funci `correct_answer()`, která u otázky a vytvoří string správných odpovědí 
- díky ` app.state.correct_answer = correct_answer(question)` si při každé otázce server uloží správné řešení, aby ho mohl porovnat s odpovědí hráče 
- upravila funkci `check_answer()` ve třídě `Results`, kam se teď posílá správná odpověď.
- vyhodnocení správné odpovědi:
`  correct = (set(answer.lower().strip()) == set(correct_answer))` Odpověď se zbaví bílých znaků na koncích řetězce, převede na malá písmena a převede se na množinu, takže nezáleží na pořadí odpovědí a ignorují se duplicity
- PR byl schválen

### Důležitý návrh
- na srazu zazněl skvělý návrh, aby se odpověď vyhodnocovala už na straně klienta a ne až na serveru.

---

### Poznámky: 
- pokud akceptujeme v našich PR na GitHub `suggestions`, je nutné si potom k sobě změny stáhnout přes `git pull`.Pokud bychom to neudělali a lokálně si mezi tím commitli další změnu, nastane konflikt.

- nebudeme dávat PR do tabulky projektu. Ikdyž se naváže PR na issue, v tabulce projektu se PR automaticky přidá. 
To můžeme vypnout v okně PR, v nastavení záložky `Projekts`, oddělat zelenou šipečku , potom se PR v tabulce nezobrazí a zůstanou tam pouze `issues`. 
Proto je důležité vždy PR nalinkovat k issue.