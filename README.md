# FAN Sortare R1 - PWA Deploy

## Ce e in folder
- `index.html` - aplicatia principala
- `manifest.json` - face app instalabil pe telefon
- `sw.js` - service worker (offline + cache)
- `vercel.json` - config Vercel (rezolva CORS la API FAN)
- `icon-192.png` / `icon-512.png` - iconite placeholder

## DEPLOY PE VERCEL (2 minute)

### Optiunea 1: drag-drop fara Git (cel mai rapid)

1. Mergi pe **https://vercel.com/new**
2. In partea de jos: "Import" sau "Deploy a folder"
   - Daca nu vezi optiunea: scroll → "Browse all templates" → "Empty"
   - Apoi tragi folderul `fan-sort-pwa` complet
3. La "Project Name" scrie ce vrei: `fan-sortare`
4. Click **Deploy**
5. Astepti ~30 secunde
6. Primesti URL: `https://fan-sortare-xxx.vercel.app`

### Optiunea 2: Vercel CLI (daca ai instalat)

```bash
cd fan-sort-pwa
npx vercel --prod
```

Urmaresti promptul, gata.

### Optiunea 3: GitHub + Vercel (daca preferi)

1. Creezi repo pe github cu fisierele din folder
2. Pe vercel.com/new → Import Git Repository → alegi repo
3. Deploy

## TEST DUPA DEPLOY

### Pe laptop browser (verificare rapida)
1. Deschizi URL-ul de la Vercel
2. Apesi **SETARI** (sus dreapta)
3. La "Mediu detectat" trebuie sa vezi:
   - Secure: DA
   - ZXing: incarcat
   - API base: /api/fan
4. Apesi **TEST API** - daca scrie "TEST OK: oras = Abrud" → API merge prin proxy
5. Apesi pe modul "ORAS (test)" → tastezi "Bucuresti" → ecran verde OK

### Pe Samsung S21 (test real)
1. Deschizi URL-ul in Chrome (NU Samsung Internet)
2. Test la fel ca pe laptop
3. Apesi **CAM** (butonul portocaliu) → permite camera → aliniezi un barcode
4. Pentru install ca app:
   - Chrome → meniul ⋮ (3 puncte) → **Install app** sau **Add to Home Screen**
   - Apare icon pe home screen, deschizi de acolo → fullscreen ca app nativa

### Pe iPhone (daca vrei sa testezi si acolo)
1. Deschizi URL in Safari
2. Camera ar trebui sa mearga acum (HTTPS)
3. Pentru install: Safari → Share button (patrat cu sageata) → **Add to Home Screen**

## CE TREBUIE SA TESTEZI MAINE

1. **TEST API** in setari - confirma ca API-ul merge prin Vercel proxy
   - Daca pica cu "HTTP 403" sau "Retea/CORS" → problema e la FAN si trebuie alta solutie
2. **Camera scan** pe S21 cu un barcode FAN real
3. **Sound + vibratie** - cand e OK / NU
4. **Toggle R1/R2/R3** - confirma logica de sortare
5. **Install ca app** pe home screen

## DACA API PICA

Daca TEST API zice "HTTP 403" sau alt cod de la selfawb.ro inseamna ca:
- FAN are User-Agent filtering (proxy Vercel trimite alt UA)
- Sau IP filtering (Vercel are alt IP decat browserul tau)

Solutia: facem o functie Vercel serverless (Node.js) care simuleaza exact requestul cum il face browserul. Imi spui ce eroare si fac asta.

## AWB de test
`7000107832041` → returneaza "Abrud" → clasificat R2 (NU daca ai bifat doar R1)
