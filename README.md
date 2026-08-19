# Handball Stats Pro — kiadások

Ez a tároló **csak telepítőket és frissítési adatokat** tartalmaz.
A forráskód külön, **privát** tárolóban él.

A telepítők a [Releases](../../releases) oldalon találhatók.

---

## version-info.json

Ez a fájl mondja meg az alkalmazásnak, hogy egy frissítés **kötelező-e**.

    {
      "minimumVersion": "1.2.0",
      "message": "Az adatbázis frissült."
    }

| Mező | Jelentés |
|---|---|
| `minimumVersion` | Ennél **régebbi** telepített verziónál az alkalmazás **kötelező** frissítést kér — nem lehet elhalasztani. |
| `message` | Opcionális indoklás. A kötelező ablakban jelenik meg. Hagyd üresen, ha nincs mondanivaló. |

### Mikor emeld a `minimumVersion`-t?

**Csak akkor**, ha egy adatbázis-változás miatt a régi verzió tényleg hibásan
működne. Ez ritka.

Ha csak új funkciót vagy javítást adsz ki, **ne nyúlj hozzá** — akkor a
felhasználók elhalasztható ajánlatot kapnak.

> **Figyelem:** ez a fájl azonnal hat minden felhasználóra. Ha elrontod és
> túl magasra állítod, mindenki kötelező frissítést fog látni. A visszaállítás
> is azonnali: írd vissza a helyes értéket, és a következő indításnál rendben lesznek.

---

## Kiadás menete

A **privát** forrás-tárolóban:

1. Emeld a verziót:

       npm version patch      # vagy: minor / major

2. Add meg a feltöltési kulcsot (a meglévő GitHub-bejelentkezésből):

       $env:GH_TOKEN = (gh auth token)

3. Építs és publikálj:

       npm run release

4. **Csak ha adatbázis-migráció is volt:** itt, ebben a tárolóban emeld a
   `minimumVersion`-t az új verzióra, és írj rövid `message`-t.

A felhasználók gépén az alkalmazás indulás után ~5 másodperccel veszi észre
az új verziót.
