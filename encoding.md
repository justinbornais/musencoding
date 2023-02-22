# Encoding of Music

This encoding system uses a top-down approach. That is, define the most overarching features of a score (i.e. instruments, staves, clefs) which will allow for the further implementation of the actual music.

Observe the beginning of the score could look like this:

    #T: Score_Title
    #S: Score_Subtitle
    #A: Score_Author(s)
    #C: Score_Copyright

This defines the most surface-level information about the score. It is efficient to write and makes sense when viewing (it makes sense that #T refers to the title of the score, #S refers to the subtitle, etc.).

