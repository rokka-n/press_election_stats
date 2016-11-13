# Press and statistics

## Get a list of headlines

Grep by candidates mentions, clean up it from html tags

```
for i in `seq 1 30`; \
  do curl http://www.huffingtonpost.com/archive/2016-10-$i | \
  grep -i "trump\|hillary" | \
  sed -e 's/<[^>]*>//g'  >> headlines.txt; \
done
```

## Cleanup from whitespaces and mentions only names on signle line

`sed -i 's/^ *//; s/ *$//; /^$/d; /^\s*$/d; s/^ *//g' headlines.txt  # remove leading whitespaces`

`egrep -v "^Donald Trump$"\|"^Hillary Clinton$" headlines.txt > headlines1.txt # remove single mentiones`

## Count statistics of mentions

Don't count mentions where both names present in one line.

First candidate was mentioned 570 times:
```
$ egrep -i trump headlines1.txt | grep -iv hillary | wc -l
570
```

The other was mentioned... 84

```
$ egrep -i hillary headlines1.txt | grep -iv trump | wc -l
84
```

Lol
