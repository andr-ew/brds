# brds

3 sequences, 2 function generators, 3 shift registers, 5 destinations. norns, grid, crow & just friends

a 3-track sequencer centered around a 5-output patch bay, with built-in shift-registers (for pseudo-polyphony) and muti-mode CV mixing. each output addresses either a crow voltage + function generator, internal engine, or an individual voice of just friends. sequences are input via an isometric keyboard, recorded live or through step-by-step editing. timing on each track can be syncronous or asycnronous, quantized or unquantized.

# documentation

- **E1-E3:** envelope time, slope, shape
- **K2:** envelope focus
- **K3:** envelope loop
- **K1:** alt

## grid

![brds grid docs](doc/brds.png)

## notes

cv mixing (global)
- max (>)
- sum (+)
- diff (-)
- min (<)
- random (x)
  - coin toss each new incoming step, scaled by the probability param
- modulo (%)


sync mode
- live recording + parameter recorders are synced to bars
  - time signature set via steps/bank, default is 8/8
  - its smart about rounding down, so if the pattern ends late and there is no or very little information in the pattern, it will truncate down rather than up
- manual sequences loop through every bank in full, no partially filled bank at the end
- set idepenently for seqs 1-3 and parameter recorders

playhead control
- current bank is dim component behind brighter step component
- when playing
  - mlr style, with cuts & sublooping
  - while a step is held (for sublooping), steps component grows to fill the bottom row of the grid
- in async mode
  - every step represents a new note, each step length is different
  - "time" sets the step time, gate time is a fixed ratio of the length
- in sync mode
  - every step is an even division of the bar
  - "time" sets the gate time, step time is fixed

- alternative: time sets gate length in all modes, sync + async are both fixed step length
  - this might make for more intuitive seuqencing/editing
    - i.e. copy the step + tie in any mode to increase note length
  - I think this is deffo better

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
option for scale degrees to be unique per-track or applied to all.

maybe bank keys should be a general prev/next
- yes
- while recording 
  - next to add a rest
  - prev to go back to the last step if u made a mistake
- while not playing
  - hold both keys to switch between bank/step scope, to navigate around the sequence while editing
- while playing
  - prev/next is fixed in the bank scope, and pressing the key moves the playhead to the start of that bank

step edit actions:
  - insert blank step (rest): step + next, or just next while recording
  - copy step (tie): hold keyboard note + next (same for recording/not recording). 
    - will add a gate tie, so it's basically like increasing note duration
    - will offset remaining steps in sequence
  - copy step (repeat): while sequencer is stopped, hold step + step insert repetitions between those steps. 
    - while a step is held, the steps component grows to fill the bottom row of the grid
  - change note into a rest: remove the note on the keyboard
    - I think that moving to a step should actually "play" through all the notes in the step once, so we need a new action for this. step focus menu would be a fine place
  - clear step: hold the step (entering the extended steps screen) and tap the remove button on the right side of grid 
    - maybe its an (x) glyph
  - hold rec to clear the pattern
  - copy pattern: hold src pattern key, tap destination pattern
    - copy pattern between tracks, hold src pattern, change track, tap destination pattern (or just release to write to the same slot)

modulo option in sum & diff mix modes
- wrap around a single octave or the full octave range
  - alt: modulo parameter specifies an octave value (1-5) and a scale degree value (1 - # of scale degrees)
- maybe that middle row (currently probability) should just be a general parameter section for the cv mix modes (yes)
- or maybe there should be a separate modulo glyph - this would be more intuitive. consider replacing difference or min or whatever ends up being least interesting. I bet min won't be all that great (?)

change "time" to duration, which feels more specific to both uses. so for a playing sequence, left would be faster, right would be slower.

gate fwd / alt alt menu stuff
- hold key to enable/disable gates for that track on a per-output basis
  - I think gate forward should interact with the mix process a bit
    - when gate forwarding is on, CV only contributes to the mix when gate is high
    - when gate forward is off, CV always contributes to the mix
- it really wouldn't be that bad of an idea to move this whole process to the alt menu
  - maybe combine with the sync screen
- idea: mix the whole thing up by turning this key as the alt key (instead of K1). just so happens that it's open on every alt screen currently
  - I like this idea !
  - we'll want to shift things around to put the page control on the bottom left
  - actuallyyyy: even better: we can decrease the pattern control to 5 patterns (I like less of them) and then take up 3 keys, so you just hold a key to bring up that page. perfect !!

derp I guess the sync setting for tracks should work on a pattern-by-pattern basis. maybe we should bring this setting to the main page (drop another pattern slot)

# ++

consider allowing unique mix mode per-output
- there's space in the UI if only 1 glyph is displayed at a time
- also allows for 5x5 glyphs rather than 3x3
- options screen is starting to get a little crowded with all the 3x3 glyphs

jf settings 
- coarse (oct) & fine controls
- synth mode switch here (when off brds has no effect on jf)
- maybe put this in the mix menu or perhaps as the K1 alt screen (I like k1)

variable quantization
- E1-3 for each track on the track menu
- in any mode, crossfades every step's "nudge" value between 0 and some random number
  - for a live, synced sequence only - this value will start at 100%
- maybe there could be a separate parameter for even & odd values, so for a step sequence, the odd value would essentially add swing

crow input destiations
- function 1 & 2 gate in
- output 1-5 transpose (oct or scale degree)
- global clock
- UI either in the mix menu or as the K1 alt screen (I like mix menu)

engine output (orgn)

## implementation

sequences
- data stored for each step (regardless of mode)
  - notes
    - x position
    - y position
    - duration (% of step duration)
    - slew amount
    - nudge (first note uses step nudge (so first note is 0))
  - nudge (or, +/- distance to nearest step, % of step duration)
- each step may contain multiple notes, which are sorted in order in an array
- if note nudge + note durations + note nudges >= step size then last gate down in skipped (gate tie)
- steps are either
  - iterated over by high resolution, globally synced clock
  - (for live, async mode) called in its own free-running loop, starting a new delay every step
- option: could even consider implimenting live+async just like live+sync, except allowing partial banks. by the time I've done everything else, this might just be easier.
  - yes
  - in this sense, the sync button simply controls whether the sequence loops through whole banks or loops back at the last step
    - also, this simplified definition of "sync" would make this more of a playback setting rather than a record setting, so now it makes sense to have it be a track level option rather than a pattern level option (so we can move it off the main page & into the tracks menu)
  - also allows quantization for async, which is more intutive
  - the downsides
    - the loop length in this mode would be quantized to steps, but I think I'm OK with this
    - we'll definitely want to figure out multiple CVs/gates per-step, or else playing quickly just won't be possible at a low or normal tempos. I don't think it's anything to be spooked about though
- be sure to use base 0 logic throughout the keyboard so the CV mix mode maths work as intended
