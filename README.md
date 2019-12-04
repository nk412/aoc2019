# aoc2019
Advent of Code 2019

# 1
#### 1.1
```bash
cat 1.input \
    | awk '{f+=int($1/3)-2}END{print f}'
```

#### 1.2
```bash
cat 1.input \
    | awk '{f=$1;while(f>=0){f=int(f/3)-2;print f}}' \
    | grep -Ev "\-|^0" \
    | awk '{s+=$1}END{print s}'
```

# 2
#### 2.1
```bash
f(){
    a=($( cat 2.input | tr ',' ' ' )) && p=0
    a[1]=${1} && a[2]=${2}
    while true; do
        if   [ ${a[$p]} -eq 1 ]; then a[${a[$((p+3))]}]=$((a[${a[$((p+1))]}]+a[${a[$((p+2))]}]))
        elif [ ${a[$p]} -eq 2 ]; then a[${a[$((p+3))]}]=$((a[${a[$((p+1))]}]*a[${a[$((p+2))]}]))
        else break ; fi
        let p+=4
    done
    echo ${a[0]}
}
f 12 2
```

#### 2.2
```bash
for noun in $( seq 0 100 ); do for verb in $( seq 0 100 ); do
    if [ $(f $noun $verb) -eq 19690720 ]; then
        echo $(( $noun * 100 +  $verb ))
    fi
done ; done
```

# 3

```bash
cat 3.input \
    | awk '{print NR" "$0}' \
    | tr ',' '\n' \
    | awk '{if(NF==2){x=$1;print $0}else{print x" "$1}}' \
    | awk '{print $1," ",substr($2,0,1)," ",substr($2,2,10)}' \
    | awk '{while($3>0){print $1" "$2;$3-=1}}' \
    | sed s/'U'/'0 1'/ \
    | sed s/'D'/'0 -1'/ \
    | sed s/'L'/'-1 0'/ \
    | sed s/'R'/'1 0'/ \
    | awk 'BEGIN{x=0;y=0}{if(prev!=$1){x=0;y=0}x+=$2;y+=$3;prev=$1;print $1," ",x","y}' \
    | sort \
    | uniq \
    | awk '{print $2}' \
    | sort \
    | uniq -c \
    | grep -E -v "\s1\s" \
    | awk '{print $2}' \
    | awk -F, '{print ($1<0?-$1:$1)+($2<0?-$2:$2)}' \
    | sort -n \
    | head -n 1
```
    
