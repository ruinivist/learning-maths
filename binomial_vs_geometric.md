# Binomial vs. Geometric: Two Views of One Bernoulli Process

> **One-line takeaway:** the binomial *fixes the number of trials and counts successes*; the geometric *fixes the number of successes (one) and counts trials*. Both are questions about the same random sequence, and they are linked by the event identity
>
> $$\{X_n \ge 1\} = \{T \le n\}.$$

---

## 0. Setup

A **Bernoulli process** is an infinite sequence of independent trials, each succeeding with probability $p$ (write $q = 1-p$ for failure).

Two random variables are defined on this *same* sequence:

| Symbol | Meaning | Distribution |
|---|---|---|
| $X_n$ | number of successes in the **first $n$ trials** | $X_n \sim \operatorname{Bin}(n,p)$ |
| $T$ | **trial number of the first success** | $T \sim \operatorname{Geom}(p)$, support $\{1,2,3,\dots\}$ |

---

## 1. Same sequence, two questions

Below is one realisation of the process (`S` = success, `F` = failure). The binomial looks through a **fixed window** of $n$ trials and counts; the geometric **walks forward and stops** at the first `S`.

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 720 240" width="720" role="img" aria-label="A sequence of ten Bernoulli trials. The binomial view fixes a window of six trials and counts one success. The geometric view stops at the first success at trial four.">
<rect x="0.5" y="0.5" width="719" height="239" rx="10" fill="#ffffff" stroke="#d1d5db"/>
<g font-family="Helvetica, Arial, sans-serif">
<path d="M34 96 V80 H416 V96" fill="none" stroke="#2563eb" stroke-width="2"/>
<text x="34" y="68" font-size="15" font-weight="bold" fill="#2563eb">Binomial view: fix n = 6, count successes → X₆ = 1</text>
<circle cx="60" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="60" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<circle cx="126" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="126" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<circle cx="192" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="192" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<circle cx="258" cy="130" r="20" fill="#2e9e5b" stroke="#1f7a44" stroke-width="2"/><text x="258" y="136" text-anchor="middle" font-size="16" font-weight="bold" fill="#ffffff">S</text>
<circle cx="324" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="324" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<circle cx="390" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="390" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<g opacity="0.45">
<circle cx="456" cy="130" r="20" fill="#2e9e5b" stroke="#1f7a44" stroke-width="2"/><text x="456" y="136" text-anchor="middle" font-size="16" font-weight="bold" fill="#ffffff">S</text>
<circle cx="522" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="522" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<circle cx="588" cy="130" r="20" fill="#2e9e5b" stroke="#1f7a44" stroke-width="2"/><text x="588" y="136" text-anchor="middle" font-size="16" font-weight="bold" fill="#ffffff">S</text>
<circle cx="654" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="654" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
</g>
<g font-size="12" fill="#6b7280" text-anchor="middle">
<text x="60" y="170">1</text><text x="126" y="170">2</text><text x="192" y="170">3</text><text x="258" y="170">4</text><text x="324" y="170">5</text><text x="390" y="170">6</text><text x="456" y="170">7</text><text x="522" y="170">8</text><text x="588" y="170">9</text><text x="654" y="170">10</text>
</g>
<path d="M34 186 V202 H284 V186" fill="none" stroke="#dc2626" stroke-width="2"/>
<text x="34" y="224" font-size="15" font-weight="bold" fill="#dc2626">Geometric view: wait for the first success → T = 4</text>
</g>
</svg>

*Same data, different questions:* "How many `S` in trials 1–6?" (answer $1$) versus "On which trial did the first `S` appear?" (answer $4$).

---

## 2. The event identity $\{X_n \ge 1\} = \{T \le n\}$

**Claim.** For every outcome of the process, $X_n \ge 1$ if and only if $T \le n$.

**Proof.**

- ($\Rightarrow$) If $X_n \ge 1$, at least one of the first $n$ trials is a success, so the *first* success cannot come later than trial $n$. Hence $T \le n$.
- ($\Leftarrow$) If $T \le n$, the first success occurs within the first $n$ trials, so at least one success has occurred by then. Hence $X_n \ge 1$. $\blacksquare$

The two statements are literally the sentence *"there is at least one success in the first $n$ trials"*, said in two vocabularies.

### Check by brute force: all $2^3$ outcomes for $n = 3$

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 760 352" width="760" role="img" aria-label="Enumeration of all eight outcomes of three trials, showing that X3 at least 1 and T at most 3 hold in exactly the same seven outcomes.">
<rect x="0.5" y="0.5" width="759" height="351" rx="10" fill="#ffffff" stroke="#d1d5db"/>
<g font-family="Helvetica, Arial, sans-serif">
<g font-size="14" font-weight="bold" fill="#111827" text-anchor="middle">
<text x="100" y="36">Outcome</text><text x="215" y="36">Probability</text><text x="330" y="36">X₃</text><text x="410" y="36">T</text><text x="530" y="36">X₃ ≥ 1 ?</text><text x="650" y="36">T ≤ 3 ?</text>
</g>
<line x1="16" y1="48" x2="744" y2="48" stroke="#9ca3af"/>
<rect x="16" y="58" width="728" height="28" rx="4" fill="#fef2f2"/>
<rect x="16" y="90" width="728" height="28" rx="4" fill="#f0fdf4"/>
<rect x="16" y="122" width="728" height="28" rx="4" fill="#f0fdf4"/>
<rect x="16" y="154" width="728" height="28" rx="4" fill="#f0fdf4"/>
<rect x="16" y="186" width="728" height="28" rx="4" fill="#f0fdf4"/>
<rect x="16" y="218" width="728" height="28" rx="4" fill="#f0fdf4"/>
<rect x="16" y="250" width="728" height="28" rx="4" fill="#f0fdf4"/>
<rect x="16" y="282" width="728" height="28" rx="4" fill="#f0fdf4"/>
<!-- row 0: FFF -->
<circle cx="60" cy="72" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="60" y="76" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<circle cx="100" cy="72" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="100" y="76" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<circle cx="140" cy="72" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="140" y="76" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<!-- row 1: FFS -->
<circle cx="60" cy="104" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="60" y="108" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<circle cx="100" cy="104" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="100" y="108" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<circle cx="140" cy="104" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="140" y="108" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<!-- row 2: FSF -->
<circle cx="60" cy="136" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="60" y="140" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<circle cx="100" cy="136" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="100" y="140" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<circle cx="140" cy="136" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="140" y="140" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<!-- row 3: FSS -->
<circle cx="60" cy="168" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="60" y="172" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<circle cx="100" cy="168" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="100" y="172" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<circle cx="140" cy="168" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="140" y="172" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<!-- row 4: SFF -->
<circle cx="60" cy="200" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="60" y="204" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<circle cx="100" cy="200" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="100" y="204" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<circle cx="140" cy="200" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="140" y="204" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<!-- row 5: SFS -->
<circle cx="60" cy="232" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="60" y="236" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<circle cx="100" cy="232" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="100" y="236" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<circle cx="140" cy="232" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="140" y="236" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<!-- row 6: SSF -->
<circle cx="60" cy="264" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="60" y="268" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<circle cx="100" cy="264" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="100" y="268" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<circle cx="140" cy="264" r="11" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1.5"/><text x="140" y="268" text-anchor="middle" font-size="11" fill="#6b7280">F</text>
<!-- row 7: SSS -->
<circle cx="60" cy="296" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="60" y="300" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<circle cx="100" cy="296" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="100" y="300" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<circle cx="140" cy="296" r="11" fill="#2e9e5b" stroke="#1f7a44" stroke-width="1.5"/><text x="140" y="300" text-anchor="middle" font-size="11" font-weight="bold" fill="#ffffff">S</text>
<g font-size="14" fill="#111827" text-anchor="middle">
<text x="215" y="77">q³</text><text x="215" y="109">pq²</text><text x="215" y="141">pq²</text><text x="215" y="173">p²q</text><text x="215" y="205">pq²</text><text x="215" y="237">p²q</text><text x="215" y="269">p²q</text><text x="215" y="301">p³</text>
<text x="330" y="77">0</text><text x="330" y="109">1</text><text x="330" y="141">1</text><text x="330" y="173">2</text><text x="330" y="205">1</text><text x="330" y="237">2</text><text x="330" y="269">2</text><text x="330" y="301">3</text>
<text x="410" y="77">&gt; 3</text><text x="410" y="109">3</text><text x="410" y="141">2</text><text x="410" y="173">2</text><text x="410" y="205">1</text><text x="410" y="237">1</text><text x="410" y="269">1</text><text x="410" y="301">1</text>
</g>
<g font-size="17" font-weight="bold" text-anchor="middle">
<text x="530" y="78" fill="#dc2626">✗</text><text x="650" y="78" fill="#dc2626">✗</text>
<text x="530" y="110" fill="#16a34a">✓</text><text x="650" y="110" fill="#16a34a">✓</text>
<text x="530" y="142" fill="#16a34a">✓</text><text x="650" y="142" fill="#16a34a">✓</text>
<text x="530" y="174" fill="#16a34a">✓</text><text x="650" y="174" fill="#16a34a">✓</text>
<text x="530" y="206" fill="#16a34a">✓</text><text x="650" y="206" fill="#16a34a">✓</text>
<text x="530" y="238" fill="#16a34a">✓</text><text x="650" y="238" fill="#16a34a">✓</text>
<text x="530" y="270" fill="#16a34a">✓</text><text x="650" y="270" fill="#16a34a">✓</text>
<text x="530" y="302" fill="#16a34a">✓</text><text x="650" y="302" fill="#16a34a">✓</text>
</g>
<text x="380" y="338" text-anchor="middle" font-size="13" fill="#374151">The two ✓ columns match in every row, so the events are identical: P = 1 − q³ (everything except FFF).</text>
</g>
</svg>

Only `FFF` fails both tests, which is the "no success in three trials" event of probability $q^3$.

---

## 3. What the identity buys you

### 3.1 The geometric CDF falls out immediately

Take complements: $\{X_n = 0\} = \{T > n\}$. For the binomial, "zero successes" has the simplest possible probability:

$$
P(T > n) = P(X_n = 0) = \binom{n}{0}p^0 q^n = q^n .
$$

Therefore

$$
\boxed{P(T \le n) = P(X_n \ge 1) = 1 - (1-p)^n}
$$

### 3.2 The geometric PMF by differencing

$$
P(T = k) = P(T \le k) - P(T \le k-1) = \bigl(1 - q^{k}\bigr) - \bigl(1 - q^{k-1}\bigr) = q^{k-1}p, \qquad k = 1,2,\dots
$$

which is exactly "$k-1$ failures, then a success".

### 3.3 Picture: the CDF as a "success-by-now" probability

Each bar below is $P(T \le n) = P(X_n \ge 1)$ for $p = 0.3$. The pale red cap above it is the leftover mass $q^n = P(T > n) = P(X_n = 0)$, which shrinks geometrically.

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 700 322" width="700" role="img" aria-label="Bar chart of P(T at most n) equals 1 minus 0.7 to the n for n from 1 to 10 with p equal to 0.3, rising towards 1. The remaining mass above each bar is 0.7 to the n.">
<rect x="0.5" y="0.5" width="699" height="321" rx="10" fill="#ffffff" stroke="#d1d5db"/>
<g font-family="Helvetica, Arial, sans-serif">
<rect x="70" y="8" width="12" height="12" fill="#2e9e5b"/>
<text x="88" y="19" font-size="13" fill="#111827">P(T ≤ n) = P(Xₙ ≥ 1) = 1 − qⁿ</text>
<rect x="340" y="8" width="12" height="12" fill="#fde2e2" stroke="#f5a3a3"/>
<text x="358" y="19" font-size="13" fill="#111827">P(T &gt; n) = P(Xₙ = 0) = qⁿ</text>
<line x1="70" y1="50" x2="650" y2="50" stroke="#9ca3af" stroke-dasharray="4 4"/>
<line x1="70" y1="160" x2="650" y2="160" stroke="#e5e7eb" stroke-dasharray="4 4"/>
<g fill="#fde2e2" stroke="#f5a3a3" stroke-width="0.8">
<rect x="90" y="50" width="40" height="154"/>
<rect x="146" y="50" width="40" height="107.8"/>
<rect x="202" y="50" width="40" height="75.5"/>
<rect x="258" y="50" width="40" height="52.8"/>
<rect x="314" y="50" width="40" height="37"/>
<rect x="370" y="50" width="40" height="25.9"/>
<rect x="426" y="50" width="40" height="18.1"/>
<rect x="482" y="50" width="40" height="12.7"/>
<rect x="538" y="50" width="40" height="8.9"/>
<rect x="594" y="50" width="40" height="6.2"/>
</g>
<g fill="#2e9e5b">
<rect x="90" y="204" width="40" height="66"/>
<rect x="146" y="157.8" width="40" height="112.2"/>
<rect x="202" y="125.5" width="40" height="144.5"/>
<rect x="258" y="102.8" width="40" height="167.2"/>
<rect x="314" y="87" width="40" height="183" fill="#1d4ed8"/>
<rect x="370" y="75.9" width="40" height="194.1"/>
<rect x="426" y="68.1" width="40" height="201.9"/>
<rect x="482" y="62.7" width="40" height="207.3"/>
<rect x="538" y="58.9" width="40" height="211.1"/>
<rect x="594" y="56.2" width="40" height="213.8"/>
</g>
<g font-size="11" font-weight="bold" fill="#ffffff" text-anchor="middle">
<text x="110" y="219">.30</text><text x="166" y="173">.51</text><text x="222" y="141">.66</text><text x="278" y="118">.76</text><text x="334" y="102">.83</text><text x="390" y="91">.88</text><text x="446" y="84">.92</text><text x="502" y="78">.94</text><text x="558" y="74">.96</text><text x="614" y="71">.97</text>
</g>
<line x1="70" y1="50" x2="70" y2="270" stroke="#374151" stroke-width="1.5"/>
<line x1="70" y1="270" x2="650" y2="270" stroke="#374151" stroke-width="1.5"/>
<g font-size="12" fill="#374151" text-anchor="end"><text x="62" y="274">0</text><text x="62" y="164">0.5</text><text x="62" y="54">1.0</text></g>
<g font-size="12" fill="#374151" text-anchor="middle">
<text x="110" y="288">1</text><text x="166" y="288">2</text><text x="222" y="288">3</text><text x="278" y="288">4</text><text x="334" y="288" font-weight="bold">5</text><text x="390" y="288">6</text><text x="446" y="288">7</text><text x="502" y="288">8</text><text x="558" y="288">9</text><text x="614" y="288">10</text>
</g>
<text x="360" y="311" text-anchor="middle" font-size="13" fill="#374151">n (number of trials), with p = 0.3</text>
</g>
</svg>

**Worked example ($p = 0.3$, $n = 5$, the blue bar).** The chance of at least one success in five trials, equivalently of the first success arriving by trial 5, is

$$
1 - 0.7^5 = 1 - 0.16807 = 0.83193 .
$$

---

## 4. Generalisation: the $r$-th success and the negative binomial

Let $T_r$ be the trial number of the **$r$-th** success. The identity generalises verbatim:

$$
\boxed{\{X_n \ge r\} = \{T_r \le n\}}
$$

"At least $r$ successes in the first $n$ trials" is the same as "the $r$-th success has arrived by trial $n$".

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 700 270" width="700" role="img" aria-label="Nine Bernoulli trials with successes at trials one, four, six and eight. The first six trials contain three successes, so the third success time T3 equals six. The waiting times between successes are 1, 3 and 2.">
<rect x="0.5" y="0.5" width="699" height="269" rx="10" fill="#ffffff" stroke="#d1d5db"/>
<g font-family="Helvetica, Arial, sans-serif">
<path d="M34 96 V80 H436 V96" fill="none" stroke="#2563eb" stroke-width="2"/>
<text x="34" y="68" font-size="15" font-weight="bold" fill="#2563eb">X₆ = 3 ≥ r = 3   ⟺   the 3rd success has arrived by trial 6 (T₃ = 6 ≤ 6)</text>
<circle cx="60" cy="130" r="20" fill="#2e9e5b" stroke="#1f7a44" stroke-width="2"/><text x="60" y="136" text-anchor="middle" font-size="16" font-weight="bold" fill="#ffffff">S</text>
<circle cx="130" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="130" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<circle cx="200" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="200" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<circle cx="270" cy="130" r="20" fill="#2e9e5b" stroke="#1f7a44" stroke-width="2"/><text x="270" y="136" text-anchor="middle" font-size="16" font-weight="bold" fill="#ffffff">S</text>
<circle cx="340" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="340" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<circle cx="410" cy="130" r="20" fill="#2e9e5b" stroke="#1f7a44" stroke-width="2"/><text x="410" y="136" text-anchor="middle" font-size="16" font-weight="bold" fill="#ffffff">S</text>
<g opacity="0.45">
<circle cx="480" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="480" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
<circle cx="550" cy="130" r="20" fill="#2e9e5b" stroke="#1f7a44" stroke-width="2"/><text x="550" y="136" text-anchor="middle" font-size="16" font-weight="bold" fill="#ffffff">S</text>
<circle cx="620" cy="130" r="20" fill="#f3f4f6" stroke="#9ca3af" stroke-width="2"/><text x="620" y="136" text-anchor="middle" font-size="16" fill="#6b7280">F</text>
</g>
<g font-size="12" fill="#6b7280" text-anchor="middle">
<text x="60" y="170">1</text><text x="130" y="170">2</text><text x="200" y="170">3</text><text x="270" y="170">4</text><text x="340" y="170">5</text><text x="410" y="170">6</text><text x="480" y="170">7</text><text x="550" y="170">8</text><text x="620" y="170">9</text>
</g>
<g fill="none" stroke="#dc2626" stroke-width="2">
<path d="M34 184 V198 H86 V184"/>
<path d="M104 184 V198 H296 V184"/>
<path d="M314 184 V198 H436 V184"/>
</g>
<g font-size="14" font-weight="bold" fill="#dc2626" text-anchor="middle">
<text x="60" y="219">G₁ = 1</text><text x="200" y="219">G₂ = 3</text><text x="375" y="219">G₃ = 2</text>
</g>
<text x="34" y="250" font-size="14" fill="#111827">T₃ = G₁ + G₂ + G₃ = 6, where each wait Gᵢ is an independent Geom(p).</text>
</g>
</svg>

### 4.1 Negative binomial PMF

The $r$-th success lands exactly on trial $k$ iff trial $k$ is a success **and** the first $k-1$ trials contain exactly $r-1$ successes:

$$
P(T_r = k) = \binom{k-1}{r-1}\,p^{r}\,q^{\,k-r}, \qquad k = r, r+1, \dots
$$

### 4.2 Two more consequences

- **Sum of geometrics.** The waiting times $G_1,\dots,G_r$ between successes are i.i.d. $\operatorname{Geom}(p)$ (the process restarts after each success), so $T_r = G_1 + \dots + G_r$. Hence $\mathbb E[T_r] = r/p$.
- **Negative binomial CDF from the binomial.**
  $$
  P(T_r \le n) = P(X_n \ge r) = \sum_{j=r}^{n}\binom{n}{j}p^{j}q^{\,n-j}.
  $$
  Setting $r = 1$ recovers $1 - q^n$.

---

## 5. Cheat sheet

| | Binomial | Geometric | Negative binomial |
|---|---|---|---|
| **Fixed** | number of trials $n$ | number of successes $=1$ | number of successes $=r$ |
| **Random** | successes $X_n$ | trials needed $T$ | trials needed $T_r$ |
| **PMF** | $\binom{n}{k}p^k q^{n-k}$ | $q^{k-1}p$ | $\binom{k-1}{r-1}p^r q^{k-r}$ |
| **Link** | $\{X_n \ge 1\}$ | $=\{T \le n\}$ | $\{X_n \ge r\} = \{T_r \le n\}$ |
| **Mean** | $np$ | $1/p$ | $r/p$ |

**Key insight.** *Binomial = "how many successes in a fixed number of trials?" Geometric = "how many trials until the first success?"* They are two projections of the same Bernoulli process, and the bridge between them is the statement "at least one success in the first $n$ trials". For the $r$-th success, switch to the negative binomial.

> **Convention warning:** here $T$ counts the *trial number* of the first success, so its support is $\{1,2,\dots\}$. Some textbooks and libraries (e.g. NumPy's `negative_binomial`, or R's `dgeom`) instead count the number of *failures before* the first success, with support $\{0,1,2,\dots\}$. Always state which convention you are using.
