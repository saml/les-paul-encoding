# Les Paul Encoding

This is for: http://www.google.com/logos/2011/lespaul.html

You can set `#tune=` parameter. The parameter is base64 encoding of chunks.

# Example Demo

http://saml.github.com/les_paul_encoding.html

# Chunk

Each chunk has the following format:

    <is polyphonic><note value><is 5 bit><delay from previous>
          0            4          0              5
          1            10         1              20

The largest chunk is 32 bits. The smallest chunk is 11 bits.

# `<is polyphonic>`

This is one bit. 0 or 1. If 0, `<note value>` is 4 bits.
If 1, `<note value>` is 10 bits.

# `<note value>`

For monophonic, base 10 values are (the lowest to the highest):

<table>
    <tr><th>note</th>   <th>base 10</th>    </tr>
    <tr><td>G, do</td>  <td>2</td>          </tr>
    <tr><td>A, re</td>  <td>6</td>          </tr>
    <tr><td>B, mi</td>  <td>3</td>          </tr>
    <tr><td>C, fa</td>  <td>0</td>          </tr>
    <tr><td>D, sol</td> <td>7</td>          </tr>
    <tr><td>E, la</td>  <td>1</td>          </tr>
    <tr><td>F#, ti</td> <td>8</td>          </tr>
    <tr><td>G2, do</td> <td>4</td>          </tr>
    <tr><td>A2, re</td> <td>9</td>          </tr>
    <tr><td>B2, mi</td> <td>5</td>          </tr>
</table>


Actual `<note value>` is base 2 reversed. For example, for D, it is not 0111, but 1110.

For polyphonic, `<note value>` is 10 bit. base 10 value in the table is used as the index of the 10 bit array.
For example, for C,E,G2, it is 1101000000.

    1101000000
    || +-------- G2, 4
    |+---------- E,  1
    +----------- C,  0

# `<is 5 bit>`

If `<is 5 bit>` is 0, `<delay from previous>` is 5 bit, base 2, reversed.

If `<is 5 bit>` is 1, `<delay from previous>` is 20 bit, base 2, revversed.

# `<delay from previous>`

Probably 1/100 milliseconds. It's always base 2 and reversed.




