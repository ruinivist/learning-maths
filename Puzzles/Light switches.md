# Light switches

## Information theory prerequisites

If there are $N$ equally likely possibilities, Shannon entropy (uncertainty) is $H=\log_2 N$ bits.

An observation with $K$ possible outcomes provides at most $\log_2 K$ bits.

If each visit produces $K$ distinguishable outcomes and you need to distinguish $N$ possibilities, the minimum number of visits is

$$v_{\min}=\left\lceil\log_K N\right\rceil=\left\lceil\frac{\log_2 N}{\log_2 K}\right\rceil.$$

## 3 bulbs, 3 switches

If you can only tell whether a bulb is on or off, each visit has $K=2$ outcomes. To distinguish among $N=3$ switches, you need

$$v_{\min}=\left\lceil\log_2 3\right\rceil=2.$$

If you can also tell whether an off bulb is warm or cold, each visit has three outcomes: on, off but warm, and off and cold. Then $N=K=3$, so one visit is enough.

## 1 bulb, 4 switches

With one bulb and four switches, how many visits are needed to identify which switch controls the bulb? Assume exactly one switch controls it.

### Solution

The bulb's on/off and hot/cold states give four possible observations. Turn switches 1 and 2 on long enough to heat the bulb, then turn switch 1 off. Shortly before entering the room, turn switch 3 on. Leave switch 2 on and switch 4 off.

At the visit, the bulb's state identifies the switch:

- Off and warm: switch 1.
- On and warm: switch 2.
- On and cold: switch 3.
- Off and cold: switch 4.

One visit is enough. The general idea is to assign a distinct observable state to each possibility.
