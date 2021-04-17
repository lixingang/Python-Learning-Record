遥感图像通常有很多波段，日常的cv库无法满足可视化要求，一种方案是通过matplot的subplot进行可视化，但是比较繁冗。

利用`torchvision.util.make_grid()`函数，结合以for循环，可快速展示多通道图像，make_grid的其他参数见pytorch文档

```
# 可视化
plt.rcParams['figure.figsize'] = (80.0, 80.0)
shp=crt_modis.shape
crt_modis_vis =np.reshape(crt_modis[0:shp[0]//3*3,:,:],(shp[0]//3,3,shp[-2],shp[-1])).astype(np.float32)
crt_modis_vis = torch.tensor(crt_modis_vis)
print(crt_modis_vis.shape)
rlt = torchvision.utils.make_grid(crt_modis_vis, normalize=True)

plt.imshow(np.transpose(rlt,(1,2,0)))
```
