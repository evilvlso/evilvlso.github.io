# Golang碎片化学习笔记

- `counter := map[int]int{}  和 counter := make(map[int]int)`是等价的，直接上去{}初始化更装

- 对slice，map进行for遍历，得到的值取决于用几个值接收

  ```Golang
  for i,k := range slice  #i为索引  k为值
  for i := range slice # 则i仅为索引
  
  for k,v := range map  # key value都能取到
  for k := range map # 只有k
  ```

- `make`创建的slice map 会初始化为该类型的零值，返回变量

  ```Golang
  a:=make([]int,2)
  a[0]  #0 
  a[1]  # 0
  ```

- `container/list`这是一个双向链表，他的主要方法有：

  ```Golang
  l:=list.New()
  l.Front()
  l.Back()
  l.PushBack(你的数据)
  l.PushFront(你的数据)
  l.Remove(e) #e一定是他的Element类型 比如 l.Front 而不是你的数据  e.Value才是你的数据
  l.MoveFront(e) #e是Element类型 将要移动的数据
  l.MoveBack(e)
  ```


- 字符串遍历的结果是???

  ```go
  a := "asdasf"
  for _, c := range a {
    fmt.Println(c)
  }
  #97
  115
  100
  97
  115
  102
  a := "够神呐虐"
  for _,i := range a {
    fmt.Println(i)
  }
  #
  22815
  31070
  21584
  34384
  ```

- Slice取最后一个元素 索引不能是-1 

  ```go
  	a := []int{}
  	fmt.Println(a[-1])  # must be a non-negtive
  	fmt.Println(a[len(a)-1])
  ```

- `len()`获得的中文字符串长度不是你想的，获取的是字节长度

  ```
  	a := "够神呐虐"
  	fmt.Println(len(a)) # 12 fuck
  	b := []rune(a)   # 4
  	b := []byte(a)  # 4  
  ```


-  **Printf、Sprintf、Fprintf区别**

  # ![image-20220427171722010](https://raw.githubusercontent.com/evilvlso/picsbed/master/image-20220427171722010.png)

- 小写变量在**本包内**可以访问

- 字符串匹配

- ```
  pattern []string
  pattern[0]=="a"  ??
  ```

- 使用unicode筛选匹配中文

 ```
  # 匹配所有汉字
  print(re.findall('[\u4e00-\u9fa5]', data))
 ```