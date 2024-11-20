# Movements in Nvim

## Some Basics
Format for a vim command: Command Count Motion
| Key Binding | Description |
| ----------- | ----------- |
| d           | delete duhh. This goes to current buffer to paste |
| i/a         | insert/append |
| v/V         | visual/ visual line mode |
| o :visual   | jump between outside of your highlight |
| c           | change selected text |
| %           | jump between opening and closing |

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

## Advanced Motions and Stuff
| Key Binding | Description |
| ----------- | ----------- |
| vi*         | visual block withIn block characters inputted |
| va*         | visual block Around block characters inputted or next occurence |
| yi* ya*     | yank the visual block defined by vi/va* |
| viw         | highlight current word |
| viW         | highlight current text until whitespace |
| di* ci*     | delete or change inner |
| =ap         | re-indent entire paragraph |


### For practice
```
function foo(blaz: {oddly: "long" | "type"}) {
    // ....
}
```
