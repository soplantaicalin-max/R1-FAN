# FAN Sortare R1 - PWA v2.1 (camera fix)

## Schimbari fata de v2.0
- **ZXing inclus local** (`zxing.js`) - nu mai depinde de CDN extern
- **Buton FORCE RELOAD** in setari - curata cache + service worker
- **Buton TEST CAMERA** in setari - diagnostic pas-cu-pas

## Ce e in folder
- `index.html` - aplicatia principala
- `zxing.js` - librarie barcode scanning (385 KB, inclusa local)
- `manifest.json` - face app instalabil pe telefon
- `sw.js` - service worker (cacheaza si zxing.js)
- `vercel.json` - config Vercel (rezolva CORS la API FAN)
- `icon-192.png` / `icon-512.png` - iconite placeholder

## CRITIC: Daca ai versiunea veche deja deployed pe Vercel

Service worker-ul VECHI a cached `unpkg.com/...` (care nu mai exista in fisier).
Trebuie sa fortezi update-ul. 2 optiuni:

### Optiunea A: Force Reload din app (cel mai simplu)
1. Deschizi URL-ul vechi pe telefon
2. SETARI -> FORCE RELOAD (curata cache) -> confirma
3. Pagina se reincarca, ia versiunea noua

### Optiunea B: Sterge tot manual (daca A nu merge)
Pe Chrome Android:
1. Chrome -> meniul -> Settings -> Site settings -> All sites
2. Cauti *.vercel.app -> Clear & reset
3. Inchizi Chrome complet, redeschizi URL-ul

Pe Safari iPhone:
1. Settings (iPhone) -> Safari -> Advanced -> Website Data
2. Cauti vercel.app -> swipe left -> Delete
3. Redeschizi URL-ul

## DEPLOY (la fel ca v2.0)

### Pe acelasi proiect Vercel (recomandat)
1. Mergi pe dashboard.vercel.com -> proiectul tau
2. Deployments -> click ... pe ultimul deploy -> Redeploy
3. SAU: drag-drop folderul nou peste

### Pe Vercel CLI
```
cd fan-sort-pwa
npx vercel --prod
```

## TEST DUPA DEPLOY (in ordine)

1. FORCE RELOAD in setari (curata cache vechi)
2. TEST CAMERA in setari - citeste log-ul pas cu pas
3. Daca toate sunt verzi, butonul CAM (portocaliu) trebuie sa mearga
4. Aliniezi barcode -> beep + verdict

## Daca TEST CAMERA inca pica

Trimite-mi exact ce scrie log-ul. Probabilitati:
- isSecureContext: false -> nu ai HTTPS, verifica URL-ul
- mediaDevices: false -> browser foarte vechi sau restrictionat
- NotAllowedError -> ai refuzat permission (Chrome -> site settings -> permite camera)
- NotFoundError -> device fara camera (sau in uz de alt app)
- ZXing global: undefined -> fisierul zxing.js nu se serveste corect

## AWB de test
7000107832041 -> returneaza "Abrud" -> clasificat R2
