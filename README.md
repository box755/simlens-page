# SIMLENS project page

Project page for the WACV 2027 paper *SIMLENS: Sound-Informed Multimodal LLMs for
Full-Curve Video Engagement Prediction*.

It is built on the original version of the
[Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template/tree/original-version)
(itself adapted from [Nerfies](https://nerfies.github.io)): Bulma, Google Sans for
titles, Noto Sans for text, and the template's own colours, sizes and spacing. The
template asks for a link back in the footer, which `index.html` keeps, and the website
is licensed under [CC BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/).

```
index.html                  page content: title, authors, abstract, method, demo, BibTeX
static/css, static/js       the template's files, unmodified (Bulma, Font Awesome, carousel, index.css/js)
static/css/demo.css         our additions: larger type and figures that grow with the screen, and the demo
static/js/demo.js           the replay-curve demo (video + synced chart)
static/js/examples.js       curves of the demo videos (generated)
static/images/              teaser figure, architecture figure, favicon, social preview
tools/build_examples.py     regenerates static/js/examples.js   (kept locally, not in the repository)
preview.bat                 local preview on Windows             (kept locally, not in the repository)
```

## Preview locally

YouTube embeds only work over `http://`, so the page cannot be opened as a file.

```
python -m http.server 8765
```

Then open http://localhost:8765/ . On Windows, double-click `preview.bat`.

## Published site

The site is served by GitHub Pages from the `main` branch of
[box755/simlens-page](https://github.com/box755/simlens-page) at
<https://box755.github.io/simlens-page/>.

To update it, commit and push; the site rebuilds in about a minute:

```
git add -A
git commit -m "Describe the change"
git push
```

## Things to fill in

| What | Where in `index.html` |
|---|---|
| Paper, arXiv and code links | The three buttons under the authors. Add `href` and `target="_blank"`, then delete `disabled`, `title` and the "(soon)" text. |
| Talk video | The commented "Video presentation" block near the bottom. Uncomment it and set the YouTube video ID. |
| Text and figure sizes | The "sizing" block at the top of `static/css/demo.css`. The root font size follows the window width (15px up to 1920px, growing evenly to 20px at 2560px), and everything else follows it. |

Other template building blocks (image carousel, video carousel, poster viewer) are
described in the template's own README and can be pasted back in.

## Regenerating the demo curves

`tools/build_examples.py` reads per-second predictions from the research workspace,
which is not part of this repository. Run it on the machine that has those files:

```
python tools/build_examples.py --root <simlens_pro> --baselines <simlens_baselines> --baseline-run <run folder>
```

Edit `EXAMPLES` in that file to change the videos. The script standardises every
curve within its video, computes the per-video Spearman correlation with the paper's
definitions, checks that each video can still be embedded, and writes
`static/js/examples.js`.

## Notes

- `index.html#ex=video_31465&na=1&base=1&t=45` opens a given example with the
  no-audio curve and the baseline shown, positioned at 0:45.
- The demo examples are hand-picked from the test sets. The page says so under the chart.
- Videos are embedded from YouTube through `youtube-nocookie.com`. Nothing is re-hosted.
