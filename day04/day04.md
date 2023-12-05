
# Part 1

## Steps

Count lines
- `:let @x = line('$')`

Transform text such that games are separated by two newlines, and numbers are on their own line
- `:%s/  / /g`
- `:%s/.*: //`
- `:%s/\n/\r\r`
- `:%s/ | /\r`
- `:%s/ \+/\r/g`
- `:norm gg`

Record a macro that counts the starting number of numbers, removes dups, and then counts them again.
write the score using this information
- `:let @k = "jvip:let @a = line(\"'>'€kb\") - line(\"'<\") + 1gv:sort uvip:let @b = line(\"'>\") - line(\"/€kb'<\") + 1:let @c = @a - @bO:exe @c > 0 ? \"norm i1\" : \"\":exe @c > 1 ? \"norm \" .. (@c - 1) .. \"A*2\" : \"\"gvd"`

reply macro number-of-games times
- `:norm @x@k`

add everything up
- `:g/^\s*$/d _`
- `:norm! vipJ`
- `:s/ /+/g`
- `:norm VD`
- `:let @a = eval(@")`
- `:norm "ap`

## result
22488

# Part 2
## Idea

This is going to have to be way different. Might not be possible b/c it's exponential in the number
of cards.. We need to do dynamic programming somehow.

## Steps


## result
