# Kinyerő prompt — Claude beszélgetésekből strukturált jegyzet

> Akkor használd, ha egy Claude fiókban/Projectben hónapok óta halmozódik a
> tudás chat formában, és át akarod vinni egy jegyzetrendszerbe (Obsidian vault)
> vagy egy másik fiókba. A chateket nem lehet fiókok között mozgatni — a
> következtetéseket viszont ki lehet nyerni, és csak azok érnek valamit.
>
> Nyisd meg a forrás-fiókot (vagy a Projectet), és illeszd be az alábbi blokkot.
> A `<<< >>>` részeket töltsd ki.

---

## PROMPT

Nem tanácsot kérek és nem új ötletet. **Kinyerési feladatod van.**

Ebben a Projectben / ezekben a beszélgetésekben hónapok óta gyűlik az anyag a
következő témáról: `<<<téma, pl. a főmunkám és az ügyfeleim>>>`.

Menj végig mindenen, amit erről a témáról tudsz a rendelkezésedre álló
kontextusból, és sűrítsd strukturált jegyzetté.

### Szabályok

1. **Ne találj ki semmit.** Csak azt írd le, ami tényleg elhangzott. Amit nem
   tudsz, oda írj `???`-t. A hiányzó információ hasznos — a kitalált káros.
2. **Következtetéseket adj, ne átiratot.** Nem a beszélgetés érdekel, hanem ami
   kiderült belőle: döntések, számok, nevek, megállapodások, tanulságok.
3. **Ami elavult, azt jelöld.** Ha valami megváltozott menet közben, a legfrissebb
   állapot számít — de írd oda, hogy korábban más volt.
4. **Ne szépíts.** Ha valami félbemaradt vagy kudarcba fulladt, az is információ.

### Kimeneti formátum

Témánként egy külön markdown blokk, pontosan ilyen fejléccel:

```markdown
---
status: active | paused | idea | done | killed
next_action: "egy konkrét mondat, vagy ??? "
updated: <<<mai dátum, YYYY-MM-DD>>>
type: work | hustle | project | idea | note
---

# <cím>

## Egy mondatban
Mi ez.

## Ami eddig történt
Időrendben, tényszerűen. Dátummal, ahol tudod.

## Számok, nevek, megállapodások
Konkrétumok: árak, jutalékok, határidők, kapcsolattartók.

## Nyitott kérdések
Amit el kell dönteni vagy utána kell járni.

## Amit nem tudok
Amire a beszélgetésekből nincs válasz.
```

### Végén

Zárd egy rövid listával: **mi az a 3-5 dolog, amit a beszélgetésekből nem
lehet kiolvasni, de tudni kellene** ahhoz, hogy valaki teljes képet kapjon.

Ha egy témához túl kevés az anyag, azt írd oda — ne tölts ki fejezeteket
üresen vagy találgatásból.
