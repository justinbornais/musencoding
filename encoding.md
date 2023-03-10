# Encoding of Music

This encoding system uses a top-down approach. That is, define the most overarching features of a score (i.e. instruments, staves, clefs) which will allow for the further implementation of the actual music.

## Beginning Information

Observe the beginning of the score could look like this:

```
#T: Score_Title
#S: Score_Subtitle
#A: Score_Author(s)
#C: Score_Copyright
```

This defines the most surface-level information about the score. It is efficient to write and makes sense when viewing (it makes sense that `#T` refers to the title of the score, `#S` refers to the subtitle, etc.).

## Representing Music

In order to support more complex tasks such as hiding staves for certain measures, adding more instruments, etc. this encoding system uses a **measure-by-measure** approach. To maintain ease of visibility, each measure gets its own section:

```
M1:4/4
  P1.1G: a4.5 b4.5 cs5.4_b4.4_a4.4
  P1.2F: a2/e3.7

M2:
  P1.1G: cs5.4 Cs5.4 b4.4 b4.4 a4.6
  P2.2F: a2/e3.7
```

The above shows a lot of useful details. The heading is `M1` to signify the first measure. `M2` would equally signify the second measure, `M3` the third measure, etc.
- The first measure needs a time signature. The second and following measures don't need to write the time signature explicitly unless they're changing it.
- If a measure has notes adding up to more than the allowed beats per measure should simply be discarded.

The `P` blocks refer to the parts. They can be represented in decimal format, understood as the following:
- The whole number portion refers to the instrument number.
- The decimal refers to the staff number (the above example would likely refer to a piano labelled instrument one).
- The letter refers to the clef. G refers to the treble clef (or G clef), while F refers to the bass clef (or F clef).
- Note: to support suddenly adding instruments above the top instrument, any part can be given an instrument number of 0 or even a negative value.

The notes are represented in parts like this, each note separated by a space:
- Start with the letter of the note (a-g). Can be uppercase or lowercase.
- Use an `s` to represent a sharp, a `b` to represent a flat. Note: writing `bb4` would represent a B-flat.
- Use a number to represent the octave. By convention, **Middle C is C4**.
- Use a dot and then the number for the duration. By convention, a quarter note is `5`. Numbers smaller than 5 are faster, and numbers larger than 5 are bigger.
  - Can be a negative number if you need something faster than a 64th note.
  - For dotted durations, such as a dotted quarter note, just write `5.` So a dotted quarter note of G in the fourth octave would be `g4.5.`
- To have multiple notes in a chord, use a forward slash `/` before the duration.
  - Implementation of separate voices will be thought about later. Could potentially further break the part into voices.
- If you have repeated notes (i.e. 4 `G4`'s in a row each with the same duration, simply add a number before the letter name. For example: 4 G4 quarter notes would look like `4g4.5`. For different durations (i.e. a quarter note followed by a half note), use multiple dots: `2g4.5.6`
  - If the duration uses a dot, it will work the same. For example: 2 G4s, one a dotted half note, the other a quarter note, it would be `2g4.6..5`
- To slur different notes, use an underscore instead of a space.

## Sample Encoding

Here is the sample score also available in the repository:
![Sample Score](/sample.jpg?raw=true "Sample Score")

The encoding of this score would look like this:
```
#T: Epic Song
#S: What an Amazing Song
#A: Justin Bornais
#C: All Rights Reserved

M1:4/4
  P1.1G: c4.5 d4.5 e4.5 c4.5
  P1.2F: c3/g3.7
M2:
  P1.1G: f4.5 g4.5 c4/g4.6
  P1.2F: c3/f3.6 c3/e3.6
M3:3/4
  P1.1G: e4.4_d4.4_c4.5 c4.5
  P1.2F: 3g3.5
M4:4/4
  P1.1G: c4/c5.7
  P1.2F: c3.6 c2.6
```
