
# Part 1
## Idea

- pad the start and end with space
- `/\d` to get to the next number
- yank it
- determine the length
- macro to check if a char is a symbol (I think we might want to keep a count and then do a
- comparison at the end)
- run that macro on each char around the number, using the length in the x axis, if we see no symbols,
- replace the number with spaces
- loop for every number
- remove symbols
- join and replace whitespace with + to sum them

## Steps

This one is complex... There's a subprocess!

Pad with `.` around the entire file
- `:%norm i.`
- `:%norm A.`
- `:let @a = col('$') - 1`
- `:norm ggO`
- `:norm @ai.`
- `:norm Go`
- `:norm @ai.`

Remove all dots. just b/c I like the look
- `:%s/\./ /g`
- `:norm gg`

Match all the numbers, so that I know how many times to repeat the macro, and this is also how
I traverse
- `:let @n = "/\\d\\+\<CR>"`
- `:norm @n`

Create the macro that adds 1 to a counter if there is a symbol at the current cursor pos
- `:let @t = "\"oyl:let @x = @o == \" \" ? @x : @x + 1\<CR>"`

Count the number of numbers that we need to check
- `:let @v = searchcount(#{recompute: 1, maxcount: 0})["total"]`

Macro to invoke the subprocess which counts the number of symbols surrounding a number, if there's
0 symbols, deletes the number and then goes next
- `:let @r = ":so ./day03/part1.1\<CR>"`

Run it @v times
- `:norm @v@r`

Remove all the symbols, clean up whitespace, put + signs between things, and do math
- `:%s/[^0-9 ]/ /g`
- `:%s/\n/ /`
- `:%s/\s*$//`
- `:%s/^\s*//`
- `:%s/\s\+/+/g`
- `:s/\s/+/g`
- `:norm VD`
- `:let @a=eval(@")`
- `:norm "ap`


### part1.1

Counter
- `:let @x = 0`

Yank the number, and store it's length (+ 1 b/c that's what we need)
- `:norm "cyiw`
- `:let @l = len(@c) + 1`

"Direction"
- `:let @d = "h"`

Setup a macro to move by direction and then invoke @t defined above
- `:let @q = "@d@t"`

Invoke @q a few times, changing the direction as we go, and using the length that we stored above
- `:norm @q`
- `:let @d = "j"`
- `:norm @q`
- `:let @d = "l"`
- `:norm @l@q`
- `:let @d = "k"`
- `:norm 2@q`
- `:let @d = "h"`
- `:norm @l@qjl`

Decide if we're going to delete this one or keep it
- `:exe @x == 0 ? "norm viwr " : ""`

Go next
- `:norm @n`

## result
514969

# Part 2
## Idea


## Steps


## result
