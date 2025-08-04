---
layout: post
title: simple MIDI to list of (frequency, duration) (Python)
---

# simple MIDI to list of (frequency, duration) (Python)

Let's say, hypothetically, that you have a simple midi file with just notes, for instance, [from here](https://onlinesequencer.net/2713476#).

And for the sake of the argument, you have a MicroPython-controlled device with a buzzer, that you want to play this MIDI on.

Wouldn't it then follow, that you want to convert this midi into something easy to play back?

No need to try and use stuff like `librosa` - the [`pretty_midi`](https://pypi.org/project/pretty_midi/) library will do just fine.
`pip install pretty_midi`, then

```python
import math
import pretty_midi
midi_data = pretty_midi.PrettyMIDI('smasnug.mid')

freqs = []

prev_end = 0
for note in midi_data.instruments[0].notes:
    delay = note.start - prev_end
    if delay != 0:
        #print(delay)
        freqs.append((0, round(delay, 2)),)
    #print(note, pretty_midi.note_number_to_hz(note.pitch))
    freq = pretty_midi.note_number_to_hz(note.pitch)
    duration = note.end-note.start
    freqs.append((round(freq, 2), round(duration, 2)),)
    prev_end = note.end

print(freqs) # this is our list of freq/duration
```
## MicroPython example

```python
pp = Pin(14, Pin.OUT, None)
p = PWM(pp)

#######################################
# SMASNUG MODE ACTIVATED
#######################################

print("SMASNUG")
notes = [(659.26, 0.22), (0, 0.08), (880.0, 0.22), (0, 0.08), (880.0, 0.22), (0, 0.07), (1108.73, 0.22), (0, 0.08), (1108.73, 0.22), (0, 0.07), (880.0, 0.6),
 (659.26, 0.23), (0, 0.08), (659.26, 0.15), (0, -0.15), (659.26, 0.15), (0, 0.15), (659.26, 0.38), (0, 0.08), (659.26, 0.15), (987.77, 0.15), (880.0, 0.15),
(830.61, 0.15), (739.99, 0.15), (659.26, 0.52), (0, 0.38), (659.26, 0.22), (0, 0.08), (880.0, 0.22), (0, 0.08), (880.0, 0.3), (1108.73, 0.23), (0, 0.07), (11
08.73, 0.23), (0, 0.08), (880.0, 0.45), (0, 0.15), (659.26, 0.22), (0, 0.08), (880.0, 0.23), (0, 0.07), (830.61, 0.3), (739.99, 0.15), (830.61, 0.15), (880.0
, 0.23), (0, 0.07), (622.25, 0.3), (659.26, 0.52), (0, 0.38), (659.26, 0.3), (830.61, 0.22), (0, 0.08), (830.61, 0.3), (880.0, 0.15), (830.61, 0.15), (739.99
, 0.15), (830.61, 0.15), (880.0, 0.45), (0, 0.15), (659.26, 0.22), (0, 0.07), (880.0, 0.3), (830.61, 0.22), (0, 0.08), (830.61, 0.22), (0, 0.07), (830.61, 0.
15), (1174.66, 0.15), (987.77, 0.15), (830.61, 0.15), (880.0, 0.53), (0, 0.38), (880.0, 0.22), (0, 0.08), (739.99, 0.22), (0, 0.07), (739.99, 0.23), (0, 0.07
), (739.99, 0.22), (0, 0.08), (880.0, 0.22), (0, 0.07), (880.0, 0.53), (0, 0.07), (659.26, 0.23), (0, 0.07), (659.26, 0.23), (0, 0.07), (659.26, 0.38), (0, 0
.07), (659.26, 0.15), (987.77, 0.3), (830.61, 0.3), (880.0, 0.52), (0, 0.38), (880.0, 0.22), (0, 0.07), (830.61, 0.15), (739.99, 0.07), (0, 0.07), (739.99, 0
.23), (0, 0.07), (739.99, 0.15), (880.0, 0.15), (830.61, 0.15), (987.77, 0.15), (880.0, 0.52), (0, 0.07), (659.26, 0.23), (0, 0.07), (659.26, 0.23), (0, 0.07
), (659.26, 0.38), (0, 0.07), (659.26, 0.15), (987.77, 0.3), (830.61, 0.3), (880.0, 0.6), (0, 0.15), (1108.73, 0.23), (0, 0.07), (1318.51, 0.15), (987.77, 0.
15), (1108.73, 0.15), (880.0, 0.15), (739.99, 0.23)]
for freq, duration in notes:
    p.duty_u16(0)
    if freq == 0:
        pass
    else:
        p.freq(int(freq))
        p.duty_u16(4096)
    sleep(duration)

p.duty_u16(0)
p.freq(2048)

print("SMASNUGN'T")
```

have fun making noises lmao

If you think that this is bad advice, contact me somehow and let me know. Cheers!
