```
# 把普通标签编码成独热编码
import torch
batch_size = 5
nb_digits = 10 #类别个数
y = torch.LongTensor(batch_size,1).random_() #待独热编码的标签
y_onehot = torch.FloatTensor(batch_size, nb_digits)
y_onehot.zero_()
y_onehot.scatter_(1, y, 1)
print(y)
print(y_onehot)
```

```
#把独热编码解码成普通标签
one_hot = torch.tensor([[0,0,1],[0,1,0],[0,1,0]])
print(one_hot)
label = torch.argmax(one_hot, -1)
# label = torch.topk(one_hot, 1)[1].squeeze(1)
print(label)
```
```

```
