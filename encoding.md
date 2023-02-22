# Encoding of Music

This encoding system uses a top-down approach. That is, define the most overarching features of a score (i.e. instruments, staves, clefs) which will allow for the further implementation of the actual music.

## Beginning Information

Observe the beginning of the score could look like this:

    #T: Score_Title
    #S: Score_Subtitle
    #A: Score_Author(s)
    #C: Score_Copyright

This defines the most surface-level information about the score. It is efficient to write and makes sense when viewing (it makes sense that `#T` refers to the title of the score, `#S` refers to the subtitle, etc.).

## Representing Music

In order to support more complex tasks such as hiding staves for certain measures, adding more instruments, etc. this encoding system uses a **measure-by-measure** approach.

```
test code
```
