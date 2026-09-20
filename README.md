# Ristikko

https://madebyfranz.github.io/Ristikko/

**Browser-based 2D timber truss & rafter analysis with Eurocode 5 design checks.**

Ristikko (Finnish for *truss*) is a single, self-contained HTML file — no build step, no
dependencies, no server. It analyses timber roof trusses and rafters with a real
direct-stiffness solver and checks them against EN 1990 / 1991 / 1995 (Eurocode 5),
then produces a printable calculation report.

**Live demo:** `https://<your-username>.github.io/ristikko/`

---

## What it does

- **Direct-stiffness 2D frame solver** — 3 DOF/node beam-column elements carrying axial +
  bending. Verified against textbook cases (simply-supported beam, cantilever, pin-jointed
  truss).
- **10 parametric truss types** — Fink, king post, queen post, Howe, Pratt, Fan,
  parallel-chord (flat), scissor, mono-pitch, attic/room-in-roof, and rafter + collar tie.
- **Flexible geometry** — span, rise/pitch, panel count, **asymmetric ridge position**,
  independent **left/right eave heights** (raised heel, stepped bearings, shed slopes),
  and separate sections for top chord / bottom chord / webs.
- **Load combinations (EN 1990 / 1991)** — ULS envelope over balanced and asymmetric snow
  (EN 1991-1-3) and wind uplift, with γ and ψ factors. Wind pressure `qp(z)` computed to
  EN 1991-1-4 from site wind speed, terrain category and reference height.
- **EC5 member design (EN 1995-1-1)** — tension/compression + bending interaction,
  flexural buckling (§6.3.2), lateral-torsional buckling (§6.3.3), shear (§6.1.7), and
  bearing perpendicular to grain at supports (§6.1.5), with `kmod`, `kdef` and `γM` per
  service class and load duration. Worst case per member across the whole envelope.
- **Connections (EN 1995-1-1 §8)** — dowel-type joints via Johansen yield theory (nails,
  screws, bolts/dowels; timber–timber and steel–timber, single and double shear),
  including rope effect, effective number `nef`, and minimum spacings/edge distances; plus
  punched metal-plate fasteners (§8.8, anchorage + plate capacity).
- **Interactive joint editor** — click any node to see the members framing in, their
  forces, the angle to grain relative to the through-chord, and the connection each needs.
- **Result views** — geometry + loads, axial force, bending, deflection, and a utilisation
  map, plus reactions, deflection (`w_inst` / `w_fin` with creep) and a sortable member table.
- **Printable calculation report** — one click, with embedded diagrams and the governing
  EC5 interaction equations written out with substituted numbers; print or save as PDF.
- **Save / load named designs** in the browser.

## Usage

Open `index.html` in any modern browser, or host it on GitHub Pages (Settings → Pages →
deploy from branch, root). Everything runs client-side. Saved designs are stored in the
visitor's own browser (localStorage) and are never uploaded or shared.

## Standards referenced

EN 1990 (basis of design), EN 1991-1-3 (snow), EN 1991-1-4 (wind), EN 1995-1-1 (Eurocode 5:
timber). Material properties follow EN 338 (sawn) and EN 14080 (glulam).

## Scope & limitations

This is a study and preliminary-design tool, not certified design software.

- Partial factors and `ψ` / `kmod` follow EN recommended values — **check against the
  Finnish National Annex** for real work.
- Wind: `qp(z)` is computed per EN 1991-1-4, but the net pressure coefficient is a single
  editable value, not the full roof-zone `cpe` / `cpi` breakdown.
- Metal-plate fastener values are generic placeholders — replace with the manufacturer's
  ETA data.
- Not yet included: connection splitting/block shear, notched-member and combined-stress
  special cases, fire, vibration, and second-order (large-displacement) effects.

**All results must be independently verified by a qualified structural engineer before
construction.**

## Technical

Plain HTML + vanilla JavaScript in one file (~100 KB). The solver, generators and all code
checks are hand-written; the only external resource is Google Fonts. No frameworks, no
bundler, no network calls to any backend.

## License

MIT (see `LICENSE`).
