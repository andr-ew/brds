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

patterns shared between tracks (maybe)

gate summing modes (global)
- or (∨)
- and (∧)
- xor (⊻)
- not (¬)
- random (x)
  - coin toss each new incoming step, scaled by the probability param

cv mixing (global)
- max (>)
- sum (+)
- diff (-)
- min (<)
- random (x)
  - coin toss each new incoming step, scaled by the probability param

sync mode
- live recording + parameter recorders are synced to bars
  - time signature set via steps/bank, default is 8/8
  - its smart about rounding down, so if the pattern ends late and there is no or very little information in the pattern, it will truncate down rather than up
- manual sequences loop through every bank in full, no partially filled bank at the end
- set idepenently for seqs 1-3 and parameter recorders

playhead control
- when playing
  - mlr style, with cuts & sublooping
- in async mode
  - every step represents a new note, each step length is different
  - "time" sets the step time, gate time is a fixed ratio of the length
- in sync mode
  - every step is an even division of the bar
  - "time" sets the gate time, step time is fixed

- alternative: time sets gate length in all modes, sync + async are both fixed step length
  - this might make for more intuitive seuqencing/editing
    - i.e. copy the step + tie in any mode to increase note length

sequencing
- play/rec keys
  - record + play to record live sequence
  - just record to begin a manual sequence, advancing to the next step after each note
  - when paused (regardless of recording) tap a step key to enter that step & edit the note
  - play/pause is synced to the clock when in sync mode or if the seuquence is manual. an async live sequence runs completely off the clock.
- step
  - shows 8-step sections of curent sequence
  - bank keys page through 8-step sections of the sequence
- can add slew per-step just like realtime. the reverse key toggle gate ties.

# ++

jf coarse (oct) & fine controls (alt menu, probably on the screen in the mix section)

variable quantization
- E1-3 for each track on the sync alt page
- in any mode, crossfades every step's "nudge" value between 0 and some random number
  - for a live, synced sequence only - this value will start at 100%
- maybe there could be a separate parameter for even & odd values, so for a step sequence, the odd value would essentially add swing

crow input destiations
- function 1 & 2 gate in
- output 1-5 transpose (oct or scale degree)
- global clock

option for scale degrees to be unique per-track or applied to all.

maybe bank keys should be a general prev/next
- default: prev/next step
  - while recording 
    - next to add a rest
    - prev to go back to the last step if u made a mistake
- hold both keys to switch between bank/step scope
- copy/insert actions:
  - insert blank step (rest): step + next, or just next while recording
  - copy step: hold keyboard note + next (some for recording/not recording). will add a gate tie, so it's basically like increasing note duration

## implementation

sequences
- data stored in each step (regardless of mode)
  - duration
  - has gate
  - nudge (or, +/- distance to nearest step)
  - gate duration (maybe stored as a ratio of duration)
  - slew amount
  - gate tie
- modes
  - live, async: variable duration, always gate, never nudge, variable gate duration
  - live, sync: fixed duration, sometimes gate, variable nudge, variable gate duration
    - not sure what to do if the user tries to play two notes in one step. just keep the first one only ? can't play too fast I guess
  - manual, async: either variable duration (quantized) or fixed, sometimes gate, never nudge, gate duration = 50% of duration or vairable
  - manual, sync: fixed duration, sometimes gate, never nudge, variable gate duration
- steps are either
  - iterated over by high resolution, globally synced clock
  - (for live, async mode) called in its own free-running loop, starting a new delay every step
