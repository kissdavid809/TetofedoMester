# Weboldal-modernizáció: problémák és megállapítások

## Rövid összefoglaló

A projekt jelenlegi állapota egy régi weboldal főoldalának statikus mentése, nem egy teljes, önálló webhely. A megjelenés több olyan képfájltól függ, amelyek nem találhatók meg a projektben, a fix szélességekre építő elrendezés mobilon nem használható, a navigáció pedig az éles webhely régi URL-jeire mutat. A HTML, a CSS és a JavaScript több régi technikát és fölösleges függőséget tartalmaz.

Az ellenőrzés a munkaterületen található fájlokra és a főoldal forrására korlátozódott; az éles webhely, szerverbeállítások és a hiányzó aloldalak működését nem vizsgáltam.

## Kritikus működési problémák

1. **Hiányzó CSS-képek:** a [main.css](main.css) a `../img/` útvonalon keresi a `bg_body.png`, `bg_menu.png`, `snp_menu_mod.png`, `snp_menu.png`, `bg_bd.png`, `loader.gif` és `bg_footer.png` fájlokat. A projektben nincs `img/` könyvtár, ezért ezek a háttérképek nem tölthetők be. A menüpontok felirata CSS-ben el van rejtve (`text-indent: -9999px`), így a menühöz szükséges képek nélkül a navigáció láthatatlanná vagy nehezen használhatóvá válhat.
2. **Hiányzó galéria-képek:** a [style.css](style.css) `loader.gif`, `prev.png`, `next.png`, `dot.png` és `triangle.png` fájlokra hivatkozik, de ezek sincsenek a projektben. A galéria stílusai a jelenlegi HTML-ben nem használtak, így ez valószínűleg más oldalakból visszamaradt, hiányos komponens.
3. **A navigáció nem a projekten belül működik:** a [TetofedoMester.html](TetofedoMester.html) menüpontjai a `https://tetofedomester.hu/?w=1`–`?w=6` címekre mutatnak. A projektben csak egyetlen HTML-oldal van; ha a helyi példányt böngészik, a menü elhagyja azt, és az éles domain működésétől függ. A JavaScript a kattintásokat elkapja, majd ugyanoda navigál tovább, ezért a viselkedés nem jelent helyi aloldal-kezelést.

## Fájlszerkezet és függőségek

- **A fájlnevek letöltési maradványt tartalmaznak:** a JavaScript-fájlok neve `.js.letöltés` végű. Ez nem szokványos webes fájlkiterjesztés; a webszerver MIME-típusa és a fejlesztői eszközök kezelése ettől függően problémás lehet. Érdemes szabványos `.js` névre átnevezni őket.
- **Régi, projektben szétszórt függőségek:** a [TetofedoMester.html](TetofedoMester.html) helyi fájlként tölti be a jQuery 1.7.1-et és két bővítményt. A jQuery-verzió nagyon régi, a függőségek verziózása és frissítése nincs dokumentálva.
- **Használatlannak tűnő bővítmények:** a `jquery.mousewheel.js.letöltés` és a `jquery.infieldlabel.js.letöltés` be van töltve, de a jelenlegi oldalon nincs egérgörgő-funkció vagy űrlap, amely ezeket igénybe venné. A fölösleges függőségek elhagyhatók.
- **Hiányzik az eszközlánc és a projektleírás:** nincs csomagkezelő-konfiguráció, build- vagy tesztbeállítás, sem dokumentáció arról, hogyan kell az oldalt futtatni vagy módosítani. Egy egyszerű statikus webhelyhez nem feltétlenül kell buildrendszer, de a fájlstruktúrát és futtatást érdemes dokumentálni.
- **A fájlok nincsenek szerepkör szerint csoportosítva:** minden fájl a gyökérben van, a képek és a stílusok helye nem egységes. Javasolt például `assets/images/`, `css/` és `js/` mappákat használni, ha az oldal több fájllal bővül.

## HTML és hozzáférhetőség

- **Hiányzik a HTML5 doctype:** a dokumentum nem `<!doctype html>` sorral kezdődik, ezért a böngésző kompatibilitási/quirks módba válthat.
- **Nincs megadva a dokumentum nyelve:** a `<html>` elemről hiányzik a `lang="hu"`, ami rontja a képernyőolvasók és nyelvfelismerő eszközök működését.
- **Nincs mobilnézetet beállító viewport meta:** hiányzik a `width=device-width, initial-scale=1` beállítás, így a mobil böngészők az oldalt kicsinyített asztali nézetként jeleníthetik meg.
- **Hiányoznak a szemantikus oldalrészek és a címsor-hierarchia:** a fejléc, navigáció, fő tartalom és lábléc egyszerű `div` elemekkel készül; a tartalomnak nincs látható `h1` címe. A szemantikus elemek és címsorok javítanák a billentyűzetes és képernyőolvasós tájékozódást, valamint a keresőmotorok tartalomértelmezését.
- **Nincsenek képleírások:** a logó, a bemutatkozó kép és az aláírás képe nem tartalmaz `alt` attribútumot. A dekoratív képeknél üres `alt` kell, a tartalmi képeknél rövid, értelmes leírás.
- **A tartalom elrendezése sortörésekkel és inline stílusokkal történik:** több `<br>` és közvetlenül az elemekre írt stílus szabályozza a térközöket és az igazítást. Ez nehezíti az újratördelést, az akadálymentesítést és a későbbi módosításokat.
- **A `<meta>` karakterkódolás régi formában szerepel:** a jelenlegi `http-equiv` változat helyett a rövidebb `<meta charset="UTF-8">` forma javasolt, a HTML5 doctype-pal együtt.

## CSS és reszponzivitás

- **Kötelező 1010 px minimális szélesség:** a [main.css](main.css) a `body` környezetében több elemre, például a fejléc- és tartalmi sávokra `min-width: 1010px` értéket állít. Keskeny kijelzőn vízszintes görgetést és levágott tartalmat okoz.
- **Fix méretekre és pozicionálásra épít:** a fejléc, a tartalom, a lábléc és a navigáció rögzített méretekkel, negatív margókkal, abszolút pozíciókkal és fix magasságokkal van elrendezve. Hosszabb szöveg vagy eltérő betűméret esetén átfedés, levágás vagy üres hely keletkezhet.
- **A HTML és a JavaScript is kézzel állít magasságokat:** a HTML-ben inline magasságok vannak, a JavaScript pedig futáskor újraméretezi a wrapper- és tartalmi elemeket. Ez törékeny, nehezen követhető elrendezést eredményez; a magasságot inkább a tartalom és a CSS kezelje.
- **Régi, képsprite-alapú navigáció:** a menü megjelenése külső sprite-képekre és háttérpozíciókra támaszkodik. A szöveg elrejtése miatt a felirat nem látható, és az állapotok (hover/aktív) karbantartása is a képfájltól függ.
- **Elavult CSS-szintaxis és böngésző-specifikus maradványok:** a stílusokban többek között `cursor: hand`, ismételt `outline` deklarációk és régi `-moz-`/`-webkit-` prefixek vannak. Ezek tisztítandók, a támogatott böngészőkhöz igazítva.
- **Túl apró alapbetűméret és sorkizárt szöveg:** a `body` 68.5%-os betűméretet, a bemutatkozó blokk pedig sorkizárást használ. Ez olvashatósági gondot okozhat, különösen kisebb kijelzőn vagy nagyított betűméretnél.
- **Az oldalakhoz nem tartozó galériastílusok is betöltődnek:** a [style.css](style.css) jelenleg nem használt galéria- és előnézeti szabályokat tartalmaz. Ezeket vagy a hozzájuk tartozó működést kell beépíteni, vagy a stíluslapot elhagyni.

## JavaScript és működés

- **Nem szükséges JavaScript a főoldal tartalmához:** a főoldal statikus szöveg és képek megjelenítése JS nélkül is működhetne. A jelenlegi kód jQuery-t tölt be képek előtöltéséhez, menükattintás kezeléséhez és méretek számításához.
- **Böngésző-azonosítás user-agent alapján:** a `main.js.letöltés` a `navigator.userAgent` szövegéből próbálja felismerni a böngészőt. Ez törékeny; ahol szükséges, képességvizsgálat vagy szabványos böngészőviselkedés használata javasolt.
- **A menü működése JavaScript-függővé válik:** a kód kattintáskor letiltja az alapértelmezett navigációt, majd saját átirányítást indít. Ha a script betöltése hibázik, eltérhet a viselkedés; ha nem hibázik, a helyi menüpontok akkor is az éles webhelyre visznek.
- **Egy sorba sűrített, nehezen karbantartható saját kód:** a `main.js.letöltés` teljes logikája tömörített, formázatlan sorokban van. Ez megnehezíti a hibakeresést és a biztonságos módosítást.

## Tartalom és kereshetőség

- **A meta leírás kulcsszóhalmozás:** a hosszú leírás vesszővel elválasztott szolgáltatásneveket sorol fel. Helyette rövid, természetes nyelvű, az oldal tartalmát összefoglaló leírás javasolt.
- **Hiányos kereső- és megosztási metaadatok:** nincs canonical URL vagy közösségi megosztáshoz szükséges Open Graph metaadat. Ezek beállítását az új URL-struktúra és az éles oldal üzemeltetése után kell elvégezni.
- **Hiányos kapcsolatfelvételi út a mentett főoldalon:** a bemutatkozás szolgáltatásokat kínál, de a jelenlegi HTML-ben nem látható telefonszám, e-mail-cím vagy kapcsolatfelvételi gomb. Ellenőrizni kell, hogy ezek más, jelenleg hiányzó aloldalon szerepelnek-e.
- **A főoldalmentés nem tartalmazza a menü mögötti oldalakat:** a szolgáltatások, referenciák, technológiák és elérhetőségek tartalma nem található a projektben. Teljes webhely-modernizációhoz ezek forrására és aktuális tartalmára is szükség lesz.

## Javasolt javítási sorrend

1. Szerezzük be a hiányzó képeket, vagy cseréljük le a képalapú megjelenést CSS-re; javítsuk az összes erőforrás-útvonalat.
2. Tisztázzuk, hogy a cél egy önálló, helyben navigálható webhely-e. Ennek megfelelően készüljenek el az aloldalak és a belső URL-ek.
3. Alakítsuk át a HTML vázát HTML5-re, adjuk hozzá a `lang`, viewport, szemantikus elemek, címsorok és képek `alt` értékeit.
4. Váltsunk reszponzív, tartalomvezérelt CSS-re; távolítsuk el a fix minimális szélességeket, a törékeny pozicionálást és az inline megjelenítési szabályokat.
5. Távolítsuk el a nem használt bővítményeket, csökkentsük a szükségtelen JavaScriptet, és frissítsük vagy váltsuk ki a régi jQuery-függőséget.
6. Egyszerűsítsük a fájlszerkezetet és a neveket; adjunk rövid README-t a futtatásról, az eszközökről és az oldal tartalmi forrásáról.
7. Ellenőrizzük a működést mobilon és asztali nézetben, billentyűzettel, képernyőolvasóval, valamint törött hivatkozásokra és hiányzó erőforrásokra.