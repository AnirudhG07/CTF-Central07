# natas24

If you read about `strcmp`, it messed up when you compare it with non string values. When you enter an empty array, it returns NULL or 0, which is exactly what we want. But if we input `[]`, it will be taken as `"[]"`, which is not what we want.
Thus you can simply change the link from `passwd=` to `passwd[]=[]` i.e. no need to input anything simply change the link and we are done.