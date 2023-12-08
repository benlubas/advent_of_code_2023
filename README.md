# AOC in (neo)Vim

Solutions to some Advent of Code 2023 problems using mainly tools exposed by the vim text editor.

Inspired by @denvaar on youtube.

## Using this repo

Each day gets its own folder, inside each folder there are a few files: a markdown file, explaining
what each step does; a text file with problem input; a part1 file with the vim commands that solve
part1; and similarly for part2. More complex days also have an example file.

### Running

Running a solution is as simple as opening the input file, and running an `:so` command. If I wanted
to run day 1 part 1, I open `./day01/day01.txt`, and run `:so ./day01/part1` this takes the text in
the part1 file as vim commands (one on each line), and runs them all, which produces the answer from
the input file.

## Common tricks or how to do things

### Math
The most common 'trick' used is the expression register to do math that's written out in the buffer.
If I have 1+2+3 written in the buffer, I can evaluate this by yanking it, `yiW`, entering insert
mode and pressing `<c-r>=<c->"`. see `:h expr-register`. The way I do it is similar but not quite
the same. b/c I'm using `:so` to run these from a file, insert mode doesn't work that well. so I use
`:let @<reg>` and `eval` and then paste from the register. But works basically the same.

### Search and Replace
Search and replace is used _heavily_ to solve these problems. And in ways that you might not be
familiar with, in order from most to least useful (subjectively):

- non-greedy (`:h non-greedy`)
`:s/.\{-}hi` will match as few chars as possible before matching 'hi'. where `:s/.*hi` will match as
many as possible. This is the difference between matching "hi" vs "hi there hi" in the string: "hi
there hi there"

- `:s//\=` entering expression land (`:h sub-replace-\=`)
You can sub expressions with `\=` and everything after is just an expression. use `submatch(0)`
0 indexed to access capture groups

- e flag
the e flag just prevents `:s` expressions from erroring if they don't match anything

