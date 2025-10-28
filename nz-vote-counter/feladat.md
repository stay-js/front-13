## `<monogram>-vote-counter`

Ebben a projektben egy opcióobjektumokat tartalmazó tömböt kezelsz (`{ id, text, votes }`). Cél: gombokkal beszúrás a lista elejére vagy végére, szavazás opciókra, alap `computed` értékek megjelenítése. Használd a Vue 3 Composition API-t (`ref`, `computed`), `v-model`, `v-for`, `v-text` és mustache interpolációt. (Mustache interpoláció: órán 'bajuszoperátorként' hallhattátok, a v-text behelyettesítésére használható: `{{ valtozoneve }}`)

## 1. Tároló
- Szövegmező új opcióhoz `v-model.trim` kötésben. (Mire jó a .trim? Beszúráskor lefuttat egy String.trim()-et, amivel eltávolítja a külső szóközöket.)
- Gombok:
  - Beszúrás elejére: `unshift`, majd a mező ürítése.
  - Beszúrás végére: `push`, majd a mező ürítése.
- Üres bevitelnél ne történjen beszúrás.
- A beszúró függvény állítsa az irányt: `lastInsert = 'eleje'` vagy `lastInsert = 'vége'`.
- Opcionális: Összes törlése gomb a lista kiürítéséhez.

## 2. Tároló
- **H3**: opciók aktuális száma `computed count` alapján.
- **H5**: utolsó beszúrás iránya egyszerű állapotból.
- További `computed` értékek:
  - `totalVotes`: az összes szavazat összege.
  - `winnerText`: vezető opció logika:
    - nincs elem → „nincs”
    - minden szavazat 0 → „még nincs szavazat”
    - több maximum → „holtverseny”
    - különben a legtöbb szavazatot kapott opció szövege

## 3. Tároló
- Rács, soronként 4 kártya (Tailwind grid).
- `v-for="(opt, idx) in options"` és stabil kulcs `:key="opt.id"`.
- Kártyán jelenjen meg:
  - opció szövege `v-text`-tel,
  - aktuális szavazatszám,
  - valamint egészítsd ki a minta szerinti opciókkal
- Kártyagombok:
  - Szavazok: növeli `opt.votes` értékét 1-gyel.
  - Nulla: `opt.votes = 0`.
  - Törlés: eltávolítás az index alapján (`splice(idx, 1)`).

## Mi kell a kiváló teljesítéshez?
- A két beszúró gomb a megfelelő helyre szúr és a mező ürül.
- A `count`, `totalVotes`, `winnerText` helyesen frissül.
- A kártyákon a szöveg látható.
- Szavazás, nullázás és törlés kártyánként működik.