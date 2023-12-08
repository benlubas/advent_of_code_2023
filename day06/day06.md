
# Part 1

## Steps

Convert into "time number"
- `:%s/.\{-}\s\+//`
- `:%s/\s\+/ /g`
- `:let @q = "jdwkelpi"`
- `:norm gg3@qJ`

Pad with newlines
- `:%s/\n/\r\r/`

Setup macros to write out `time` 0s and use `g<C-a>` to create 1-`time` in a paragraph and then
search and replace with expression to do some math on each line
- `:let @k = ":s/.*/\\=submatch(0) * (@t-submatch(0)) > @d\<CR>"`
- `:let @n = "\"tyiww\"dyiwo@to0vipgvip@k:norm! vipJ\<CR>:s/ /\\+/g\<CR>"`

Apply macros
- `:norm gg@njj@njj@njj@n`

Cleanup original numbers and blank lines
- `:g/\d\+ \d\+/d _`
- `:g/^$/d _`

Add () to each line
- `:%norm I(A)`

Do math
- `:norm! vipJ`
- `:s/ /*/g`
- `:norm VD`
- `:let @a = eval(@")`
- `:norm "ap`

## result

741000

# Part 2

## Steps


## result
