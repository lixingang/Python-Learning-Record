append()用来添加训练、验证、测试结果
draw()用来利用plt画图输出
```
class var_collection():
    def __init__(self):
        super().__init__()
        self.train_col = []
        self.valid_col = []
        self.test_col = []
    def append(train_v, valid_v, test_v):
        self.train_col.append(train_v)
        self.valid_v.append(valid_v)
        self.test_v.append(test_v)
    def draw(path,dpi=100):
        df = pd.DataFrame({"train":self.train_col, "valid":self.valid_col, "test":self.test_col},columns=['train', 'valid', 'test'])  
        fig = plt.figure()
        ax = sns.lineplot(data=df)
        plt.grid()
        plt.savefig(path,dpi)
```
