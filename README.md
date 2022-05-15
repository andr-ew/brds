# brds

3 sequences, 2 function generators, 3 shift registers, 5 destinations. norns, grid, crow & just friends

a 3-track sequencer centered around a 5-output patch bay, with built-in shift-registers (for pseudo-polyphony) and muti-mode CV & gate mixing. each output addresses either a crow voltage + internal function generator, or an individual voice of just friends. sequences are input via an isometric keyboard, recorded live or through step-by-step editing. timing on each track can be both syncronous or asynronous, quantized or unquantized.

# documentation

- **E1-E3:** envelope time, slope, shape
- **K2:** envelope focus
- **K3:** envelope loop
- **K1:** alt

## grid

![brds grid docs](doc/brds.png)

## notes

gate summing modes (global)
- or (∨)
- and (∧)
- xor (⊻)
- not (¬)
- random (x)

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

playhead control
- when playing
  - mlr style, with cuts & sublooping
- in async mode
  - every step represents a new note, each step length is different
  - "time" sets the step time, gate time is fixed
- in sync mode
  - every step is an even division of the bar
  - "time" sets the gate time, step time is fixed

sequencing
- play/pause keys
  - record + play to record live sequence
  - just record to begin a manual sequence, advancing to the next step after each note
  - when paused (regardless of recording) tap a step key to enter that step & edit the note
- playbar
  - shows 8-step sections of curent sequence
  - bank keys page through 8-step sections of the sequence
- can add slew per-step just like realtime

jf coarse (oct) & fine controls (alt menu, probably on the screen in the mix section)
