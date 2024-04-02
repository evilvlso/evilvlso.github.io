## label转one_hot编码的方法

1. 常见的是用numpy的方法，代码如下：

   ```python
    y= cv2.imread(maskPath,cv2.IMREAD_GRAYSCALE)
    y= cv2.resize(y,(self.image_size,self.image_size))
    y[y<=100]=0  #背景类
    y[y>100]=1   #病灶类
    y_onehot=np.eye(self.num_classes)[y.reshape([-1])]
    # 到第五行其实已经成为one_hot编码了,格式为  [[1,0],[1,0],[1,0],[1,0],[1,0],...[0,1],]
    y_onehot=y_onehot.reshape(self.num_classes,self.image_size,self.image_size)
    # 这一步是为reshape，但是这种reshape方式的结果呈现并不是直觉理解的（不是通道值互斥的），原因是因为reshape的原理
    # 正确的应该是
    y_onehot = rearrange(y_onehot,"(h w) c->c h w",h=self.image_size)
   ```

2. pytorch也有one_hot编码方法，代码如下：

   ```python
   from torch.nn.functional as F
   y= cv2.imread(self.Y[index],cv2.IMREAD_GRAYSCALE)
   y= cv2.resize(y,(self.image_size,self.image_size))
   y[y<=100]=0  #背景类
   y[y>100]=1   #病灶类
   # y就是图片的label
   
   y_onehot=F.one_hot(torch.Tensor(y.reshpe(-1).to(torch.int64)),num_classes)
   # 这一步结果是one_hot形式了，下一步需要变换shape就行
   # 注意第一个参数是Tensor类型并且要转为torch.int64
   y_onehot = rearrange(y_onehot,"(h w) c->c h w",h=self.image_size)
   ```

3. keras也有one_host编码方法，随后补充

   ```python
   from keras.utils import to_categorical
   intput=np.array([1,2,3,4])
   y_onehot=to_categorical(input)
   ```