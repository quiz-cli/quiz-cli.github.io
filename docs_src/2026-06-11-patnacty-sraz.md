# Patnáctý sraz - léto

**Datum:** 11.06.2026  
**Lektor:** Martin Zelený  
**Zápis:** Nina Belyavskaya

V červnu, po přestávce, nás bylo jenom tři a Martin. Další holky se připojily online.

Martin nám popovídal o workshopu MicroPython a pozval nás na DevConf.
Také Martin připomněl nápad Borise, abychom někde v září v nějakou sobotu udělali hackaton. Po prázdninách budeme potřebovat všechno připomenout.

## Stejnojmenné branches

Právě teď můžeme vytvářet issue v jednom repozitáři a PR k danému issue linkovat z různých repozitářů.
Proto v budoucnosti potřebujeme nový job v GitHub Actions, který bude spouštět testy výběrem větví se stejnými názvy z různých repozitářů. A měli bychom už teď pojmenovávat branches stejně, pokud odpovídají stejnému úkolu.

Bohužel GitHub v odkazech na issue nebo PR používá jenom čísla. Ale v tabulce projektu <https://github.com/orgs/quiz-cli/projects/1/views/1> můžeme vidět linked pull requests.

## Bug se třemi hráči

Jana nám ukázala zvláštní bug. Dosud jsme hru testovali jenom se dvěma hráči. Jana zkusila spustit hru se třemi hráči a všimla si, že po konci hry dva hráči hru normálně ukončili, ale třetí hráč zůstal připojený k serveru. Vyzkoušeli jsme to na dalších počítačích a ujistili jsme se, že chyba existuje a lze ji reprodukovat. Martin také spustil více hráčů a zjistil, že každý třetí hráč zůstává připojený.

Není zřejmé, jestli ten bug byl v původním kódu, nebo byl přidán v nějakém commitu. Martin řekl, že možná budeme potřebovat příkaz `git bisect`, který automaticky rozdělí historii na půl a postupně zužuje rozsah – dokud nenajde přesně ten commit, kde se chyba poprvé objevila. 

Také Martin nám ukázal, jak použít debugging, ale pro tento bug to neposkytlo žádné informace.

Hned po srazu ale Jana udělala PR, který ten bug fixnul.

