### pandas 打开文件编码问题

常见的编码格式三种，gbk，uincode,utf-8,都试试就好了。代码如下：

```
file_path=r'C:\Users\23263\Desktop\test.csv'
mydf=pd.read_csv(file_path,encoding='gbk')
print(mydf)
```
