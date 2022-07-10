# brds (WIP)

3 sequences, 2 function generators, 3 shift registers, 5 destinations. norns, grid, crow & just friends

a 3-track sequencer centered around a 5-output patch bay, with built-in shift-registers (for pseudo-polyphony) and muti-mode CV mixing. each output addresses either a crow voltage + function generator, internal engine, or an individual voice of just friends. sequences are input via an isometric keyboard, recorded live or through step-by-step editing. timing on each track can be syncronous or asycnronous, quantized or unquantized.

# documentation

## norns

- **E1-E3:** envelope time, slope, shape
- **K2:** envelope focus
- **K3:** envelope loop
- **K1:** alt

## grid

![brds grid docs](doc/brds.png)

## notes

cv mixing modes
- normal (priority by track #)
- max
- sum
- diff
- min
- random (maybe)

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
- (someday: w/syn)

grow gate out modes:
- function 1
- function 2
- gate
- trig
