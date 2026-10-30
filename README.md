# xcrew-assets

The images [xcrew](https://github.com/breferrari/xcrew)'s README shows, and the script that draws most of them. They live here, not in xcrew, so the files xcrew ships don't carry them.

| File | What it is |
|---|---|
| `banner.svg`, `band.svg`, `test-result.svg`, `failures-pane.svg`, `architecture.svg` and their `-light` twins | What `mockups.py` draws: the banner, embedding `screw.png`, and the mockups in its frame and colours |
| `icon.svg` | The plugin's icon, drawn by hand: `screw.png` large on a dark rounded tile, so the orange X is what reads at small sizes |
| `social-preview.svg` | The repository's social preview, drawn by hand |
| `screw.png` | The screw the banner shows |
| `icon.png` | `icon.svg` rendered at its own 1024×1024, the file xcrew ships as its plugin icon |
| Each other `.png` | The SVG of the same name, rendered at 2x |

Each picture the README shows has a dark version and a `-light` twin, so the README shows it in the reader's theme.

## Regenerating

On a Mac with Python 3 and librsvg (`brew install librsvg`):

```sh
python3 mockups.py && python3 mockups.py --light
for f in banner band test-result failures-pane architecture; do
  rsvg-convert -z 2 $f.svg -o $f.png
  rsvg-convert -z 2 $f-light.svg -o $f-light.png
done
```

Render a hand-drawn SVG the same way after editing it, except the icon, which stays at its own size:

```sh
rsvg-convert -w 1024 -h 1024 icon.svg -o icon.png
```

## How xcrew uses it

xcrew's README names each image by its raw URL at a commit of this repository: `https://raw.githubusercontent.com/breferrari/xcrew-assets/<commit>/<file>`. A change here reaches the README only when xcrew moves that commit, in a pull request of its own, the way it pins its test bed. xcrew's CI checks this repository out at the same commit to pair `mockups.py` with the colours its mod draws, and its weekly canary fetches every image URL the README names.

To change an image: open a pull request here, then one in xcrew that moves the commit.

The first commit holds `assets/` from xcrew at commit e7546174cc741254af3375b1eb24990c33d60884, the last to change it there.

## Licence

MIT. See [LICENSE](LICENSE).
