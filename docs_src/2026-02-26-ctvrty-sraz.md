Zápis z meetingu – IT projekt



Vysvětlovali jsme is logiku hry.Procházeli jsme část admin, ale nejdřív jsme si museli spustit server. Ke spuštění serveru používáme UV - příkaz uv run.



&nbsp;       uv = hlavní command



&nbsp;       run = subcommand (spustí nástroj nebo aplikaci)



Pak jsme spustili quiz-admin pomocí 

&nbsp;	quiz-admin localhost:8000 .\\data\\quiz\_example.yaml 



Pokud příkaz není nalezen, stačí doplnit uv run:

&nbsp;   uv run quiz-admin localhost:8000 .\\data\\quiz\_example.yaml



Pak jsme si spustili quiz-client. Pokud klient nezadá jméno hned, aplikace se zeptá:



&nbsp;       quiz-client localhost:8000



&nbsp;       Choose your name:



Když klient vypíše jméno, tak se nám pak na admin propíšou přihlášení hráči. Typická jména pro IT verze bývají Alice a Bob.





Průběh kvízu



Máme nadefinované otázky - budeme k tomu využívat YAML.



Admin odešle otázku na server (y) → server pošle otázku ke klientům → klienti odpovídají.



Server registruje odpovědi, ale zatím je nevyhodnocuje. 



Když admin znovu pošle otázku (y), posílá se další otázka.



Počet otázek je nyní 2. Kvíz se ukončí, jakmile se odpoví na poslední otázku. 



Po zodpovězení poslední otázky server odpojí klienty. 



Pak se výsledky v JSON pošlou adminovi. Budeme je formátovat pomocí jq (instalace jq na Windows:winget install jqlang.jq). Samotné formátování pak vypadá takto:  

&nbsp;	'\[{"player":"alice","question\_number":0,"answer":"a","correct":true},{"player":"bob","question\_number":0,"answer":"b","correct":true},{"player":"alice","question\_number":1,"answer":"cd","correct":true},{"player":"bob","question\_number":1,"answer":"blabla","correct":true}]' | jq





Admin se následně také odpojí. Konec.

 

Aktuální omezení:

* &nbsp;	Máme jen 2 otázky, doplníme další. 
* &nbsp;	Máme variantu otázky jen na a-b-c
* &nbsp;    Klienti mohou odpovídat i mimo aktivní otázku, ale odpověď se nezaznamená.
* &nbsp;	Admin nevidí počet hráčů, kteří už odpověděli (např. 4 ze 7).
* &nbsp;	Nemáme hodnocení odpovědí

&nbsp;		Je v plánu zobrazovat výsledky pomocí JSON.

&nbsp;		Padl návrh udělat kontrolu odpovědí. Kdyby zadaná odpověď nebyla v nabídce, měli bychom hráče upozornit.



Potom jsme si otevřeli soubory k projektu ve VS Code. Otevřeli jsme si samostatná okna pro server - client - admin.



**Vysvětlujeme si klienta (client)**



Klient zavolá asynchronně send and receive messages. Tím se vytvoří websocket spojení na to url. Přijímání a odpovídání na otázky je tedy asynchronní a tedy korutinní pro: send messages, receive messages.



Při prvním spojení si také vytváříme ID klienta přes jeho odpověď na otázku na jméno.



Server si díky tomu poznačí, že je to ID toho daného klienta a pak budou všechny odpovědi spárované přes to ID. 

await ws.send(json.dumps({"client\_id": client\_id, "answer": user\_input}))



Klient přijímá otázky ze serveru permanentně. Když admin zašle otázku, tak se zobrazí u klienta, ten na otázku odpovídá. Po zadání odpovědi se odešle JSON.





**Konečné poznámky:** 

Musíme se starat o logiku té hry

Možná funkci def print\_question přidáme do quiz-common, aby to bylo možné pro více komponentů.

Pak jsme se přesunuli na Pyvo, kde měla přednášku Veronika Kabátová z RedHat.

