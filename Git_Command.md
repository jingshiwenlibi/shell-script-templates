### git blame
-w will ignore whitespaces and -M will detect moved or copied lines.
```
git blame -w -M
```

### git reset
HEAD is the latest commit, and HEAD^ is 2nd latest commit.
```
git reset --soft HEAD
git reset --soft HEAD^
git reset --hard HEAD
```


## If auto-generated file is really generated automatically? 
### Limitation: only check the latest commit for a specific file

### Approach
```
bool is_auto_generated():
  1. git log -5 xxx/xxx.go
  2. if this last commit is a [revert] commit, skip checking this file for this time. return true.
  3. check if timestamp in file is after the 2nd-latest commit.
  4. if NOT true, return false.
  5. return true.
```

### Edge case
```
    Revert "Merge branch 'XXX' into 'YYY'"

    This reverts merge request !1234
```
