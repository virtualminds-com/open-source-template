# Choosing a License

## About

This page is a quick reminder of what each pre-approved license does. It is
**not** legal advice and it is **not** the full process - the approval flow,
the rules about which license fits which project type, and any company-specific
notices that must accompany the `LICENSE` file live in our internal
documentation on Confluence. Read those before picking one and talk with the
Open Source group stakeholders.

License files whose name ends with `_template` contain placeholders like
`<YEAR>` that you must fill in. All other files are verbatim canonical texts and
are copied as-is. Each entry below links to the SPDX and OSI canonical pages -
diff against those if you want to confirm a copy hasn't drifted.

## Algorithm

Answer these questions about the project before choosing a license:
- Is it code or assets (images, configs, datasets)?
- Do we use it exclusively inside our infra (backend server), or we ship it to
  clients (a mobile app SDK, a desktop app)?

### If it is assets

Use **CC0 1.0**. It is a public-domain dedication that fits non-code
artefacts: images, configs, datasets, documentation, examples. The
software licenses on this page assume "source code" and "distribution"
semantics and do not map cleanly onto assets.

### If it is code

Your default choice is **MIT License** if the project is a small
business-agnostic tool, doing something generic and technical, not having any
advanced company-developed algorithms and formulas.

If the project touches complex things like exposing certain algorithms that we
developed in ML, crypto-algos, complex data structures, then it might be better
to use **Apache License 2.0**. This will make sure that other people can't take
our stuff or contribute their own code, then patent it, and sue us. Only makes
sense if there is anything that might be patented. For instance, a fast XML
parser would live fine on **MIT**. But an elaborate click probability prediction
formula might need the **Apache 2.0**.

#### And we ship the binary to clients

Copyleft licenses should be avoided. Stick with the **MIT** or **Apache
2.0** choice above. Once any external contributor's copyleft code lands
in a project we ship out - an SDK, a desktop or mobile app, an on-prem
deployment, anything where the compiled output leaves our
infrastructure - the whole shipped work has to be released under that
copyleft.

The trap is one-way and permanent. As long as a project stays purely
internal, we can pull in GPL code freely. But the moment we want to ship
that project out - to a customer, to an open release, to a partner - any
external contributor's GPL'd patch forces the whole shipped work to
become GPL. There is no walking that back later. The same lock-in blocks
future relicensing of our own public GPL project: external contributors
own their patches, so without a Contributor License Agreement we can
never dual-license or close it.

#### And we only run it on our own infra

Copyleft is safe in this branch. The binary stays on Virtual Minds
servers, so distribution obligations never trigger - we can pull in GPL
code and accept external GPL contributions without forcing anything
open. The one exception is **AGPL**: it treats network access as
distribution, so AGPL code in a backend that serves clients over the
network would force us to publish source to those clients. Plain GPL
does not.

For the license to put on our own code in this branch, the **MIT** or
**Apache 2.0** rule above still applies.

### Verify the choice

Whatever license the algorithm above lands on, run it past the **Open
Source group** and **Legal** before applying. They will confirm the
choice against any company-specific notices, IP commitments, or
project-specific concerns the algorithm does not cover.

---

## Permissive

### MIT - [`licenses/MIT_template.txt`](licenses/MIT_template.txt)

Canonical:
[SPDX](https://spdx.org/licenses/MIT.html) |
[OSI](https://opensource.org/license/mit)

The shortest and most widely recognized permissive license. Allows commercial
use, modification, distribution, and private use; the only condition is that
the copyright and license notice ships with the software. Good default for
small libraries and tools where you don't care whether derivatives stay open.

### BSD 2-Clause "Simplified" - [`licenses/BSD-2-Clause_template.txt`](licenses/BSD-2-Clause_template.txt)

Canonical:
[SPDX](https://spdx.org/licenses/BSD-2-Clause.html) |
[OSI](https://opensource.org/license/bsd-2-clause)

Permissive, functionally equivalent to MIT. Pick this over MIT only when there
is a specific reason to match a BSD-ecosystem project.

### BSD 3-Clause "New" / "Revised" - [`licenses/BSD-3-Clause_template.txt`](licenses/BSD-3-Clause_template.txt)

Canonical:
[SPDX](https://spdx.org/licenses/BSD-3-Clause.html) |
[OSI](https://opensource.org/license/bsd-3-clause)

BSD 2-Clause plus a non-endorsement clause: the project's name and the names
of contributors may not be used to promote derivative products without
permission. Useful when the project's name itself is something you want to
keep protected from marketing reuse.

### Apache License 2.0 - [`licenses/Apache-2.0.txt`](licenses/Apache-2.0.txt)

Canonical:
[SPDX](https://spdx.org/licenses/Apache-2.0.html) |
[OSI](https://opensource.org/license/apache-2-0)

Permissive like MIT or BSD, but adds patent protection that those leave
out. Two key parts:

1. **Patent promise.** Each contributor promises not to sue users over
   patents that cover their contribution. MIT and BSD say nothing about
   patents at all.
2. **"Stop suing" clause.** If you sue anyone claiming the software
   infringes your patents, you lose your right to use it - so patent
   attacks are discouraged among the project's users.

Redistributors must keep the license text, attribution notices, the
upstream `NOTICE` file if one exists, and mark files they modify.
Derivatives can otherwise be released under any license, proprietary
included.

A good default for mid-to-large libraries, especially in patent-heavy
areas (codecs, crypto, ML, networking, payments) or when contributors
are expected from multiple companies.

### Boost Software License 1.0 - [`licenses/BSL-1.0.txt`](licenses/BSL-1.0.txt)

Canonical:
[SPDX](https://spdx.org/licenses/BSL-1.0.html) |
[OSI](https://opensource.org/license/bsl-1-0)

Permissive, MIT-style, but does **not** require the license text to be
reproduced when distributing in compiled / binary form. Common in C++
libraries and other code that ships embedded in larger binaries.

## Copyleft

These licenses share one rule: **using the software, even commercially,
creates no obligation by itself**. The output of running a copyleft
tool (a binary produced by a GPL compiler, an image edited in GIMP) is
your work, not a derivative of the tool. Obligations only trigger when
you **distribute** the licensed code, or a modified version of it - at
which point you must ship the source under the same license. AGPL is
the one exception below: it treats "offering the software over a
network" (e.g. running it inside a SaaS product) as distribution.

The licenses below differ in *how much* of a combined work must stay
open when you distribute: the entire program (strong copyleft), or
only the original files or library (weak / file-level copyleft).

### Copyleft (strong)

#### GPL v3.0 - [`licenses/GPL-3.0.txt`](licenses/GPL-3.0.txt)

Canonical:
[SPDX](https://spdx.org/licenses/GPL-3.0-only.html) |
[OSI](https://opensource.org/license/gpl-3-0)

Strong, whole-program copyleft. Anything you distribute that includes
GPL code (statically or dynamically linked) must itself be GPL v3
with full source. Includes a patent grant and anti-tivoization
clauses - users must be able to install modified versions on the
hardware the software was delivered on. Pick when you want
derivatives to stay open.

#### GPL v2.0 - [`licenses/GPL-2.0.txt`](licenses/GPL-2.0.txt)

Canonical:
[SPDX](https://spdx.org/licenses/GPL-2.0-only.html) |
[OSI](https://opensource.org/license/gpl-2-0)

The earlier GPL, famously used by the Linux kernel. Same
whole-program distribution scope as GPL v3 but no explicit patent
grant. Prefer GPL v3 for new projects unless there is a specific
interoperability reason - for example, contributing to an existing
GPL v2 codebase.

#### GPL Affero v3.0 (AGPL) - [`licenses/AGPL-3.0.txt`](licenses/AGPL-3.0.txt)

Canonical:
[SPDX](https://spdx.org/licenses/AGPL-3.0-only.html) |
[OSI](https://opensource.org/license/agpl-v3)

GPL v3 with one extra trigger: **offering the software over a network
counts as distribution**. If you run AGPL code as part of a public
web service, users of that service can demand the source, even
though you never shipped a binary. Pick to prevent cloud providers
from running your code without contributing back.

### Copyleft (weak / file-level)

#### GPL Lesser v2.1 (LGPL) - [`licenses/LGPL-2.1.txt`](licenses/LGPL-2.1.txt)

Canonical:
[SPDX](https://spdx.org/licenses/LGPL-2.1-only.html) |
[OSI](https://opensource.org/license/lgpl-2-1)

Library-friendly variant of GPL. Modifications to the LGPL library
itself must stay LGPL, but an application that merely links against
it (dynamic linking, or static linking that provides relinkable
object files) can be under any license. Used by glibc and similar
low-level libraries.

#### Mozilla Public License 2.0 - [`licenses/MPL-2.0.txt`](licenses/MPL-2.0.txt)

Canonical:
[SPDX](https://spdx.org/licenses/MPL-2.0.html) |
[OSI](https://opensource.org/license/mpl-2-0)

File-level copyleft. Only the original MPL files and modifications to
them must stay MPL; the rest of a larger work can be under any
license, including proprietary. Patent grant included. Much easier to
mix with closed-source code than GPL.

#### Eclipse Public License 2.0 - [`licenses/EPL-2.0.txt`](licenses/EPL-2.0.txt)

Canonical:
[SPDX](https://spdx.org/licenses/EPL-2.0.html) |
[OSI](https://opensource.org/license/epl-2-0)

File-level copyleft in the spirit of MPL - same scope: EPL files and
modifications to them stay EPL, the rest of a larger work can be
under any license. Adds a patent grant and extra
contributor-protection clauses. Widely used in the Java / Eclipse
ecosystem.

## Public-domain dedication

### Creative Commons Zero v1.0 Universal - [`licenses/CC0-1.0.txt`](licenses/CC0-1.0.txt)

Canonical:
[SPDX](https://spdx.org/licenses/CC0-1.0.html) |
[Creative Commons](https://creativecommons.org/publicdomain/zero/1.0/) *(not OSI-approved)*

Dedicates the work to the public domain to the fullest extent allowed, with a
fallback permissive license for jurisdictions that don't recognise public
domain dedication. **Not recommended for code** - there is no explicit patent
grant - but standard for data sets, documentation, configuration files, and
small examples.

### The Unlicense - [`licenses/Unlicense.txt`](licenses/Unlicense.txt)

Canonical:
[SPDX](https://spdx.org/licenses/Unlicense.html) |
[OSI](https://opensource.org/license/unlicense)

A short, plain-English public-domain dedication. Same patent-grant caveat as
CC0. Use only when attribution is genuinely not required and the project is
small enough that the patent concern is moot.
