
Cau, 
tak jsem dneska koukal do tech dokumentu a snazil se co nejvice toho projit. Hlavne jsem se zameroval na cenu a co presne by mel byt vystup toho co dostanete.  
  
A musim rict, ze ta cena je opravdu relativne vysoka. Nicmene co vede k tak vysoke cene?
1. Vystup projektu je opravdu rozsahly a zahrnuje relativne dost funkcionality
2. Mapotico samo v dokumentu uvadi, ze snazi omezit vendor lock na 3rd party services, coz ve vysledku znamena vice vlastniho kodu a tudiz i spoustu casu, ktere jim budete muset zaplatit
3. Micro-service architektura - prijde mi to jako docela overkill pro start-up, zase vede k vetsi komplexite celeho reseni a k navyseni ceny
4. Fokus na velkou skalovatelnost, nevim kolik mate zakazniku, ale navrhovane reseni mi prijde jako pro velky korporat, ktery by mel umet obslouzit deseti tisice zakazniku denne
5. Responzivita webu - samotny portal by mel byt responzivni na vsech zarizenich (dalsi pridana komplexita, ktera mozna ani nedava smysl)
6. Relativne dost casu straveneho na prvni a posledni fazi - jak jsem jiz zminil, spoustu reseni si chteji delat vlastnich, tudiz se to prodrazi, plus relativne dost casu na konci pro testovani atd... , vsechno prodlouzene kvuli bodum zminenym vyse - komplexita systemu

Ve vysledku dostanete docela dost komplexni aplikaci, s micro-service's, dev-ops zahrnujici nekolik prostredi na development, automatizovane testy, prodkucni prostredi
Vsechny tyto casti, by meli mit naprogramovany dobry tooling na monitoring, zachytavani bugu a monitoring vytizenosti.

Nicmene z me vlastni zkusenosti toto muze byt i relativne kontra-produktivni, jelikoz komplexni system, ktery je pripraveny skalovat z hlediska vytizenosti je taky daleko tezsi menit, nebo pridavat funkcionalitu. Tudiz muze dost zpomalit dalsi vyvijeni systemu (trade off mezi tim kolik uzivatelu najednou system zvladne oproti flexibilite). Je tam relativne dost dev ops funkcionalit, jako napriklad prostredi pro autmatizovane testy, ktere vam budou k nicemu pokud na tom uz nikdo nebude vyvijet

Custom reseni nekterych casti take muze zpusobit daleko slozitejsi on-boarding do kodu a platformy, ktere nemusi byt dokonce industry standartem. Delegovani nekterych veci na 3rd part snizuje komplexitu, coz znamena i mensi prostor pro bugy ve vlastni aplikaci.  3rd party reseni muze zpusobit vendor-lock, nicmene je to take abstrakce k rychlejsui pochopeni a praci s danou problematikou



