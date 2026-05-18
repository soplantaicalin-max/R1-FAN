# FAN Sortare R1 - PWA v3.6 WALLPAPER

## Schimbari fata de v3.5

### Wallpaper static integrat
- **Imagine generativa Worley cellular** (39 KB JPEG, encoded base64 in HTML)
- Albastru-violet profund (deep navy + violet purple cells)
- **35% opacity efectiv** (overlay 55-70% negru peste)
- Structura: 80 puncte Voronoi cu ridge function -> aspect "topografic" ca inspirația ta
- Background **fix** (background-attachment: fixed) - nu se misca la scroll, premium feel

### Performance impact
- Zero performance (imagine statica, nu animatie)
- +52 KB la HTML (base64), neglijabil
- Telefoanele cache-uiesc automat

### Tot ce e in v3.5 pastrat
- Sunet 400ms premium (3 layere oscilator)
- UI iOS 17 (glass morphism, SF Pro, gradiente Apple)
- Verdict box cu dot indicators luminoase
- City band gradient amber
- Specs grid glass cards
- Audio unlock dublu
- Sortare offline cartare 3339 chei

## Deploy
1. Open GitHub Desktop
2. Drop fisierele noi peste folderul R1-FAN local
3. Commit + Push
4. Vercel auto-deploy
5. Pe telefon: FORCE RELOAD din setari -> vezi background nou

## Specs background
- Source: Worley/Voronoi cellular noise
- Output: 800x1333 JPEG, quality 78
- Format: data:image/jpeg;base64 inline in CSS
- Overlay: linear-gradient(180deg, 55% black, 70% black)
- Result: deep dark with subtle organic cellular pattern visible

## Test
- Deschizi URL pe iPhone -> FORCE RELOAD
- Verifici ca vezi pattern subtil violet in fundal (mai vizibil pe ecran intunecat)
- Verdict OK/NU trebuie sa fie cititbil clar (gradient verde/rosu peste background)
- Sound TEST SUNET pentru a verifica v3.5 audio
