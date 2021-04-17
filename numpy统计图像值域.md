有时候遥感图像中存在异常值，想要获取真正的值域，需要得到次大值和次小值，以下为找到的较为简洁的解决方案：
利用numpy的unique功能，可以快速地统计图像中地最大值、次大值、最小值、次小值等信息，方便排除异常值
```
stat = {"max":[],"max_2":[],"min":[],"min_2":[],"mean":[],"std":[]}
for i in [modis_dir, pre_dir, tmp_dir, soil_dir]:
    filenames = glob.glob(join(i,"*.tif"))
    crt = filenames[0]
    crt = gdal.Open(crt).ReadAsArray()
    crt = np.unique(crt)
    stat["max"].append(crt[-1])
    stat["max_2"].append(crt[-2])
    stat["min"].append(crt[0])
    stat["min_2"].append(crt[1])
    stat["mean"].append(np.mean(crt))
    stat["std"].append(np.std(crt))
   
    
stat = pd.DataFrame(stat, index=None)
print(stat)
```
