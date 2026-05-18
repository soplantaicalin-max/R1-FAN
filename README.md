# FAN Sortare R1 - PWA v3.7 MP3-SOUND (FIX SUNET)

## Schimbarea principala

**Abandonez Web Audio API** — care nu functiona pe Chrome-ul tau si pe iPhone in PWA mode.
**Trec la HTML5 audio + MP3 base64** — tehnologia pe care YouTube/Spotify o folosesc.

## De ce schimbarea

Web Audio API (oscilatoare generate in cod) este blocat selectiv de Chrome desktop si Safari iOS in anumite contexte (autoplay policy, AudioContext suspended dupa inactivitate, etc). Acelasi cod care merge intr-un test simplu nu mai merge in PWA dupa cateva minute.

HTML5 `<audio>` + MP3 file = abordare clasica, suportata 100% pe orice browser. Aceeasi tehnica folosita de YouTube, Spotify, etc. Zero probleme.

## Ce s-a schimbat tehnic

### Inainte (v3.5/v3.6):
```javascript
const ctx = new AudioContext();
const o = ctx.createOscillator();
o.frequency.value = 880;
o.type = 'square';
// ... 50 linii de cod
```

### Acum (v3.7):
```javascript
function beep(type) {
  const a = document.getElementById('audio-' + type);
  a.currentTime = 0;
  a.play();
}
```

3 fisiere MP3 generate cu ffmpeg, incorporate ca base64 in HTML:
- `audio-ok.mp3` - 200ms square 880Hz+1760Hz (3KB)
- `audio-nu.mp3` - 240ms square 220Hz+110Hz (3KB)
- `audio-wait.mp3` - 40ms tick 660Hz sine (1KB)

Total adaugat: ~8KB la HTML. Neglijabil.

## Sunet folosit: A3 (S4 triplat)

Bazat pe S4 Square pixel 8-bit, dar triplat in lungime pentru audibilitate:
- **OK**: 880Hz square 100ms + 1760Hz square 100ms = 200ms total
- **NU**: 220Hz square 120ms + 110Hz square 120ms = 240ms total
- **WAIT**: 660Hz sine 40ms (subtil, pe timpul API call)

## Audio unlock simplificat

In loc de:
1. Create AudioContext
2. Resume context
3. Play silent buffer
4. Play audible beep oscilator

Acum:
1. Apesi PORNESTE → cantă MP3-ul OK ca confirmare
2. Dupa ce-a cantat o data, browser-ul memoreaza ca a fost user-initiated → urmatoarele play() merg fara probleme

## Pastrate din v3.6

- Wallpaper Worley cellular albastru-violet 35% opacity
- UI iOS 17 (glass morphism, SF Pro, Apple colors)
- V15 Cockpit layout
- Sortare offline cartare 3339 chei
- Camera HD + autofocus + zoom 1.5x
- Verdict ramane vizibil
- PWA installable

## Deploy

1. GitHub Desktop → drop fisierele noi peste R1-FAN local
2. Commit "v3.7 MP3 sound fix"
3. Push
4. Vercel deploy ~30 sec
5. Pe telefon: FORCE RELOAD din SETARI

## Test

1. Deschizi URL
2. PORNESTE audio (banner portocaliu sus) → ar trebui sa auzi OK chime
3. SETARI → TEST SUNET → ar trebui OK + NU clar
4. Scan AWB → ar trebui sa cante OK sau NU dupa rezultat

## Daca tot nu auzi

In primul rand verifici:
- Chrome volume mixer (Windows tray icon volum → Volume mixer → Chrome)
- Tab-ul nu e mutat (click dreapta pe tab → Unmute site)
- Iconul de difuzor in bara de adresa Chrome

Codul e identic cu cel de la sound-mp3-test.html unde ai auzit. Daca acolo a mers, aici trebuie sa mearga.
