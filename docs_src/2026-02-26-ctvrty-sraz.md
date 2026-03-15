2026-02-26

**Lektor:**  
Martin Zelený

**Zápis:**  
Veronika Vrbková

---

Vysvětlovali jsme si logiku kvízu. Procházeli jsme část admin a klient a řekli si nějaká kvízová omezení, která zatím máme. Pak jsme se přesunuli na Pyvo do Artbaru.

---

## Spuštění aneb jaké repo pustit dřív

Nejdřív si spouštíme server. Ke spuštění serveru používáme UV - příkaz uv run.
- uv = hlavní command
- run = subcommand (spustí nástroj nebo aplikaci)

Pak jsme spustili quiz-admin pomocí
quiz-admin localhost:8000 .\\data\\quiz\_example.yaml 
- pokud příkaz není nalezen, stačí doplnit uv run:
uv run quiz-admin localhost:8000 .\\data\\quiz\_example.yaml

Nakonec jsme si spustili quiz-client. 

Pokud klient nezadá jméno hned, aplikace se zeptá, př: 
quiz-client localhost:8000
Choose your name:

Když klient vypíše jméno, tak se nám pak na admin propíšou přihlášení hráči. Dozvěděli jsme se, že typická jména pro IT verze bývají *Alice* a *Bob*.

Testovací kvízové otázky máme zatím jen 2. K jejich tvorbě budeme využívat YAML. 

## Jak se děje kvíz

1. Admin odešle otázku na server pomocí *y* 
2. Server pošle otázku ke klientům
3. Klienti odpovídají
4. Server registruje odpovědi, ale zatím je nevyhodnocuje! 
5. Admin znovu pošle otázku *y*, posílá se přes server klientům další otázka.
6. Klienti odpovídají.
7. Kvíz se ukončí, jakmile se odpoví na poslední otázku (v našem případě po zodpověezení druhé otázky). Po zodpovězení server odpojí klienty. 
8. Pak se výsledky v JSON pošlou adminovi.
9. Admin se následně také odpojí. Konec.

**Formátování výsledků JSON**
Budeme je formátovat pomocí jq 
- Instalace jq na Windows >> winget install jqlang.jq 
- Samotné formátování výsledků pak vypadá takto:  
'\[{"player":"alice","question\_number":0,"answer":"a","correct":true},{"player":"bob","question\_number":0,"answer":"b","correct":true},{"player":"alice","question\_number":1,"answer":"cd","correct":true},{"player":"bob","question\_number":1,"answer":"blabla","correct":true}]' | jq

## Vysvětlujeme si klienta (client)
Potom jsme si otevřeli soubory k projektu ve VS Code. Otevřeli jsme si samostatná okna pro server - client - admin.

Klient zavolá asynchronně send and receive messages. Tím se vytvoří websocket spojení na to url. Přijímání a odpovídání na otázky je asynchronní a tedy korutinní.

Při prvním spojení si také vytváříme ID klienta přes jeho odpověď na otázku na jméno.

Server si díky tomu poznačí, že je to ID toho daného klienta a pak budou všechny odpovědi spárované přes to ID. 
await ws.send(json.dumps({"client\_id": client\_id, "answer": user\_input}))

Klient přijímá otázky ze serveru permanentně. Když admin zašle otázku, tak se zobrazí u klienta, ten na otázku odpovídá. Po zadání odpovědi se odešle JSON.

## Aktuální omezení:

* Máme jen 2 otázky, doplníme další. 
* Máme variantu otázky jen na a-b-c
* Klienti mohou odpovídat i mimo aktivní otázku, ale odpověď se nezaznamená.
* Admin nevidí počet hráčů, kteří už odpověděli (např. 4 ze 7).
* Nemáme hodnocení odpovědí - padl návrh udělat kontrolu odpovědí tzn. kdyby zadaná odpověď nebyla v nabídce, měli bychom hráče upozornit.


**Konečné poznámky:** 

* Musíme se starat o logiku hry.
* Možná funkci def print\_question přidáme do quiz-common, aby to bylo možné pro více komponentů.
* Pak jsme se přesunuli na Pyvo, kde měla přednášku Veronika Kabátová z RedHat o tom, jaké to je v IT a jak se posunovat na žebříčku výš.

