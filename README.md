# FAN Sortare R1 - PWA v3.3 COCKPIT+CAM

## Schimbari fata de v3.2

### 1. Camera reparata pentru modul AWB
**Problema veche**: in modul AWB camera nu detecta barcode-ul.
**Cauza**: ZXing folosea reader generic + rezolutie mica (640x480) + delay 500ms intre scanari.
**Fix v3.3**:
- Rezolutie ceruta explicit 1920x1080 (fallback 1280x720)
- Continuous autofocus + continuous exposure + auto white balance
- Zoom usor 1.5x pentru barcode mic (pe device-uri care suporta)
- ZXing hints: prioritizeaza Code 128 (formatul FAN), apoi Code 39, Code 93, EAN, ITF, Codabar, UPC
- TRY_HARDER activ pe ZXing (efort suplimentar de decode)
- delayBetweenScanAttempts redus de la 500ms la 100ms (5x mai rapid)
- Fallback grațios daca constraint-uri HD nu sunt suportate (sare la cerere simpla)

### 2. Verdict ramane pe ecran pana la urmatorul scan
**Inainte**: dupa scan, daca mai apasai ceva sau treceai pe alta interactiune, verdict-ul disparea.
**Acum**: verdict-ul (OK/NU + AWB + Oras + SORT/HUB/JUD + timestamp) RAMANE vizibil pana la urmatorul scan nou.
- Mecanism: variabila `verdictLocked` blocheaza `showIdle()` accidental
- Lock-ul se anuleaza automat la: start scan nou, switch mode, FORCE RELOAD
- Daca vrei sa fortezi resetul manual, schimbi mode-ul (AWB <-> ORAS)

### 3. Status camera mai descriptiv
Vechi: "Pornesc... -> Aliniaza barcode"
Nou: "PORNESC HD... -> FOCUS... ALINIAZA BARCODE -> DETECTAT: [text]"
Logul de evenimente arata acum rezolutia reala obtinuta + zoom level.

### 4. Stop camera mai curat
Cleanup explicit pentru video.srcObject (previne probleme cand redeschizi camera).

## Ce e in folder
- index.html - aplicatia (873 KB)
- zxing.js - librarie scanare
- manifest.json, sw.js, vercel.json - PWA + CORS proxy
- icon-192.png / icon-512.png - placeholder

## DEPLOY

### Pe acelasi proiect Vercel
- dashboard.vercel.com -> proiectul tau -> Deployments -> Redeploy
- SAU drag-drop folderul nou peste

### CLI
```
cd fan-sort-pwa
npx vercel --prod
```

## CRITIC dupa deploy
SW are versiune v5. Forteaza update:
1. Deschizi URL pe telefon
2. SETARI -> FORCE RELOAD -> confirma
3. Pagina reincarcata cu v3.3

## TEST in ordine

1. Audio: banner PORNESTE sus -> beep
2. Modul AWB -> apesi CAM -> ar trebui sa vezi rapid "DETECTAT" cand aliniezi un barcode
3. Camera detecteaza -> verdict ramane pe ecran (NU mai dispare)
4. Apesi din nou CAM si scanezi alt barcode -> verdict-ul vechi se inlocuieste cu cel nou
5. Daca scanezi acelasi barcode in 2 sec -> ignorat (debounce)
6. Schimbi mode pe ORAS si inapoi pe AWB -> verdict-ul se reseteaza

## Diagnostic in setari
- TEST SUNET - verifica audio S4 Square pixel
- TEST CAMERA - testeaza permission + rezolutie
- TEST API - testeaza proxy CORS

## AWB de test
- `7000107832041001F6642` (full barcode) -> instant offline -> Abrud R2 (RED)
- `7000107832041002B7000` -> Bucuresti R1 (GREEN)
- `7000107832041` (numai AWB) -> API fallback ~500ms -> Abrud R2 (RED)

## Limite reale camera

Performanta detectie depinde de telefon:
- iPhone 15 Pro / Samsung S21+: 1920x1080 60fps, focus rapid -> detectie sub 1s
- Telefoane mid-range: 1280x720 30fps, focus mai lent -> 1-3s
- Telefoane vechi (2018-): pot ramane la fallback simplu, detectie 3-5s

Pentru zone slab luminate: tap pe FLASH (icon portocaliu in cam controls).
