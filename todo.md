# Weboldal-modernizáció – tennivalók

## 1. Projekt és tartalom előkészítése
- [ ] Döntés: önálló, helyben navigálható webhely legyen-e a modernizált változat.
- [ ] Beszerzés: hiányzó képek, logók, galériafájlok és eredeti tartalom összegyűjtése.
- [ ] Ellenőrzés: érvényes elérhetőségi adatok, telefonszám és e-mail-cím beazonosítása.
- [ ] Megadás: szolgáltatások, referenciák, technológiák és egyéb aloldalak végleges tartalma.
- [ ] Dokumentálás: oldal célja, futtatási módja és tartalomforrásai egy rövid README-ben.

## 2. Fájlszerkezet és erőforrások
- [ ] Átnevezés: JavaScript-fájlok végződésének egységesítése `.js` kiterjesztésre.
- [ ] Átszervezés: létrehozni `assets/images/`, `css/` és `js/` mappákat.
- [ ] Áthelyezés: képek, stíluslapok és szkriptek szerepkör szerint rendezése.
- [ ] Javítás: minden elavult vagy hibás kép-, stílus- és szkriptútvonal korrigálása.
- [ ] Tisztítás: ténylegesen nem használt fájlok és fölösleges erőforrások eltávolítása.

## 3. HTML és szemantika
- [ ] Javítás: HTML5 `<!doctype html>` hozzáadása.
- [ ] Javítás: `<html lang="hu">` beállítása.
- [ ] Javítás: modern `<meta charset="UTF-8">` és viewport meta hozzáadása.
- [ ] Átalakítás: `<header>`, `<nav>`, `<main>`, `<footer>` és megfelelő szekcióelemek használata.
- [ ] Javítás: egyértelmű, hierarchikus címsorstruktúra felépítése; látható `h1` hozzáadása.
- [ ] Javítás: minden tartalmi képhez értelmes `alt` szöveget, a dekoratív képekhez üres `alt` értéket adni.
- [ ] Tisztítás: felesleges `<br>` elemek és inline stílusok lecserélése CSS-re.
- [ ] Eltávolítás: kézzel beállított HTML-magasságok megszüntetése.

## 4. Navigáció és aloldalak
- [ ] Tervezés: belső, jól érthető URL-struktúra meghatározása.
- [ ] Átalakítás: menühivatkozások helyi aloldalakra mutatására vagy egyértelmű külső URL-ek használatára.
- [ ] Létrehozás: `Főoldal`, `Bemutatkozás`, `Szolgáltatások`, `Referenciák`, `Technológiák` és `Kapcsolat` tartalma.
- [ ] Ellenőrzés: minden menüpont, belső hivatkozás és törött link működik-e.
- [ ] Javítás: aktív, hover és fókuszált menüállapotok áttekinthető CSS-sel történő kialakítása.
- [ ] Biztonság: külső hivatkozásokhoz `rel="noopener"` és új laphivatkozáshoz egyértelmű jelzés adása.

## 5. CSS és reszponzív kialakítás
- [ ] Átalakítás: fix 1010 px minimális szélesség és rögzített elrendezés eltávolítása.
- [ ] Átalakítás: tartalomvezérelt, rugalmas elrendezés készítése CSS Grid/Flexbox segítségével.
- [ ] Javítás: mobil, tablet és asztali töréspontok definiálása.
- [ ] Javítás: alapbetűméret, sortáv és sorköz olvashatóvá alakítása.
- [ ] Eltávolítás: abszolút pozicionálás, negatív margók és törékeny képmagasságok átdolgozása.
- [ ] Átalakítás: képsprite-alapú navigáció CSS-alapú vagy egyszerű szöveges menüre cserélése.
- [ ] Tisztítás: elavult CSS-szintaxis, felesleges prefixek és nem használt galériastílusok eltávolítása.
- [ ] Cserélés: hiányzó hátterekhez és ikonokhoz helyi képek vagy modern CSS formák beállítása.
- [ ] Ellenőrzés: hosszabb szöveg, nagyobb betűméret és eltérő kijelzőarányok hibamentes megjelenítése.

## 6. JavaScript és függőségek
- [ ] Áttekintés: minden szkript használata és tényleges szükségességének ellenőrzése.
- [ ] Eltávolítás: jQuery, `mousewheel` és `infieldlabel` bővítmények, ha már nem szükségesek.
- [ ] Frissítés: csak valóban szükséges modern függőség megtartása vagy natív JavaScript használata.
- [ ] Átalakítás: tömörített `main.js.letöltés` tartalmának olvasható, dokumentált JavaScriptbe helyezése.
- [ ] Eltávolítás: user-agent alapú böngészőazonosítás.
- [ ] Eltávolítás: menükattintásokhoz kötött JavaScript-átirányítás, alapértelmezett hivatkozások megtartása.
- [ ] Eltávolítás: képek előtöltéséhez és futásidejű kézi méretezéshez használt fölösleges kód.
- [ ] Ellenőrzés: fő tartalom és navigáció JavaScript nélkül is használható legyen.

## 7. Kereshetőség és megosztás
- [ ] Javítás: rövid, természetes nyelvű meta description létrehozása.
- [ ] Megadás: végleges canonical URL beállítása minden oldalon.
- [ ] Megadás: releváns Open Graph cím, leírás és megosztási kép beállítása.
- [ ] Létrehozás: `robots.txt` és, ha több oldal készül, XML sitemap.
- [ ] Ellenőrzés: oldalcímek egyediek, relevánsak és címsorra épülnek.

## 8. Megvalósítás és tesztelés
- [ ] Megvalósítás: HTML-, CSS- és JavaScript-átszervezés lépésenkénti, visszakereshető változtatásokkal.
- [ ] Futtatás: helyi szerver vagy egyszerű statikus publikálási mód dokumentálása.
- [ ] Ellenőrzés: mobil, tablet és asztali nézetek áttekintése.
- [ ] Ellenőrzés: billentyűzetes navigáció, látható fókusz és logikus tab-sorrend.
- [ ] Ellenőrzés: képernyőolvasóval értelmezhető címsor-, lista-, link- és képleírás-struktúra.
- [ ] Ellenőrzés: törött képek, hibás útvonalak, 404-es oldalak és hibás hivatkozások.
- [ ] Ellenőrzés: színek, betűméret, kontraszt és szöveg nagyítási viselkedése.
- [ ] Tesztelés: népszerű modern böngészőkön és különböző képernyőméreteken.
- [ ] Dokumentálás: ismert korlátozások és későbbi fejlesztési lehetőségek feljegyzése.
