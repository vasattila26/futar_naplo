# Futárnapló – GitHub Pages PWA

Statikus, mobilbarát futárnyilvántartó. Nem igényel Flasket, szervert, regisztrációt vagy központi adatbázist.

## Funkciók
- Egyszeri névmegadás; nincs fiók vagy jelszavas bejelentkezés.
- Műszakok: dátum, munkaidő, rendelések, borravaló nélküli bevétel, borravaló, kilométer és megjegyzés.
- Kiadások: heti költség (7 naptári napra elosztva), havi költség (az adott hónap naptári napjaira elosztva), egyszeri költség (csak a kezdőnapon).
- Napi/heti/havi/egyéni statisztika, teljes bevétel, költségek, nettó eredmény, munkaidő, kilométer és rendelésenkénti átlag.
- JSON adatmentés és visszaállítás.
- AES-256-GCM titkosított mentés, PBKDF2-SHA-256 kulcsszármaztatással.
- Offline használat a PWA első sikeres betöltése után, ha a böngésző megtartja a cache-t.

## GitHub Pages telepítés
1. Hozz létre egy GitHub repository-t, például `futarnaplo` néven.
2. A ZIP tartalmát töltsd fel a repository **gyökérkönyvtárába**. Az `index.html` közvetlenül a gyökérben legyen, ne egy további almappában.
3. A repositoryban nyisd meg: **Settings → Pages**.
4. A **Build and deployment** résznél válaszd a **Deploy from a branch** lehetőséget.
5. Branch: `main`, mappa: `/(root)`, majd **Save**.
6. Várd meg a GitHub Pages telepítést; az URL a Pages oldalon fog megjelenni.
7. Nyisd meg a címet HTTPS-en, majd iPhone-on Safari → Megosztás → **Főképernyőhöz adás**, Androidon Chrome menü → **Alkalmazás telepítése** / **Hozzáadás a kezdőképernyőhöz**.

## Adatvédelem – fontos
- A műszakok, kiadások és a név a böngésző `localStorage` tárhelyén vannak, nem kerülnek fel GitHubra és nincsenek automatikusan szinkronizálva más eszközökre.
- A helyi adatok ebben a verzióban **nincsenek titkosítva a böngésző tárhelyén**. Az alkalmazás ugyanazon eszközön/böngészőprofilban elérhető lehet annak, aki hozzáfér a készülékhez.
- A jelszóval védett mentés AES-256-GCM-mel titkosítja a letöltött fájlt. A jelszót nem küldi el sehova. A jelszó elvesztése esetén a mentés nem fejthető vissza.
- A titkosítatlan JSON exportot csak akkor használd, ha tudatosan ezt választod, mert az olvasható szövegként tartalmazza az adatokat.
- Másik eszközön a mentési fájlt kézzel át kell vinned, majd a megfelelő jelszóval visszaállítani. Ez nem felhőszinkronizálás.
- A böngészőadatok törlése, privát böngészés vagy alkalmazásadat-törlés elveszítheti a helyi adatokat. Készíts rendszeres mentést.
- A GitHub Pages HTTPS-t használ, ami szükséges a Web Crypto titkosításhoz és a Service Workerhez.

## Fejlesztés
Nincs build lépés vagy függőség. Nyisd meg az `index.html` fájlt fejlesztéshez; az offline/PWA funkciók és a Web Crypto azonban HTTPS-en vagy localhoston működnek teljesen.
