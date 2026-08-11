---
layout: page
title: Rupert's problem
permalink: /projects/ruperts-problem/
description: A 350-year-old question about holes in polyhedra, settled with 10,000 lines of C++.
img:
importance: 1
category: research
---

Prince Rupert of the Rhine won a bet in the 1600s by showing that a cube has a hole
cut through it large enough for a second, equally large cube to pass. The obvious
follow-up question stayed open for three and a half centuries: does *every* convex
polyhedron have this property?

Since June 2024 I have been settling it. The proof is heavily computer-assisted —
over 10,000 lines of C++ built on interval arithmetic, so that every floating-point
result carries a rigorous bound rather than a hopeful number. Getting there needed
novel solutions to a series of sub-problems that turned out to be interesting in
their own right, and something on the order of a thousand hours of independent work.

A preprint is in progress. Until then, the honest summary is: solved, being written up.

- **Language:** C++ for the search and the proof, TypeScript for visualising it
- **Key technique:** interval arithmetic to bound floating-point inaccuracy
- **Status:** preprint in progress

When there is something to turn and look at in a browser, it will appear under
[apps](/apps/).
