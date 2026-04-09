

# Commits

**Datum:** 2026-03-19  
**Lektor:** Martin Zelený
**Zápis:** Veru T.

---

Hlavní téma této lekce byly commity. Bohužel v naší dokonalosti jsme neměli žádný problém, který bychom společně mohli vyřešit, ale prošli jsme alespoň základní principy a pravidla, kterými se bume řídit.

---

## What we have committed to

Github nám dovoluje commitovat více způsoby, pro náš projekt se omezíme pouze na *squash and merge* a *rebase and merge*. 

### Squash and merge
Pokud máte více commitů, které třeba vznikly i z řešení merge konfliktu, ale jednotlivé commity jsou malé a spíše na sobě nezávislé, je vhodné je mergnout do společného kódu v jednom commitu. O to se postará právě squash and merge - vaše commity "scucne" do jednoho, který dostané nové unikátní ID a description.

### Rebase and merge
Tato volba mergování se hodí spíše pro velké úpravy kódu rozdělené do více commitů, které na sebe logicky navazují. Toto nám povolí stále procházet historii změn po menších na sebe navazujících celcích. 
Git hub vezme celou vaši větev commitů a přehodí ji na poslední commit společné main větve.

**Před zmergováním:**

![before](before.png)


⬇

**A po zmergování:**

![after](after.png)


## Nejčastější chyby:
1. Pozor, abyste vždy při commitování používali aktuální verzi kódu - tj. nejdřív git pull, až pak git push. 
2. Nepracujte se společným mainem - **vytvořte si vlastní branch, kterou po mergování smažete**.
3. Nevytvářejte merge commity - chceme jen jeden main branch, žádný složitý nádraží.
4. No a pište slušný commit zprávy, ať víme, co se stalo a nemusíme po tom v kódu pátrat.