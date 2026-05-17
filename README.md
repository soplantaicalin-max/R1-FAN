# FAN Sortare R1 - PWA v3.4 N2-SOUND

## Schimbari fata de v3.3.1
- Sunet schimbat din S4 Square pixel (50ms, prea scurt) la **N2 Notification ping** (240ms, sine wave premium)
- Service worker bumped la v7

## Profil sunet N2
- **OK**: sine wave 988Hz -> 1318Hz sweep + armonic 1976Hz, total 240ms. Sound similar cu notificare iOS.
- **NU**: sine wave 220Hz -> 110Hz descending + armonic 440Hz, total 240ms. Distinct, autoritar.
- **Wait**: sine 660Hz 40ms (subtil, pe timpul API call).

De ce N2 si nu altele:
1. Sine wave > square wave pe speakers small (iPhone, Zebra TC27)
2. 240ms - clar audibil dar nu intarzie scan urmator
3. Armonice superioare adauga warmth, suna premium
4. Pentru 8h/zi - oboseste urechea mai putin decat square waves

## Deploy
1. Sterge fisierele vechi din GitHub repo r1-fan (sau le inlocuiesti)
2. Pune fisierele noi
3. Vercel deploy automat
4. Pe telefon: FORCE RELOAD din setari, apoi PORNESTE audio

## Test rapid
- Deschide URL pe iPhone
- PORNESTE audio (banner portocaliu sus)
- SETARI -> TEST SUNET -> ar trebui sa auzi OK (high sweep up) + NU (low sweep down)
- Mod AWB -> scan
