# Contributing

Dodajanje novih funkcionalnosti ali popravljanje napak se dogaja prek
pull requestov (PR). To najlažje naredite prek svojega forka repozitorija.
Vsebino PR in commitov pišite v slovenščini.

Poskrbite, da PR ni prevelik in da je zaključena celota. Po vsakem PR mora aplikacija še vedno
delovati. Pri vsakem PR:

* napišite smiselen naslov, ki pove, kaj PR naredi;
* napišite opis, kjer opišete, kaj je problem in kako ga rešite (lahko se sklicujete ali zaprete
  primeren issue)
* commiti v PRju so zaključene celote (če je potrebno kaj popraviti, uredite obstoječi commit in
  ne naredite novega)
* sprememba naj bo ena sama in koda naj bo čimbolj berljiva
* PR mora na githubu dobiti kljukico, da so vsi avtomatski testi ok. To vključuje
  - test funkcionalnosti
  - test stila kode
  - test generiranja dokumentacije (po #25)

Te tri teste lahko poženete tudi lokalno (glejte ukaze v [.github/workflows/](.github/workflows/)).
Za poganjanje je potrebno imeti instaliran `black` in `sphinx`. Kodo lahko samodejno oblikujete v
urejevalniku, lahko pa tudi poženete

    python -m black .

Morebitne napake popravite tako, da uredite svoje commite (ne dodati na koncu enega commita, ki
popravi vse napake). Enako velja za spremembe med procesom pregleda.

Po prvem uspešno sprejetem PRju boste tudi dodani na seznam razvijalcev.

## Dodajanje novih problemov

Za dodajanje novega problema je potrebno:

- V datoteko `nadlogar/problems/models.py` dodati nov podrazred razreda `Problem`.
- V dokumentacijski niz razreda napišite en stavek, ki opisuje vrsto problema. Ta stavek naj bo golo besedilo (brez LaTeXa, HTMLja, …), ki se bo prikazalo uporabnikom ob izbiri problema.
- Vsem parametrom je treba kot prvi argument podati niz s pravilnim prikazom imena (s šumniki in morebitnimi velikimi začetnicami).
- Vsem parametrom je treba podati argument `help_text` z besedilom, ki opisuje namen parametra.
- V podrazredu `Meta` je treba definirati spremenljivko `verbose_name` s pravilnim prikazom imena problema.
- Definirati metodo `generate`, ki vrne bodisi slovar podatkov.

V metodi `generate` naključne vrednosti izbirate s pomočjo funkcij iz knjižnice `random`. Za nastavitev semena generatorja psevdonaključnih števil vam ni treba skrbeti. Če želite v problemu delati s simbolnimi izrazi, uporabite knjižnico `sympy`. Če želite lepo rešitev, je običajno bolje, da generirate najprej rešitev in nato nalogo, na primer najprej ničle polinoma in iz njih koeficiente ter ne obratno. Včasih se to ne da in za generiranje lepe rešitve potrebujete več poskusov. V tem primeru uporabite izjemo `GeneratedDataIncorrect`, ki jo sprožite, kadar podatki niso ustrezni. V tem primeru bo program izbral novo seme generatorja ter nalogo poskusil sestaviti znova.
