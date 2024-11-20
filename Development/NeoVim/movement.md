# Movements in Nvim

## Horizontal movements
| Key Binding | Description |
| ----------- | ----------- |
| w/b         | move forward/back through words |
| _           | begining of text on current line |
| 0/$         | jump to 0 or end of line | 
| f*/t*       | jump forward/to the typed character. Use ;/, to move next/prev |
| F*/T*       | jump backward/to the typed character. Use ;/, to move next/prev |
| I/A         | move to beginning/end of line and enter insert mode | 
| o/O         | insert a newline below/above pos and enter insert mode |

Don't forget that we can use all of these motions with actions like 'd'.
For example, 'df(' would delete everything from the cursor to the first
occurence of a '('.

## Vertical Movements
| Key Binding | Description |
| ----------- | ----------- |
| {/}         | jump based on paragraph |
| C-d/u       | jump by half page |
| gg/G        | jump to top/bottom of file |
| :<line>     | go to line number |
| /__  ?__    | search forward/backward |
| astr/octo   | search for selected word |

## Buffers
A window contains a buffer.
A buffer is some representation of the file below (kept in memory).

## Advanced Motions
