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

- **E1-E3:** envelope time, slope, shape
- **K2:** envelope focus
- **K3:** envelope loop
- **K1:** alt

### grid

![brds grid docs](doc/brds.png)

## notes

cv mixing 
- mix x & y coordinites, then map to scale
- independently assign modes for x & y axes
- mixed keymaps (1-5) are displayed on screen when not in output focus
- modes
  - normal (priority by track #)
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
- cv crow 1+2
- cv crow 2+3
- ii jf 1-6
- ii crow 1+2
- ii crow 3+4
- w/syn 1-x
- orgn 1-x

grow gate out modes:
- function 1
- function 2
- gate
- trig
