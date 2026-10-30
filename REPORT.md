A dékáni hivatal „működő” kapcsolati űrlapja – hibariport
Repó: https://github.com/markbocskai/bughunt1
Készítette: Bocskai Márk-László, Informatică

1. hiba
Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia): Megnyitáskor képernyőolvasóval (NVDA / VoiceOver) a szintetizátor angol kiejtéssel olvassa fel a magyar szöveget, így az teljesen érthetetlenné válik.

Gyökérok (melyik sor, melyik szabály sérül): index.html 2. sor: A <html> tagből hiányzik a lang attribútum (WCAG 3.1.1 Language of Page).

Javítás (commit link, előtte/utána kódrészlet):

Előtte: <html>

Utána: <html lang="hu">

Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó): VoiceOver képernyőolvasóval felolvastatva, valamint Chrome DevTools Lighthouse Accessibility audit futtatásával.

Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium): WCAG 3.1.1 – A dokumentum alapértelmezett nyelvét mindig meg kell adni a html elemben.

2. hiba
Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia): Képernyőolvasóval a fejlécre navigálva a logó tartalmának leírása helyett a nyers fájlnév („logo.png”) kerül felolvasásra.

Gyökérok (melyik sor, melyik szabály sérül): index.html 10. sor: Az <img> elem nem tartalmaz alt attribútumot (WCAG 1.1.1 Non-text Content).

Javítás (commit link, előtte/utána kódrészlet):

Előtte: <img src="logo.png" width="120" height="40">

Utána: <img src="logo.png" alt="ÁOK Dékáni Hivatal logója" width="120" height="40">

Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó): W3C Markup Validation Service ellenőrzéssel és képernyőolvasós bejárással.

Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium): WCAG 1.1.1 – Minden nem szöveges tartalomhoz kötelező alternatív szöveget biztosítani.

3. hiba
Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia): A főcím („Kapcsolatfelvétel”) fekete színű marad a böngészőben a várt zöld szín helyett.

Gyökérok (melyik sor, melyik szabály sérül): style.css 3. sor: .cim { colour: #0e7c66; font-size: 2rem; } – A colour brit helyesírású szó érvénytelen CSS tulajdonságnév, a böngésző eldobja.

Javítás (commit link, előtte/utána kódrészlet):

Előtte: colour: #0e7c66;

Utána: color: #0e7c66;

Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó): Chrome DevTools Inspect Element panelén az érvénytelen CSS szabály figyelmeztetésének ellenőrzésével.

Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium): A CSS szabvány szigorúan az amerikai angol color szintaxist fogadja el.

4. hiba
Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia): Mobilböngészőben az e-mail mezőre kattintva a sima billentyűzet jelenik meg (@ gomb nélkül), és a form hibás e-mail címet (pl. „alma”) is enged beküldeni.

Gyökérok (melyik sor, melyik szabály sérül): index.html 16. sor: <input type="text" name="email" ...> – type="text" van megadva type="email" helyett.

Javítás (commit link, előtte/utána kódrészlet):

Előtte: <input type="text" name="email" placeholder="E-mail cím" required>

Utána: <input type="email" id="email" name="email" placeholder="E-mail cím" required>

Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó): Chrome Device Mode mobil emulációval és form-validáció tesztelésével.

Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium): Megfelelő HTML5 input típusok használata javítja a mobil felhasználói élményt és automatikus validációt biztosít.

5. hiba
Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia): Tab billentyűvel navigálva a Küldés gombra kétszer kell Tab-ot nyomni, a W3C validátor pedig súlyos szerkezeti hibát jelez.

Gyökérok (melyik sor, melyik szabály sérül): index.html 22. sor: <a href="#"><button>Küldés</button></a> – A gomb egy hivatkozás (<a>) elemen belülre van ágyazva, ami érvénytelen HTML szerkezet.

Javítás (commit link, előtte/utána kódrészlet):

Előtte: <a href="#"><button>Küldés</button></a>

Utána: <button type="submit">Küldés</button>

Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó): W3C HTML Validator futtatásával és billentyűzetes Tab-bejárással.

Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium): Szemantikus HTML: űrlap beküldésére kizárólag a button[type="submit"] való, interaktív elemeket nem ágyazunk egymásba.

6. hiba
Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia): Képernyőolvasó használatakor a mezőbe lépve csak annyi hallatszik, hogy „szerkesztés, üres” vagy „szerkesztés, Teljes név”, gépelés után pedig a mező azonosítója teljesen eltűnik.

Gyökérok (melyik sor, melyik szabály sérül): index.html 15–21. sorok: Hiányoznak a <label> elemek és az id attribútumok (WCAG 1.3.1 Info and Relationships, WCAG 4.1.2 Name, Role, Value).

Javítás (commit link, előtte/utána kódrészlet):

Előtte: <input type="text" name="nev" placeholder="Teljes név" required>

Utána:

HTML
<div class="form-group">
  <label for="nev">Teljes név</label>
  <input type="text" id="nev" name="nev" placeholder="Teljes név" required>
</div>
Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó): Lighthouse Accessibility audit futtatásával és képernyőolvasóval.

Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium): WCAG 1.3.1 – A placeholder nem helyettesíti a címkét; explicit <label> elemeket kell használni for attribútummal kötve.

7. hiba
Hiba leírása és reprodukálása (lépések, böngésző, segédtechnológia): Billentyűzettel (Tab / Shift+Tab) történő navigáció során egyáltalán nem látható, hogy éppen melyik mezőn vagy gombon áll a fókusz.

Gyökérok (melyik sor, melyik szabály sérül): style.css 6. sor: input:focus, select:focus, textarea:focus, button:focus { outline: none; } – A fókuszkeret el van távolítva alternatív stílust beállítása nélkül (WCAG 2.4.7 Focus Visible).

Javítás (commit link, előtte/utána kódrészlet):

Előtte: outline: none;

Utána: outline: 2px solid #0e7c66; outline-offset: 2px;

Hogyan tesztelted (W3C validátor, Lighthouse, Tab-bejárás, képernyőolvasó): Kizárólagos billentyűzetes (Tab) navigációval.

Tanulság / érintett alapelv (pl. Szemantika előbb, stílus később; WCAG-kritérium): WCAG 2.4.7 – A látható fókuszállapot elengedhetetlen a billentyűzetet használó felhasználók számára.

Összegzés
Mit tanultam: Az akadálymentesség (A11y) és a helyes HTML/CSS szemantika elengedhetetlen az alapvető használhatósághoz. A vizuális stílusok és placeholder-ek nem helyettesíthetik a strukturális HTML elemeket és a billentyűzetes visszajelzéseket.

Melyik alapelv sérült a leggyakrabban: A WCAG akadálymentességi irányelvek (érvényes fókuszállapotok, nyelvi beállítások, explicit label-ek hiánya).