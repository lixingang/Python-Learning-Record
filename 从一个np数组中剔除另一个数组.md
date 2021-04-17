```
a = np.arange(1,16)
b = np.arange(1,10)
c = a[[i not in b for i in a]]

return: 11,12,13,14,15
```
