Autor: David Martinek
E-mail: martinek NA fit.vutbr.cz
Datum: 31.3.2006
Verze: 1.0

Používání BibTeXu podle normy ČSN ISO 690
-----------------------------------------
Standardní BibTeXové styly nejsou přeloženy do češtiny a formátování položek nesouhlasí s normou. Pro své potřeby jsem si vytvořil nový styl czechiso.bst, který se snaží tyto problémy řešit. Tento styl vzniknul překladem souboru

/usr/share/texmf/tex/latex/custom-bib/english.mbs

a následným použitím příkazu

latex makebst

Tím vniknul skript czechiso.dbj, který po přeložení latexem vytvoří soubor se stylem czechiso.bst. Pokud budete potřebovat ve stylu něco změnit, nejjednodušší je upravit skript czechiso.dbj a vygenerovat nový, modifikovaný styl (latex csechiso.dbj).

Styl czechiso.bst
-----------------
Styl je přeložen do češtiny, takže ve výsledném dokumentu by se měly objevovat výrazy 'vydání' namísto 'edition', 'ročník' namísto 'volume' apod. Tento styl vychází ze stylu plain.

Položky isbn a issn jsou standardními styly bibtexu ignorovány, ale norma ISO 690 tyto údaje vyžaduje. Styl czechiso.bst se snaží této normy držet a tyto údaje zpracovat umí, takže tyto položky lze bez obav používat. (Dříve jsem tyto údaje dával do položky note, což ale není nejlepší řešení.)

Standardní styly rovněž ignorují položku url. Ve stylu czechiso tuto položku lze používat, ale je potřeba zároveň s tímto stylem použít balík url tímto způsobem:

\usepackage{url}
\DeclareUrlCommand\url{\def\UrlLeft{<}\def\UrlRight{>} \urlstyle{tt}}

Jde o provizorní řešení. Časem snad přijdu na to, jak tento kód vložit přímo do souboru se stylem.

POZOR!
------
Tento styl zatím normě neodpovídá přesně. Aby styl odpovídal normě přesněji, je potřeba přepsat některé funkce, zejména ty, které ovlivňují pořadí položek ve výsledném dokumentu.

Dále by bylo dobré upravit
-MANUAL, ARTICLE a podobně, aby akceptovaly položku howpublished (aby šlo tisknout hodnoty [online], [CD-ROM], atd.).

Záznamy BibTeXu
---------------
Položky označené ve výčtu na konci tohoto dokumentu jako OPT jsou volitelné. Položky označené jako ALT jsou alternativy. Před použitím je nutné tyto předpony umazat, stejně jako všechny nepoužité položky.

Všechny neznámé položky jsou bibtexem ignorovány. Mohou ale být zpracovány speciálním stylem. Většina stylů například ignoruje položku annote, do které si tak lze zapisovat vlastní poznámky.

Tipy pro vytváření databází
---------------------------
Položka key
BibTeX, v závislosti na použitém stylu, řadí záznamy buď podle příjmení autora a roku vydání (plain, alpha) nebo podle pořadí použitých citací (unsrt). Pokud u některého záznamu chybí autor, může se záznam ocitnout na místě, které nechceme. V takovém případě je vhodné vyplnit položku key, která se nikde netiskne, ale BibTeX ji využije při řazení záznamů. Lze sem umístit například příjmení editora nebo první slovo z názvu.

BibTeX neumí řadit česky, takže je dobré sem umisťovat příjmení autora bez diakritiky (key = { ZOUZELKA2003 },).

Položka author
Podle normy by se měla příjmení sázet velkými písmeny. BibTeX (resp. styl czechiso) sám písmena nezvětšuje, takže je nutné psát příjmení velkými písmeny už do záznamů. Styl czechiso používá příjmení a první písmena jmen, je ale vhodné do záznamů umísťovat celá jména (pokud jsou známa), aby je šlo využít při použití jiných stylů (author = {David MARTINEK}, ).

Pokud má dokument více autorů, oddělují se v záznamu slovem and (author = {David MARTINEK and Jakub ČERNOHORSKÝ and Zdena RÁBOVÁ},).

Položka note
Sem umísťujeme informace, pro které nelze v daném záznamu nalézt odpovídající položku. Například @ARTICLE neobsahuje položku howpublished. Pokud citujeme článek z internetového časopisu, dá se text [online] umístit právě do položky note. Dalšími kandidáty pro umístění v této položce jsou texty "naposledy navštíveno", či "poslední aktualizace", pokud se tyto údaje nehodí do položky year.

Položky volume a number
Zároveň je lze použít pouze v záznamech @ARTICLE. Volume znamená ročník časopisu (bývá odlišný od roku vydání) a number znamená číslo časopisu v rámci tohoto ročníku. U jiných typů záznamů má smysl vyplňovat volume pouze, pokud jde o periodikum (v czechiso se vždy předsadí slovo ročník).

Položka edition
Edition znamená vydání a má smysl u publikací jako jsou knihy nebo sborníky. Pokud jako hodnotu této položky použijete číslovku od 1 do 5, nahradí se to v dokumentu za text "první -- páté vydání". První vydání se používá jen v případech, kdy víme, že vyšlo i nějaké další vydání, ale chceme zdůraznit, že v dokumentu bylo explicitně použito vydání původní.

Položka pages
Tato položka obsahuje informaci o stránce nebo rozsahu stránek, na kterých se dokument v rámci knihy nebo sborníku nachází. Pokud použijeme údaj 10--20, vysází se "s. 10--20", pokud použijeme údaj 10, bude to např. u časopisu (@ARTICLE) znamenat "str. 10", tedy že se článek nachází na straně 10. U knihy se vysází "10 s.", což znamená, že kniha má celkem deset stran.

Položky isbn, issn
Mají smysl jen někde. Jejich hodnotou je pouze číslo, texty ISBN, ISSN se sází automaticky.

Položka url
Její hodnotou je pouze holá adresa (url = {http://www.seznam.cz}), styl czechiso doplní automaticky text URL. 

Při použití této položky je nutné použít balík url a makrem DeclareUrlCommand nastavit formátování (norma vyžaduje, aby adresy byly v úhlových závorkách). Z praktických důvodů doporučuji nechat styl tt (strojopisný řez), jinak se nebudou správně sázet symboly jako ~ (tilda) a _ (podtržítko). Na začátek dokumentu prostě vložte toto:
\usepackage{url}
\DeclareUrlCommand\url{\def\UrlLeft{<}\def\UrlRight{>} \urlstyle{tt}}

Položky address a publisher
Do položky address se píše město, ve kterém byl dokument vydán (např. Ostrava), položka publisher obsahuje název vydavatelství (např. MARQ), styl czechiso poté vysází tyto údaje podle normy (Praha: MARQ). 

Položka editor
Vyskytuje se například u knih a sborníků. Jde o osobu, která není přímo autorem, ale provedla složení kapitol či článků od jiných autorů do jednoho celku.

Překladatelé, ilustrátoři
Pro tyto osoby nejsou definovány speciální položky. Pro jejich vysázení je nutné použít opět položku note (note = {Přeložil Jan Hromádka, ilustroval Cyril Pírko})

Položka note
Typicky se používá pro ukládání dat, které se nedají vložit nikam jinam. Například u internetových zdrojů sem lze vložit toto: note = {[Online], Verze 3.1 (2004), [rev. 2004-11-11], [cit. 2006-03-31]}, což znamená, že jde o zdroj na internetu, aktuální použitá verze byla 3.1 z roku 2004, jejíž poslední revize proběhla podle autora 11. listopadu 2004, a já jsem tuto stránku naposledy kontroloval 31. března 2006.

Článek v časopise:

@Article{,
author = {},
title = {},
journal = {},
year = {},
OPTkey = {},
OPTvolume = {},
OPTnumber = {},
OPTpages = {},
OPTmonth = {},
OPTnote = {},
OPTannote = {},

OPTisbn = {},
OPTissn = {},
}



Článek na konferenci:

@InProceedings{,
author = {},
title = {},
booktitle = {},
OPTcrossref = {},
OPTkey = {},
OPTpages = {},
OPTyear = {},
OPTeditor = {},
OPTvolume = {},
OPTnumber = {},
OPTseries = {},
OPTaddress = {},
OPTmonth = {},
OPTorganization = {},
OPTpublisher = {},
OPTnote = {},
OPTannote = {},

OPTisbn = {},
OPTissn = {},
}



Článek ve sbírce:

@InCollection{,
author = {},
title = {},
booktitle = {},
OPTcrossref = {},
OPTkey = {},
OPTpages = {},
OPTpublisher = {},
OPTyear = {},
OPTeditor = {},
OPTvolume = {},
OPTnumber = {},
OPTseries = {},
OPTtype = {},
OPTchapter = {},
OPTaddress = {},
OPTedition = {},
OPTmonth = {},
OPTnote = {},
OPTannote = {},

OPTisbn = {},
OPTissn = {},
}



Kaptitola nebo stránky v knize:

@InBook{,
ALTauthor = {},
ALTeditor = {},
title = {},
chapter = {},
publisher = {},
year = {},
OPTkey = {},
OPTvolume = {},
OPTnumber = {},
OPTseries = {},
OPTtype = {},
OPTaddress = {},
OPTedition = {},
OPTmonth = {},
OPTpages = {},
OPTnote = {},
OPTannote = {},

OPTisbn = {},
OPTissn = {},
}



Sborník konference:

@Proceedings{,
title = {},
year = {},
OPTkey = {},
OPTeditor = {},
OPTvolume = {},
OPTnumber = {},
OPTseries = {},
OPTaddress = {},
OPTmonth = {},
OPTorganization = {},
OPTpublisher = {},
OPTnote = {},
OPTannote = {},

OPTisbn = {},
OPTissn = {},
}



Kniha či monografie:

@Book{,
ALTauthor = {},
ALTeditor = {},
title = {},
publisher = {},
year = {},
OPTkey = {},
OPTvolume = {},
OPTnumber = {},
OPTseries = {},
OPTaddress = {},
OPTedition = {},
OPTmonth = {},
OPTnote = {},
OPTannote = {},

OPTisbn = {},
}



Brožura:

@Booklet{,
title = {},
OPTkey = {},
OPTauthor = {},
OPThowpublished = {},
OPTaddress = {},
OPTmonth = {},
OPTyear = {},
OPTnote = {},
OPTannote = {},

OPTisbn = {},
OPTissn = {},
}



Dizertační práce:

@PhdThesis{,
author = {},
title = {},
school = {},
year = {},
OPTkey = {},
OPTtype = {},
OPTaddress = {},
OPTmonth = {},
OPTnote = {},
OPTannote = {}
}



Diplomová práce (nebo bakalářka):

@MastersThesis{,
author = {},
title = {},
school = {},
year = {},
OPTkey = {},
OPTtype = {},
OPTaddress = {},
OPTmonth = {},
OPTnote = {},
OPTannote = {}
}



Technická zpráva:

@TechReport{,
author = {},
title = {},
institution = {},
year = {},
OPTkey = {},
OPTtype = {},
OPTnumber = {},
OPTaddress = {},
OPTmonth = {},
OPTnote = {},
OPTannote = {},
}



Technický manuál:

@Manual{,
title = {},
OPTkey = {},
OPTauthor = {},
OPTorganization = {},
OPTaddress = {},
OPTedition = {},
OPTmonth = {},
OPTyear = {},
OPTnote = {},
OPTannote = {}
}



Nepublikováno veřejně (dostupnost lze specifikovat v poznámce):

@Unpublished{,
author = {},
title = {},
note = {},
OPTkey = {},
OPTmonth = {},
OPTyear = {},
OPTannote = {}
}



Ostatní:

@Misc{,
OPTkey = {},
OPTauthor = {},
OPTtitle = {},
OPThowpublished = {},
OPTmonth = {},
OPTyear = {},
OPTnote = {},
OPTannote = {}
}
