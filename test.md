```
CASE1
   let accumulator = 0;
    for (let i = 1; i <= 10; i++) {
        accumulator += i;
    }
    console.log('accumulator : {}',accumulator)



CASE2
    const sum = (v,acc) => v > 1 ? sum(v-1, acc+v) : acc+1;
    const sums = v => sum(v, 0);
    console.log('sum : {}',sums(10))



CASE3
    const vV1= 10;
    let accV1 = 0;
    for (let i = vV1; i > 1; i++) {
        accV1 += i;
    }
    accV1++;
    console.log('accV1 : {}', accV1)
```
