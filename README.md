# aoc2019
Advent of Code 2019

## 1.1
```bash
cat 1.input \
    | awk '{f+=int($1/3)-2}END{print f}'
```

## 1.2
```
cat 1.input \
    | awk '{f=$1;while(f>=0){f=int(f/3)-2;print f}}' \
    | grep -Ev "\-|^0" \
    | awk '{s+=$1}END{print s}'
```

## 2.1
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

## 2.2
```bash
for noun in $( seq 0 100 ); do for verb in $( seq 0 100 ); do
    if [ $(f $noun $verb) -eq 19690720 ]; then
        echo $(( $noun * 100 +  $verb ))
    fi
done ; done
```
