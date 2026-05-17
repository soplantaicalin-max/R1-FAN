# FAN Sortare R1 - PWA v3.2 COCKPIT

## Versiune finala dupa alegerile tale
- UI: **V15 Cockpit** (Bebas Neue + amber tehnic + casete cu chenare F1)
- Sound: **S4 Square pixel** (8-bit, OK 50ms / NU 80ms)
- iOS audio unlock robust (mecanismul din audio-diagnostic care merge la tine)
- Sortare offline cartare (din v3.0)
- Camera scanner (din v2.1)
- API proxy CORS (din v2.0)

## Schimbari fata de v3.0
- UI complet refacut in stil Cockpit V15
- Sunete S4 Square pixel (era beep generic)
- Audio unlock dublu: buton "PORNESTE" + auto-unlock pe primul tap
- Buton TEST SUNET in setari (pe langa TEST API + TEST CAMERA)
- City fit auto: localitati lungi (Sighet Marmatiei) scad font automat

## Ce e in folder
- index.html - aplicatia (870 KB)
- zxing.js - librarie scanare
- manifest.json, sw.js, vercel.json - PWA + CORS proxy
- icon-192.png / icon-512.png - placeholder

## DEPLOY pe Vercel

### Optiunea 1: redeploy peste proiectul existent
1. dashboard.vercel.com -> proiectul tau
2. Deployments -> ... pe ultimul deploy -> Redeploy
3. SAU drag-drop folderul nou peste

### Optiunea 2: CLI
```
cd fan-sort-pwa
npx vercel --prod
```

## CRITIC dupa deploy

Service worker are versiune noua (v4). Forteaza update:
1. Deschizi URL pe telefon
2. SETARI -> FORCE RELOAD -> confirma
3. Pagina se reincarca cu v3.2

## TEST in ordine

1. **Audio**: cand se incarca pagina apare banner portocaliu sus "AUDIO INACTIV". Apesi **PORNESTE** -> banner dispare + auzi un beep scurt. Audio e gata.
2. **TEST SUNET** in setari -> auzi OK (high pitch double) + NU (low pitch double)
3. **TEST API** -> verifica ca proxy CORS merge
4. **TEST CAMERA** -> diagnostic camera
5. Scan real cu cele 3 inputuri test:
   - `7000107832041001F6642` -> OFFLINE/F6642 instant -> Abrud R2
   - `7000107832041002B7000` -> OFFLINE/B7000 instant -> Bucuresti R1
   - `7000107832041` -> ~500ms API -> Abrud R2

## AWB de test
- `7000107832041001F6642` (full barcode) -> instant offline
- `7000107832041002B7000` -> Bucuresti R1
- `7000107832041` (numai AWB) -> API fallback

## V15 Cockpit - explicatie design

Box 1 (sus): VERDICT cu corner brackets amber (4 colturi marcate F1)
- Background: gradient subtil dupa OK/NU/wait
- Verdict urias central + glow corresponzator
- AWB number sub verdict, monospace amber

Box 2 (mid): CITY BAND inversare amber pe negru
- "DESTINATIE" label sus
- Numele orasului mare, font Bebas Neue
- Auto-fit pentru orase lungi

Box 3 (jos): SPECS grid 3 coloane cu chenar amber
- SORT (R1/R2/R3)
- HUB (agentie)
- JUD (judet)

## S4 Square pixel - sound profile

OK: 880 Hz square + 1760 Hz square (50ms total)
NU: 220 Hz square + 110 Hz square (80ms total)
Wait: 660 Hz tick (20ms)

Total latency sub 100ms (cerinta ta).
