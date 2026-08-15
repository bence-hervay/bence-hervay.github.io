---
layout: post
title: embedding things
date: 2026-08-10 10:00:00 +0100
description: A reference post — every kind of thing this site can embed, in one place, actually working.
tags: reference
categories:
thumbnail: assets/img/2048-board.png
chart:
  chartjs: true
  plotly: true
  vega_lite: true
related_posts: false
---

A reference page, not a piece of writing: it exists so that every kind of embed is
proved working rather than promised. Anything below can be copied straight into a new
post in `_posts/`. Delete this file whenever it has stopped being useful — see the
README.

## Code, with syntax highlighting

Fenced blocks are highlighted server-side, so there is no flash of unstyled code.

```cpp
// Interval arithmetic: every result carries a bound rather than a hopeful number.
struct Interval {
    double lo, hi;

    Interval operator*(const Interval& o) const {
        const double a = lo * o.lo, b = lo * o.hi;
        const double c = hi * o.lo, d = hi * o.hi;
        return {std::min({a, b, c, d}), std::max({a, b, c, d})};
    }

    bool definitely_positive() const { return lo > 0.0; }
};
```

Inline `code` works too, and so does maths — $$\varphi = \frac{1+\sqrt5}{2}$$ — set
with MathJax:

$$
F_n = \frac{\varphi^n - (1-\varphi)^n}{\sqrt 5}
$$

## Images

Images go through `figure.liquid`, which handles responsive sizes, lazy loading and
a WebP version for browsers that want one. Add `zoomable=true` and it opens on click.

<div class="row mt-3">
    <div class="col-sm-8 mx-auto mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/2048-board.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    A 2048 board, drawn to have something real to embed.
</div>

## An embedded program

Anything that is a self-contained HTML page can be dropped into `assets/` and framed
in place — a compiled WebAssembly demo, a visualiser, a small game.

<iframe src="{{ '/assets/plotly/demo.html' | relative_url }}" frameborder="0" scrolling="no" height="500px" width="100%" style="border: 1px dashed grey;"></iframe>

## Interactive charts

Three chart libraries are wired in. Each is a fenced block of JSON — no JavaScript to
write, no build step to run.

Plotly:

```plotly
{
  "data": [
    {
      "x": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
      "y": [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89],
      "type": "scatter",
      "mode": "lines+markers",
      "name": "Fibonacci"
    }
  ],
  "layout": { "margin": { "t": 20 }, "yaxis": { "type": "log", "title": "value" }, "xaxis": { "title": "n" } }
}
```

Chart.js:

```chartjs
{
  "type": "bar",
  "data": {
    "labels": ["2", "4", "8", "16", "32", "64"],
    "datasets": [
      {
        "label": "illustrative tile counts",
        "data": [12, 9, 7, 5, 3, 1],
        "borderWidth": 1
      }
    ]
  },
  "options": { "scales": { "y": { "beginAtZero": true } } }
}
```

Vega-Lite:

```vega_lite
{
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "description": "An illustrative scatter of search depth against time.",
  "data": {
    "values": [
      {"depth": 1, "ms": 0.02}, {"depth": 2, "ms": 0.05}, {"depth": 3, "ms": 0.14},
      {"depth": 4, "ms": 0.41}, {"depth": 5, "ms": 1.2}, {"depth": 6, "ms": 3.6}
    ]
  },
  "mark": {"type": "line", "point": true},
  "encoding": {
    "x": {"field": "depth", "type": "quantitative", "title": "search depth"},
    "y": {"field": "ms", "type": "quantitative", "scale": {"type": "log"}, "title": "milliseconds"}
  }
}
```

The numbers in the last two are placeholders, chosen to make the axes do something.

## A Jupyter notebook

Notebooks are converted at build time and rendered inline, code and output together.

{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/example.ipynb' | relative_url %}
{% capture notebook_exists %}{% file_exists assets/jupyter/example.ipynb %}{% endcapture %}
{% if notebook_exists == 'true' %}
{% jupyter_notebook jupyter_path %}
{% else %}
<p>Sorry, the notebook you are looking for does not exist.</p>
{% endif %}
{:/nomarkdown}

## Links between pages

Internal links are ordinary paths: [projects](/projects/), [apps](/apps/),
[contact](/contact/), and [blog](/blog/), and the PDF at [/cv.pdf](/cv.pdf).
The CV page is the one exception — it's linked by its canonical address,
[cv](https://cv.bence.io/), rather than a path on this host.
