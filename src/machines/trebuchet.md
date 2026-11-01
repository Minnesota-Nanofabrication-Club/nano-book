{{#title T-2 Trebuchet — Operator and Design Manual}}

<!--
mdBook — page setup

This page is a single-file feature test. Save it as `trebuchet.md`; the
self-includes near the bottom read this file by name.

Required `book.toml` keys:

    [output.html]
    mathjax-support = true          # loads MathJax for the math below

    [output.html.code.hidelines]
    python = "~"                    # `~` hides a line in python blocks

`\{{#title ...}}` on line 1 sets the browser-tab <title>. The sidebar keeps
the name given in SUMMARY.md. The directive is removed from the output.

HTML comments such as this one are passed through to the generated HTML.
They are invisible on the page but present in the page source, so they are
not a place for anything private.
-->

# T-2 Bench Trebuchet { #t2 .doc-title }

<!--
mdBook — heading attributes

`{ #id .class }` after a heading sets its HTML id and adds classes. The id
replaces the auto-generated anchor (here it would have been
`t2-bench-trebuchet`), so links survive a rename. Classes have no effect
unless styled through `additional-css` in book.toml.
-->

<!--
mdBook — raw HTML and float classes

Inline HTML is passed through unchanged. mdBook's stylesheet defines
`.left` and `.right` (float) and `.hidden` (display: none). Click-to-zoom
applies to <img> elements only, so this inline <svg> does not zoom.
-->

<svg class="right" width="230" viewBox="0 0 230 170" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="T-2 side elevation"><line x1="5" y1="160" x2="225" y2="160" stroke="#555" stroke-width="2"/><polygon points="80,160 115,70 150,160" fill="none" stroke="#7a5230" stroke-width="5" stroke-linejoin="round"/><line x1="95" y1="125" x2="135" y2="125" stroke="#7a5230" stroke-width="3"/><line x1="25" y1="152" x2="80" y2="152" stroke="#7a5230" stroke-width="3"/><line x1="115" y1="70" x2="35" y2="140" stroke="#a0703c" stroke-width="6" stroke-linecap="round"/><line x1="115" y1="70" x2="140" y2="48" stroke="#a0703c" stroke-width="6" stroke-linecap="round"/><line x1="140" y1="48" x2="140" y2="62" stroke="#333" stroke-width="2"/><rect x="126" y="62" width="28" height="26" fill="#888" stroke="#333"/><path d="M35,140 Q50,152 64,151" fill="none" stroke="#333" stroke-dasharray="3 2"/><circle cx="68" cy="151" r="5" fill="#c33"/><circle cx="115" cy="70" r="4"/><text x="160" y="80" font-size="10" font-family="sans-serif">counterweight</text><text x="122" y="64" font-size="10" font-family="sans-serif">axle</text><text x="8" y="120" font-size="10" font-family="sans-serif">arm</text></svg>

The T-2 is a hinged-counterweight bench trebuchet built for range
demonstrations and teaching. It throws a regulation softball roughly 70 m
on level ground. This manual covers specifications, theory of operation,
the firing procedure, tuning, the range simulator, and maintenance.

<!--
mdBook — admonitions (mdBook 0.5+, `output.html.admonitions`, default on)

A blockquote whose first line is [!NOTE], [!TIP], [!IMPORTANT], [!WARNING]
or [!CAUTION] renders as a titled callout box. All five appear on this page.
On mdBook 0.4 these render as plain blockquotes with the tag as text.
-->

> [!NOTE]
> This manual describes revision C (hinged counterweight). Revision B
> machines have a fixed counterweight; see [Revision history](#revisions).

## Specifications { #specs }

<!--
mdBook — tables

GitHub-style pipe tables. The colons in the delimiter row set alignment:
`:--` left, `:-:` centre, `--:` right.
-->

| Parameter | Symbol | Value | Unit |
|:----------|:------:|------:|:-----|
| Counterweight mass | \\( M \\) | 45 | kg |
| Projectile mass (softball) | \\( m \\) | 0.18 | kg |
| Projectile diameter | \\( d \\) | 0.097 | m |
| Arm length, overall | — | 1.80 | m |
| Arm ratio, long : short | — | 4 : 1 | — |
| Counterweight drop | \\( \Delta h \\) | 0.60 | m |
| Release height | \\( y_0 \\) | 2.0 | m |
| Measured efficiency | \\( \eta \\) | 0.50 | — |
| Launch speed | \\( v \\) | 38 | m/s |
| Range, level ground | \\( R \\) | 70 ± 5 | m |

<!--
mdBook — inline math

Inline math uses `\\(` and `\\)`. The doubled backslash survives Markdown
escape processing as a single backslash, which MathJax then reads. Stock
mdBook does not support `$...$` for inline math. With the mdbook-katex
preprocessor, `$...$` works and single backslashes are used throughout.
-->

## Theory of operation { #theory }

### Energy budget

The counterweight is the only energy source. Lowering its centre of mass
through \\( \Delta h \\) releases

<!--
mdBook — display math

Display equations here use `$$` on their own lines. mdBook itself does not
recognise `$$`; MathJax's default configuration does, when it scans the
rendered page. Markdown still processes the text between the delimiters
first, so:

  * TeX commands made of a backslash and punctuation must be doubled,
    `\\,` and `\\;`, or Markdown consumes the backslash;
  * a `\\` line break must be written `\\\\`;
  * a line inside the block must not begin with `-`, `+`, `#` or `>`,
    or Markdown starts a list, heading or blockquote;
  * with smart punctuation on, `'`, `"`, `--` and `...` are converted to
    typographic characters, so use `\prime`, `\dots`, etc.

The equations below are written to avoid all four.
-->

$$
E = M g \Delta h
$$

Not all of this reaches the projectile. Energy remains in the swinging arm
and counterweight, in frame vibration, and in friction at the axle and
trough.[^denny] The losses are lumped into a single efficiency
\\( \eta \\), measured for each machine (see [Tuning](#tuning)):

$$
\tfrac{1}{2} m v^2 = \eta M g \Delta h
\quad\Longrightarrow\quad
v = \sqrt{\frac{2 \eta M g \Delta h}{m}}
$$

Launch speed grows with \\( \sqrt{M/m} \\). Doubling the counterweight
raises speed by about 41 %, not 100 %.

### Range without air resistance

For release at height \\( y_0 \\) and angle \\( \theta \\) above horizontal:

$$
R_{\text{vac}} = \frac{v \cos\theta}{g} \left( v \sin\theta + \sqrt{v^2 \sin^2\theta + 2 g y_0} \right)
$$

At \\( y_0 = 0 \\) this reduces to \\( v^2 \sin 2\theta / g \\), with a
maximum at 45°.

### Range with air resistance { #drag }

A softball at 38 m/s is above its terminal velocity, so drag dominates
the flight. The simulator integrates

$$
m \frac{d\mathbf{v}}{dt} = m\mathbf{g} + \mathbf{F_{\text{drag}}},
\qquad
\mathbf{F_{\text{drag}}} = -\tfrac{1}{2} \rho C_D A \lvert \mathbf{v} \rvert \mathbf{v}
$$

<!--
mdBook — subscripts after a closing brace

Markdown can treat `_` as emphasis when it follows a closing brace, as in
`\mathbf{F}_{x}`; two such underscores in one paragraph italicise the text
between them and break the equation. Keep the subscript inside the braces,
`\mathbf{F_{x}}`, or follow the underscore from a letter, `F_{x}`.
-->

where air density is
\\( \rho = 1.204 \\) kg/m³, \\( C_D \approx 0.47 \\) for a
sphere,[^cd] and frontal area \\( A = \pi d^2 / 4 \\).

| Case | Best angle | Range |
|:-----|-----------:|------:|
| No drag | 44.6° | 152 m |
| With drag | 38.6° | 72 m |

Drag roughly halves the range and lowers the optimum release angle. Tune
for about 39°, not 45°.

## Firing procedure { #procedure }

<!--
mdBook — Font Awesome

mdBook bundles Font Awesome 6 (free: solid, regular, brands). The
`<i class="fa-...">` syntax is converted to inline SVG at build time.
-->

<i class="fa-solid fa-triangle-exclamation"></i> Read this section in full
before operating the machine.

> [!CAUTION]
> Clear the downrange area to 120 m and 30 m either side of the line of
> fire. A premature release can throw the projectile upward or backward.

### Pre-fire checklist

<!--
mdBook — task lists

`- [ ]` and `- [x]` render as disabled checkboxes. They are not
interactive and do not persist state. Nested items need four spaces.
-->

- [ ] Frame pins seated and safety-clipped
- [ ] Axle bearings greased this session
- [ ] Sling cords free of fraying; pouch stitching intact
- [ ] Release pin angle checked against the tuning log
- [ ] Trigger latch engaged before the arm is loaded
    - [ ] Latch lanyard routed clear of the arm path
- [ ] Range clear; spotter in position

### Firing

1. Winch the arm down until the trigger latch engages. Release winch tension.
2. Lay the sling in the trough with the projectile in the pouch.
3. Hook the fixed sling loop to the arm tip and the free loop over the release pin.
4. Call "clear" and wait for the spotter's acknowledgement.
5. Pull the lanyard from the side position.

> [!WARNING]
> Never release the trigger with an empty sling (a "dry fire"). Without a
> projectile to absorb it, the full counterweight energy goes into the
> frame and axle.

## Tuning { #tuning }

> [!IMPORTANT]
> Change one variable per session — pin angle *or* sling length — and log
> every shot. Two simultaneous changes cannot be separated afterwards.

The release pin sets the release angle. Bending the pin forward releases
earlier and raises the trajectory; bending it back flattens it. Start at
the pin angle in the tuning log and adjust in 5° steps.

> [!TIP]
> If the projectile lands short and high, the release is early: bend the
> pin back. If it lands short and low or hits the trough, the release is
> late: bend it forward.

Efficiency is computed from a measured launch speed (high-speed video or a
chronograph):

<!--
mdBook — hidelines for non-Rust languages

Python has no built-in hidden-line prefix. With
`[output.html.code.hidelines] python = "~"` in book.toml, lines starting
with `~` are hidden and the `~` is removed; the eye icon reveals them.
`#` is not used because it would hide every Python comment.
-->

```python
~import math
~
~G = 9.81  # m/s^2
def efficiency(v_measured, M=45.0, m=0.18, drop=0.60):
    """Fraction of counterweight energy delivered to the projectile."""
    return m * v_measured**2 / (2 * M * G * drop)
~
~print(f"eta = {efficiency(38.4):.2f}")
```

<!--
mdBook — per-block hidelines override

`python,hidelines=<prefix>` replaces the book-wide prefix for one block.
-->

```python,hidelines=%
%import math
def launch_speed(M, m, drop, eta, g=9.81):
    return math.sqrt(2 * eta * M * g * drop / m)
```

## Range simulator { #simulator }

The simulator predicts launch speed and range from the machine parameters.
Its source is maintained alongside this manual.

<!--
mdBook — `\{{#include}}` by anchor

The parameter block below is not written here. It is pulled from the
program kept in an HTML comment at the end of this file, between
ANCHOR / ANCHOR_END marker lines named `params`. Marker lines may sit
inside any comment syntax; nested markers are stripped from the output.
Anchors survive edits to the file; line numbers do not.
-->

Parameters for revision C:

```rust,noplayground
{{#include trebuchet.md:params}}
```

<!--
mdBook — `\{{#include}}` by line number

`file:N` includes line N only. Other forms: `file::N` (lines 1 to N),
`file:N:` (N to end), `file:A:B` (A to B). This form breaks whenever lines
above the target are added or removed, which is why anchors are preferred.
-->

Air density used by the drag model:

```rust,ignore
{{#include trebuchet.md:616}}
```

The drag integrator:

```rust,ignore
{{#include trebuchet.md:drag}}
```

<!--
mdBook — Rust playground and hidden lines

A plain ```rust block gets a play button that sends the code to
play.rust-lang.org. Lines beginning `# ` (or a lone `#`) are hidden until
the reader clicks the eye icon, but are still sent to the playground and
compiled by `mdbook test`. The full program below is included by anchor;
its `use` line is hidden. A block without `fn main` is wrapped in one
automatically.
-->

Full program:

```rust
{{#include trebuchet.md:program}}
```

Expected output:

```text
launch speed        38.4 m/s
range, no drag, 45   152 m
range, drag, 45       71 m
best angle (drag)   38.6 deg (72 m)
```

<!--
mdBook — code-block attributes

Attributes follow the language, separated by commas or spaces:

  editable              reader can edit the code in place
  noplayground          no play button; still run by `mdbook test`
  ignore                not tested, not runnable; highlighted only
  mdbook-runnable       forces the play button (pair with `ignore`)
  should_panic          test passes only if the code panics
  no_run                compiled by `mdbook test`, never executed
  compile_fail          test passes only if compilation fails
  edition2015 .. edition2024   override `[rust] edition` for this block

Each one is used once below.
-->

### Quick calculation

Edit the values and press run:

```rust,editable,edition2024
fn main() {
    let (m_cw, m_proj, drop, eta) = (45.0_f64, 0.18, 0.60, 0.50);
    let v = (2.0 * eta * m_cw * 9.81 * drop / m_proj).sqrt();
    println!("launch speed: {v:.1} m/s");
}
```

### Unit conversion

Scale readings in the shop are in pounds:

```rust,noplayground
/// Pounds to kilograms (exact by definition).
fn lb_to_kg(lb: f64) -> f64 {
    lb * 0.453_592_37
}
assert!((lb_to_kg(100.0) - 45.359_237).abs() < 1e-9);
```

### Parameter validation

The simulator rejects physically meaningless input:

```rust,should_panic
# fn launch_speed(m_proj: f64) -> f64 {
#     assert!(m_proj > 0.0, "projectile mass must be positive");
#     (2.0 * 0.5 * 45.0 * 9.81 * 0.6 / m_proj).sqrt()
# }
fn main() {
    launch_speed(0.0); // panics: projectile mass must be positive
}
```

Parameters are passed by shared reference and cannot be modified by the
simulator:

```rust,compile_fail
# struct Params { efficiency: f64 }
fn tune(p: &Params) {
    p.efficiency = 0.6; // error[E0594]: cannot assign through a `&` reference
}
# fn main() {}
```

### Shot-to-shot dispersion

Release timing and counterweight swing vary slightly between shots. This
estimate perturbs efficiency and release angle and reports the spread.
Its output differs on every run.

```rust,ignore,mdbook-runnable
use std::time::{SystemTime, UNIX_EPOCH};

fn main() {
    let mut seed = SystemTime::now().duration_since(UNIX_EPOCH).unwrap().as_nanos() as u64;
    let mut rand = || {
        seed = seed.wrapping_mul(6364136223846793005).wrapping_add(1442695040888963407);
        (seed >> 11) as f64 / (1u64 << 53) as f64 // uniform in [0, 1)
    };
    let (g, y0) = (9.81_f64, 2.0);
    let mut ranges: Vec<f64> = (0..1000)
        .map(|_| {
            let eta = 0.50 + 0.04 * (rand() - 0.5);
            let theta = (39.0 + 4.0 * (rand() - 0.5)).to_radians();
            let v = (2.0 * eta * 45.0 * g * 0.6 / 0.18).sqrt();
            let (s, c) = theta.sin_cos();
            v * c / g * (v * s + (v * v * s * s + 2.0 * g * y0).sqrt())
        })
        .collect();
    ranges.sort_by(f64::total_cmp);
    println!("drag-free range, 5th to 95th percentile: {:.0} to {:.0} m",
             ranges[50], ranges[950]);
}
```

<!--
mdBook — why `ignore` here

The output is random by design, so it is excluded from `mdbook test`.
`mdbook-runnable` keeps the play button that `ignore` would remove.
-->

### Release telemetry (firmware)

The arm-angle logger polls a Hall-effect encoder on the axle. It runs until
power-off, so it is compiled but never executed in documentation tests:

```rust,no_run
use std::time::{Duration, Instant};

fn read_arm_angle_deg() -> f64 {
    0.0 // replaced by the encoder driver on target
}

fn main() {
    let t0 = Instant::now();
    loop {
        let angle = read_arm_angle_deg();
        println!("{:>8.3} s  {:>6.1} deg", t0.elapsed().as_secs_f64(), angle);
        std::thread::sleep(Duration::from_micros(500));
    }
}
```

The firing sequence implemented by the controller, in outline:

```rust,ignore
match state {
    Idle      => if latch.engaged() && range.clear() { state = Armed },
    Armed     => if lanyard.pulled() { trigger.release(); state = Fired },
    Fired     => if arm.at_rest() { log.write(shot); state = Idle },
}
```

### Running the simulator locally

```bash
cargo run --release --bin t2-sim
```

```toml
# t2-sim.toml: override any parameter of T2_REV_C
efficiency = 0.48
release_height_m = 2.1
```

## Maintenance { #maintenance }

| Interval | Task |
|:---------|:-----|
| Every session | Inspect sling cords and pouch; grease axle bearings |
| Every 50 shots | Check frame pins and gussets for cracking |
| Every 200 shots | Replace sling cords; re-measure efficiency |
| Annually | Disassemble axle; inspect bearing races |

## Revision history { #revisions }

<!--
mdBook — strikethrough and smart punctuation

`~~text~~` renders as strikethrough. With `output.html.smart-punctuation`
(default on), straight quotes become curly, `--` an en dash, `---` an em
dash and `...` an ellipsis in prose. Code spans and code blocks are not
affected.
-->

- **Rev C** -- counterweight changed from ~~fixed box~~ to hinged box;
  efficiency improved from 0.41 to 0.50.
- **Rev B** -- arm shortened from ~~2.00 m~~ to 1.80 m after the original
  arm cleared the frame by only 2 cm.
- **Rev A** -- first build; "proof of concept" only... retired.

```diff
 counterweight_kg: 45.0,
-efficiency: 0.41,
+efficiency: 0.50,
```

<!--
mdBook — `.hidden` class

Content inside an element with class="hidden" is in the HTML but not
displayed. Used here to keep a draft section in the source. Do not put
a Markdown heading inside it: hidden headings still appear in the
sidebar's heading list and in search results.
-->

<div class="hidden">

**Floating-arm conversion (draft).** Not yet tested. Do not publish.

</div>

## Glossary { #glossary }

<!--
mdBook — definition lists (mdBook 0.5+, `output.html.definition-lists`)

A term on its own line followed by one or more lines starting with `:`
(after 0 to 2 spaces). Each term becomes a link target with an id derived
from its text, e.g. `#counterweight`.
-->

Counterweight
  : The falling mass that powers the machine. On rev C it hangs from a hinge
    at the short end of the arm.

Dry fire
  : Releasing the arm with no projectile in the sling.

Release pin
  : The prong at the arm tip from which the free sling loop slides off. Its
    angle sets the launch angle.

Sling
  : Cord and pouch hung from the arm tip. Acts as a second pendulum,
    raising projectile speed above arm-tip speed.

Trebuchet
  : A gravity-powered lever engine.
  : Distinct from the mangonel, which stores energy in twisted cord.

## Background

<!--
mdBook — raw HTML blocks

<details>/<summary> gives a collapsible section. Leave a blank line after
<summary> and before </details> so the Markdown inside is still parsed.
-->

<details>
<summary>Historical note</summary>

Counterweight trebuchets appear in the Mediterranean world by the late
twelfth century and remained in use until gunpowder artillery displaced
them in the fifteenth.[^chevedden]

</details>

<!--
mdBook — footnotes

`[^label]` in the text and `[^label]: text` anywhere in the file. Notes are
numbered in order of first reference and collected at the end of the page.
Continuation lines are indented four spaces.
-->

[^chevedden]: P. E. Chevedden, L. Eigenbrod, V. Foley, and W. Soedel,
    "The Trebuchet," *Scientific American*, vol. 273, no. 1, pp. 66–71, 1995.

[^denny]: M. Denny, "Siege engine dynamics," *European Journal of Physics*,
    vol. 26, no. 4, pp. 561–577, 2005.

[^cd]: Smooth sphere in the subcritical Reynolds-number range. A softball's
    seams change the true value; 0.47 is the planning figure for this machine.

<!--
mdBook — simulator source for the includes above

Everything between the comment markers below is the simulator program. It
is never rendered; the include directives earlier on this page copy parts
of it into code blocks. Lines beginning `# ` are Rust hidden lines.
-->

<!--
ANCHOR: program
# use std::f64::consts::PI;
#
const G: f64 = 9.81; // m/s^2
const RHO_AIR: f64 = 1.204; // kg/m^3, dry air at 20 C

ANCHOR: params
/// Machine and projectile parameters, SI units.
#[derive(Debug, Clone, Copy)]
pub struct Params {
    pub counterweight_kg: f64,
    pub projectile_kg: f64,
    /// Fall of the counterweight's centre of mass, latch to bottom.
    pub drop_m: f64,
    /// Fraction of counterweight energy delivered to the projectile.
    pub efficiency: f64,
    pub release_height_m: f64,
    pub projectile_diameter_m: f64,
    pub drag_coefficient: f64,
}

/// T-2 revision C: 45 kg hinged counterweight, regulation softball.
pub const T2_REV_C: Params = Params {
    counterweight_kg: 45.0,
    projectile_kg: 0.18,
    drop_m: 0.60,
    efficiency: 0.50,
    release_height_m: 2.0,
    projectile_diameter_m: 0.097,
    drag_coefficient: 0.47,
};
ANCHOR_END: params

impl Params {
    /// Launch speed from the energy balance.
    pub fn launch_speed(&self) -> f64 {
        assert!(self.projectile_kg > 0.0, "projectile mass must be positive");
        assert!((0.0..=1.0).contains(&self.efficiency), "efficiency must lie in [0, 1]");
        (2.0 * self.efficiency * self.counterweight_kg * G * self.drop_m / self.projectile_kg).sqrt()
    }
}

/// Closed-form range with no air resistance.
pub fn range_vacuum(v: f64, theta_deg: f64, y0: f64) -> f64 {
    let (s, c) = theta_deg.to_radians().sin_cos();
    v * c / G * (v * s + (v * v * s * s + 2.0 * G * y0).sqrt())
}

ANCHOR: drag
/// Range with quadratic drag; semi-implicit Euler, 1 ms step.
pub fn range_drag(p: &Params, v: f64, theta_deg: f64) -> f64 {
    let area = PI * (p.projectile_diameter_m / 2.0).powi(2);
    let k = 0.5 * RHO_AIR * p.drag_coefficient * area / p.projectile_kg;
    let (s, c) = theta_deg.to_radians().sin_cos();
    let (mut x, mut y) = (0.0, p.release_height_m);
    let (mut vx, mut vy) = (v * c, v * s);
    let dt = 1e-3;
    while y >= 0.0 {
        let speed = (vx * vx + vy * vy).sqrt();
        vx -= k * speed * vx * dt;
        vy -= (G + k * speed * vy) * dt;
        x += vx * dt;
        y += vy * dt;
    }
    x
}
ANCHOR_END: drag

fn main() {
    let p = T2_REV_C;
    let v = p.launch_speed();
    let (best_angle, best_range) = (200..=500)
        .map(|a| a as f64 / 10.0)
        .map(|a| (a, range_drag(&p, v, a)))
        .max_by(|a, b| a.1.total_cmp(&b.1))
        .unwrap();
    println!("launch speed       {v:5.1} m/s");
    println!("range, no drag, 45 {:5.0} m", range_vacuum(v, 45.0, p.release_height_m));
    println!("range, drag, 45    {:5.0} m", range_drag(&p, v, 45.0));
    println!("best angle (drag)  {best_angle:5.1} deg ({best_range:.0} m)");
}
ANCHOR_END: program
-->