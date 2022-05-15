# brds

3 sequencers, 2 function generators, 3 shift registers, 5 destinations

# documentation

- **E1-E3:** envelope time, slope, shape
- **K2:** envelope focus
- **K3:** envelope loop
- **K1:** alt

## grid

![brds grid docs](doc/brds.png)

## ++

gate summing modes (should it be global or per-output ?)
- or/and/xor -> not

cv mixing (global)
- max (>)
- sum (+)
- diff (-)
- min (<)
- random (x) (w/ possible probablility parameter)

sync mode
- live recording is synced to bars
- its smart about rounding down, so if the pattern ends late and there is no or very little information in the pattern, it will truncate down rather than up
- set idepenently for seqs 1-3, and global patterns

consider splitting alt into separate mix & scale pages, for more UI space
- display truth tables or glyphs on grid for each mix mode 

consider playhead control in place of top/bottom keyboard row
- mlr style, with cuts & sublooping
- in async mode
  - every step represents a new note, each step length is different
  - "time" sets the step time, gate time is fixed
- in sync mode
  - every step is an even division of the bar
  - "time" sets the gate time, step time is fixed

jf coarse (oct) & fine controls (alt menu, probably on the screen)

## --

I don't think the left gate key makes sense anymore ? for ansyncrounous patterns/gates I think the you would use the right side output gates + the global parameter recorders. would just need one key to enable/disable gates entirelly in the sequence

## +?

op-z style non-realtime sequencing
- play/pause keys
  - record + play to record live seuqeunce
  - just record to begin a manual sequence (using the playbar & nav keys)
- playbar
  - when paused 
    - shows 8-beat sections of curent sequence
    - prev/next keys page through 2-bar sections of the sequence when not playing
  - when playing
    - shows 8 bars if sequence is longer than 8 beats
    - prev/next skips by bar
- can add slew per-step just like realtime
