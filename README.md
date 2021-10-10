![](scriptorium1.png)

# Hacks in the Terminal

Problem solving with `AWK` … More stuff is still hosted here: [Wordpress](http://awkologist.com)

### fasta2tbl

A way to transform FASTA to tab delimited

```awk
#!/bin/bash
awk '
{
if (substr($1,1,1) == ">"){
  if (NR>1){
    printf "\n%s ", substr($1,2,length($1)-1)
  }
  else{
    printf "%s ", substr($1,2,length($1)-1)
  }
  }
else{
  printf "%s", $0
  }
}
END{printf "\n"}' "$@"
```

### tbl2fasta

A way to transform tab delimited to FASTA

```awk
#!/bin/bash
awk ‘{
seq = $2
l = length(seq)
i = 1
printf ">%s\n", $1
while (i <= l){
  printf "%s\n", substr(seq,i,80)
  i=i+80
}
}’ "$@"
```

