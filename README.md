# FAN Sortare R1 - PWA v3.3.1 INLINE (zxing fix)

## De ce inline?
Versiunea v3.3 incarca `zxing.js` ca fisier separat. Daca acest fisier nu se serveste corect (cache vechi service worker, upload incomplet pe GitHub, sau alte probleme de retea), aplicatia da "ZXing nu s-a incarcat" si camera nu functioneaza.

**v3.3.1 incorporeaza ZXing DIRECT in index.html** (un singur fisier 1.3 MB). Nu mai e nimic separat de incarcat. Imposibil sa pice.

## Ce e in folder
- `index.html` - aplicatia + ZXing inline (1.3 MB)
- `manifest.json`, `sw.js`, `vercel.json` - PWA + CORS proxy
- `icon-192.png` / `icon-512.png` - iconite

**NU mai exista zxing.js separat** - asta e diferenta cheie.

## Deploy

### Pe acelasi proiect GitHub/Vercel
1. Mergi in GitHub repo r1-fan
2. Sterge fisierul `zxing.js` (nu mai e necesar)
3. Inlocuieste `index.html` cu cel nou din acest folder
4. Inlocuieste `sw.js` cu cel nou (versiune cache bumped la v6)
5. Vercel re-deploy automat in 30 sec

### Sau prin Vercel CLI
```
cd fan-sort-pwa-inline
npx vercel --prod
```

## CRITIC dupa deploy

Service worker cache versiune v6. Pe telefon:

1. Inchizi orice PWA instalat (delete daca a fost adaugat pe home screen)
2. Deschizi `https://r1-fan.vercel.app/?v=331` (cu parametrul ?v=331 - forteaza incarcare proaspata)
3. SETARI -> FORCE RELOAD -> confirma
4. Pagina se reincarca cu v3.3.1 INLINE

## TEST in ordine

1. Audio: banner PORNESTE sus -> beep
2. SETARI -> TEST CAMERA -> ar trebui sa scrie "ZXing: incarcat" (nu mai zice "lipsa")
3. Mod AWB -> CAM -> camera porneste fara erori
4. Verdict ramane vizibil pana la urmatorul scan

## AWB de test
- `7000107832041001F6642` -> instant offline Abrud R2
- `7000107832041002B7000` -> Bucuresti R1
- `7000107832041` -> API fallback Abrud
