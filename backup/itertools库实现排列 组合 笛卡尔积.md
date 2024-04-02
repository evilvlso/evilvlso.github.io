# 排列 (itertools.permutations)

从迭代序列里选取n个数字进行排列，有顺序

```python
a=[1,3,4]
list(itertools.permutations(a,2))
[(4, 1), (4, 3), (1, 4), (1, 3), (3, 4), (3, 1)]

list(itertools.permutations(a,3))
Out[36]: [(4, 1, 3), (4, 3, 1), (1, 4, 3), (1, 3, 4), (3, 4, 1), (3, 1, 4)]
```

## 组合(itertools.combinations)

从迭代序列里选取n个数字进行组合，重在组合

```python
a=[1,3,4]
list(itertools.combinations(a,2))
Out[32]: [(4, 1), (4, 3), (1, 3)]

list(itertools.combinations_with_replacement(a,2))
Out[33]: [(4, 4), (4, 1), (4, 3), (1, 1), (1, 3), (3, 3)]  #可重复利用数字
```

## 笛卡尔积(itertools.product)

对多个迭代器进行笛卡尔积组合，参数的意思是从每个迭代器中选取几个值进行组合

```
a=[1,3,4]
list(itertools.product([1,2,3],[2,3,4],repeat=2))
```
