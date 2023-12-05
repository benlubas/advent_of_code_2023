
# Part 1
## Steps
1. Remove chars that aren't digits
- `:%s/\D*\(\d\)\D*/\1/g`
2. Duplicate single digits
- `:%s/^\d$/&&/`
3. Get the first and last digit of each line
- `:%s/\D*\(\d\).*\(\d\)\D*/\1\2/g`
4. Combine onto one line (bang b/c I have visual `J` mapped to move lines around)
- `:norm! vipJ`
5. replace spaces with +
- `:s/ /+/g`
6. do math, and paste the result
- `:norm VD`
- `:let @a=eval(@")`
- `:norm "ap`

## result
54990

# Part 2
## Steps
1. Replace number words with their digit, taking care to deal with portmanteaus
- `:%s/eight/e8t/ge | %s/one/o1e/ge | %s/two/t2o/ge | %s/three/t3e/ge | %s/four/f4r/ge | %s/five/f5e/ge | %s/six/s6x/ge | %s/seven/s7n/ge | %s/nine/n9e/ge`
2. Run steps from above

## result
54473
