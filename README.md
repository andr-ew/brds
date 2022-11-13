# brds (WIP)

cv & ii gesture router

3-track grid keyboard with pattern recording, slew. routed into a 5-output patch bay, with built-in shift-registers (for pseudo-polyphony) and muti-mode CV mixing. each output addresses either a crow voltage + function generator or an individual voice of just friends.

## hardware

**required**

- [norns](https://github.com/p3r7/awesome-monome-norns) (220321 or later)
- [grid](https://monome.org/docs/grid/) (128 only)
- [crow](https://monome.org/docs/crow/)

**also supported**

- [just friends](https://www.whimsicalraps.com/products/just-friends?variant=5586981781533)

## install

~ not done yet ~

## documentation

### norns

- **E1:** page focus
- pages:
  - function 1 & 2
    - **E2:** time
    - **E3:** ramp
    - **K2:** shape
    - **K3:** trns/sus/cyc
  - jf
    - **E2:** note level
    - **E3:** run
    - **K2:** synth mode
    - **K3:** GOD
  - mix mode
    - **E2:** mode x
    - **E3:** mode y
- **K1 (hold):** scale

### grid

![brds grid docs](doc/brds.png)

## notes

cv mixing 
- mix x & y coordinites, then map to scale
- independently assign modes for x & y axes
- mixed keymaps (1-5) are displayed on screen when not in output focus
- edit x & y modes when not in output focus
- modes
  - top (track)
  - bottom (track)
  - max
  - sum
  - diff
  - min

sync mode
- parameter recorders are synced to bars

crow input destiations
- function 1 & 2 gate in
- output 1-5 transpose (oct or scale degree)
- global clock
- jf pitch bend

output destinations
- crow cv + func 1+2
- crow cv + func 2+3
- ii jf 1-6
- ii crow cv + gate 1+2
- ii crow cv + gate 3+4

idea: voice allocation rather than shift registers (true polphony w/ voice stealing)
