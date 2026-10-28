<p align="center">
  <a href="https://studioartepuma.it" target="blank"><img src="app_logo.png" width="600" alt="Studio Arte Puma" /></a>
</p>

<p align="center">
Sito di Emanuele Puma, pittore e scultore: il percorso delle opere come una serie di manifesti d'affissione.
</p>
<p align="center">
  <a href="https://github.com/heyatomdev/puma-arts/actions/workflows/test.yml"><img alt="Test" src="https://github.com/heyatomdev/puma-arts/actions/workflows/test.yml/badge.svg"></a>
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-blue"></a>
</p>

## Stack

- **Nuxt 4** + Vue 3, CSS puro (niente framework UI), **GSAP** per il percorso a pareti
- **@nuxtjs/i18n**: italiano su `/`, inglese su `/en`
- Immagini servite da **FileHarbor**, analytics Umami self-hosted
- Nessun backend né DB: le opere sono file TS in `app/data/`, le pagine prerenderizzate in build e servite dal server Nitro (solo `/` è dinamica, per il redirect di lingua)

## Sviluppo

Richiede Node 24 e pnpm 10.

```bash
pnpm install
pnpm dev                      # http://localhost:3000
pnpm build                    # stesso check della CI
node .output/server/index.mjs
```

## Contenuti

| Cosa | Dove |
|---|---|
| Opere (ordine, testi, tappe) | `app/data/artworks.ts` |
| Nome, contatti, ritratto | `app/data/site.ts` |
| Testi UI | `i18n/locales/{it,en}.json` |
| Immagini di condivisione | `og/`, vedi [og/README.md](og/README.md) |

Nuova opera: immagine in `public/`, riferimento in `app/data/artworks.ts`, poi

```bash
pnpm upload-images   # carica su FileHarbor e sostituisce i path (key in .env)
og/render.sh <slug>  # immagine di condivisione
```

Regole di stile, motion e contenuti: [CLAUDE.md](CLAUDE.md), [DESIGN.md](DESIGN.md), [PRODUCT.md](PRODUCT.md).

## Deploy

Ogni push esegue `pnpm build` (`.github/workflows/test.yml`). Un tag git fa partire `.github/workflows/build-image.yml`: build dell'immagine Docker e push su `registry.gitlab.com/heyatomdev/puma-arts:<tag>`.

Il banner qui sopra si rigenera da `og/app-logo.html` (comando in testa al file).

## Licenza

MIT, vedi [LICENSE](LICENSE).
