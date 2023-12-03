# AOC in (neo)Vim

Solutions to some Advent of Code 2023 problems using mainly tools exposed by the vim text editor.

Inspired by @denvaar on youtube.

## How it works

Each day gets its own folder, inside each folder there are a few files: a markdown file, explaining
what each step does; a text file with problem input; a part1 file with the vim commands that solve
part1; and similarly for part2.

### Running

Running a solution is as simple as opening the input file, and running an `:so` command. If I wanted
to run day 1 part 1, I open `./day01/day01.txt`, and run `:so ./day01/part1` this takes the text in
the part1 file as vim commands (one on each line), and runs them all.
