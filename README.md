# brds

3 cv recorders, 2 function generators, 3 shift registers, 5 destinations

pseudo-polyphonic async sequencer

# documentation

- **E1-E3:** envelope time, slope, shape
- **K2:** evelope focus
- **K3:** envelope loop
- **K1:** alt

## grid

![brds grid docs](doc/brds.png)

## ++

gate summing modes (global this time, rather than per-output)
- or/and/xor -> not

cv mixing (global)
- max (>)
- sum (+)
- diff (-)
- min (<)

pattern start/length quantization
- quantize to selected multiple of a bar. setting quant to 1+ will turn brds into a syncronous instrument

consider splitting alt into separate mix & scale pages, for more UI space
- display truth tables or glyphs on grid for each mix mode 
