# A mi naptárunk – Vercelre telepíthető közös naptár

Teljesen magyar nyelvű, sötét témájú, telefonközpontú webalkalmazás két ember közös programjaihoz. React + Vite frontend, Supabase Auth + PostgreSQL adatbázis.

## Funkciók

- E-mail/jelszó regisztráció és bejelentkezés
- Közös naptár létrehozása és csatlakozás meghívókóddal
- Hónap-, hét-, nap- és napirendnézet
- Program létrehozása, szerkesztése és törlése
- Kezdés/befejezés, egész napos program, helyszín, leírás
- Színkódok, ismétlődési beállítás és emlékeztető mező
- Programok keresése
- Sötét, telefonközpontú felület
- Közös Supabase/PostgreSQL-adatbázis és adatbázis-szintű jogosultságkezelés

## 1. Supabase-adatbázis beállítása

1. Hozz létre egy projektet a https://supabase.com oldalon.
2. Nyisd meg a **SQL Editor** felületet.
3. Másold be és futtasd a `supabase/schema.sql` teljes tartalmát.
4. Nyisd meg a Project Settings → API részt, és másold ki:
   - Project URL
   - anon / publishable klienskulcs
5. Authentication → URL Configuration alatt később add meg a Vercel-oldalad URL-jét a Site URL mezőben és az engedélyezett Redirect URLs listában.

## 2. Feltöltés GitHubra

A Vercel GitHub-repositoryból tudja a legegyszerűbben telepíteni a projektet.

1. Csomagold ki a ZIP-et.
2. Hozz létre egy új, üres repository-t a https://github.com oldalon.
3. Töltsd fel a projekt fájljait a repository gyökerébe. A `src`, `supabase`, `package.json`, `index.html`, `vercel.json` és `README.md` is legyen a gyökérben.
4. A `.env` fájlt és a titkos adatokat ne töltsd fel GitHubra.

## 3. Telepítés Vercelre

1. Nyisd meg a https://vercel.com oldalt, majd jelentkezz be GitHub-fiókkal.
2. Válaszd az **Add New → Project** lehetőséget.
3. Importáld a naptár repository-ját.
4. A projektbeállításoknál a Vercel a `vercel.json` alapján Vite-projektként fogja felismerni:
   - Build command: `npm run build`
   - Output directory: `dist`
   - Install command: `npm install`
5. A **Environment Variables** résznél add hozzá mindkét változót, Production és Preview környezethez is, ha mindkettőben használni akarod:
   - `VITE_SUPABASE_URL` = a Supabase Project URL
   - `VITE_SUPABASE_ANON_KEY` = a Supabase anon/publishable klienskulcs
6. Kattints a **Deploy** gombra.
7. A telepítés után a Vercel megad egy webcímet, például `valami.vercel.app`.

Ha a környezeti változókat a telepítés után adod hozzá vagy módosítod, indíts új redeploy-t.

## 4. Supabase hitelesítés beállítása

A Vercel-oldal elkészülte után:

1. Supabase → Authentication → URL Configuration.
2. A **Site URL** mezőbe írd be a Vercel által megadott címet.
3. Az **Additional Redirect URLs** listához is add hozzá a Vercel URL-jét, például `https://valami.vercel.app/**`.
4. Mentsd el a beállításokat.

## 5. Első használat

1. Nyisd meg a Vercel webcímet.
2. Te és a barátnőd regisztráljatok külön e-mail-címmel.
3. Az egyikőtök hozzon létre közös naptárat.
4. A másik a meghívókóddal csatlakozzon.

## Fontos megjegyzések

- Ez egy Vercelre telepíthető MVP, de az éles használathoz a Supabase-projektet és a környezeti változókat neked kell megadnod.
- A `VITE_SUPABASE_ANON_KEY` böngészőben elérhető klienskulcs; az adatokat a Supabase Row Level Security (RLS) szabályai védik. **A `service_role` kulcsot soha ne tedd a `VITE_` változók közé.**
- Az ismétlődési és emlékeztető-beállítások jelenleg elmentődnek, de a valódi automatikus ismétlődés és az értesítések még nincsenek bekötve.
- Az adatbázis Realtime bekapcsolása a SQL-ben szerepel, de az azonnali élő kliensfrissítés még nincs megvalósítva; a változások frissítés/újratöltés után biztosan lekérhetők.
- Meghívókódot csak annak adjatok meg, akit be akartok engedni a közös naptárba.
