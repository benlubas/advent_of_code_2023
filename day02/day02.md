
# Part 1
## Idea

We can write regex to match something like "n red" where n is a number < the max amount of red
cubes. Then do that for each color, and when we find a line that doesn't match (ie. there's more
than the possible amount) we delete that line (and it's ID)

## Steps

1. Find any red/green/blue amounts that are greater than the possible values, and mark them VOID
`:%s/\(\d*\) red/\=submatch(0) > 12 ? "VOID" : submatch(0)/ge`
`:%s/\(\d*\) green/\=submatch(0) > 13 ? "VOID" : submatch(0)/ge`
`:%s/\(\d*\) blue/\=submatch(0) > 14 ? "VOID" : submatch(0)/ge`
2. Delete the lines that are marked VOID
`:g/VOID/d _`
3. Get the game IDs
`:%s/Game \(\d*\).*/\1/`
4. Join the game IDs with `+` between
`:norm! vipJ`
`:s/ /+/g`
5. Do math
`:norm VD`
`:let @a=eval(@")`
`:norm "ap`

## result
2545

# Part 2
## Idea

We need to find the max number of each color pulled in each game. The first way I think of doing
this without abusing expression land is by using the sort command.

## Steps

1. remove the Game number prefix
`:%s/Game \d*: /`
2. add a whitespace between each line
`:%s/\n/\r\r/`
3. Split each number/color combo onto it's own line
`:%s/[,;] /\r/g`
4. Sort each games draws by number, high to low
`:let @s = "vip:sort! n\<CR>}j"`
`:norm gg100@s`
5. Go through each game, and pull out the highest number for each color, putting it into an x\*y\*z
   expression on the line above, deleting the games as we go
`:let @k = "ma/red0yiw'ap/blue0yiw'aA*p/green0yiw'aA*pojdapk"`
`:norm ggO100@k`
6. Eval and sum all the x\*y\*z expressions
`:norm! vipJ`
`:s/ /+/g`
`:norm VD`
`:let @a=eval(@")`
`:norm "ap`

## result
78111
