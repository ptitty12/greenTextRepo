# greenTextRepo

Drop in a photo, get back one image per greentext line — ready to save and post.

```
>if only you knew how bad things really are
>some things are worth fighting for, anon
>never give up, anon
```

## Use it

Open `index.html` in a browser. That's the whole install — no build, no
dependencies, no server. The photo is decoded and drawn locally with `<canvas>`;
nothing is uploaded anywhere.

To serve it instead (any static host works):

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

### Docker

```sh
docker build -t greentext .
docker run --rm -p 8080:80 greentext   # then open http://localhost:8080
```

nginx serving one static file — the image carries `index.html` and nothing else.

### GitHub Pages

`.github/workflows/pages.yml` publishes the repo root on every push to `main`.
It only runs once Pages is switched on: **Settings → Pages → Build and
deployment → Source: GitHub Actions**. After that the tool lives at
`https://ptitty12.github.io/greenTextRepo/`.

## What it does

- **Upload** by drag-and-drop, file picker, or paste (Ctrl/Cmd+V).
- **Renders every line at once** — eight built-in classics plus anything you type.
  One line per image; separate custom blocks with a blank line to put several
  greentext lines on one image.
- **Three styles** — classic outlined greentext, greentext on a dark band, or a
  fake 4chan post box with the `Anonymous` header and post number.
- **Style the text** — font (Arial, Impact, Courier, Times, Comic Sans), any
  color via swatch or picker, left or centered, and a toggle for the leading `>`.
  The outline flips to white behind near-black text so it stays readable.
- **Position** top / middle / bottom, plus a text-size slider. Long lines shrink
  to fit before they wrap, so a punchline stays on one row.
- **Save** any image individually or all of them at once. Output is PNG, capped
  at 1600px on the long edge.

EXIF rotation is respected, so phone photos come out the right way up.

## Notes

If a save button appears to do nothing, you're probably in an embedded viewer
that blocks page-initiated downloads — right-click (or long-press) the image and
choose *Save image*. Opening `index.html` directly in a normal browser tab always
works.
