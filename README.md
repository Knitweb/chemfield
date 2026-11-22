# ChemField — hydrometallurgy AI on the Knitweb

The **interactive EU steel-slag 3D logo** and web property for ChemField:
a steel-slag mineral sphere carrying the four vanadium oxidation-state domains
(V²⁺ / V³⁺ / VO²⁺ / VO₂⁺), the Si-28/29/30 isotope triangle, slag-matrix
elements (Fe/Ti/Mn/Mg/Ca/F/P), an aqueous ion cloud and a subtle Atomium/EU
motif. Self-contained canvas 2D — no dependencies.

| Path | What |
|---|---|
| [`logo/`](logo/) | the canonical interactive 3D logo (v3) |
| [`web/`](web/)  | the web property served at **5mart.ml/chemfield** by the [pulse 5mart deploy bundle](https://github.com/Knitweb/pulse/tree/main/deploy/5mart) |
| [`ms-identification/casmi26/`](ms-identification/casmi26/) | signed method graph of the public CASMI 2026 notebooks (MS/MS → structure), viewer in [`web/casmi26/`](web/casmi26/) |

Also live at [chemfield.github.io/logo](https://chemfield.github.io/logo/) and
[knitweb.art/chemfield](https://knitweb.art/chemfield/).

**Interaction:** drag the sphere = rotate · wheel / the brand line = zoom ·
Shift/Alt + drag = pan · chips toggle layers (V states, Si isotopes, slag
matrix, ions, Atomium) · double-click = reset.

## The wider ChemField stack

- [ChemField org](https://github.com/ChemField) — flagship `chemfield` pip
  package, `openchem` dataset (signed composition records, mass-balance
  validation, 5mart/OriginTrail publication path).
- Part of the [Knitweb](https://github.com/Knitweb) family — MOLGANG teaches
  the chemistry, ChemField industrialises it: EU critical raw materials,
  V₂O₅ recovery from steel slag, Si-28/29/30.

Apache-2.0.
