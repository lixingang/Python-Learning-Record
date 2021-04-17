读取遥感影像
```
image = np.array(gdal.Open(str(self.modis_dir / filename)).ReadAsArray(), dtype='uint16')
image = image[self.apply_bands,:,:]
# image = linearstretch(image,10,16000) # 是否拉伸影像
print('[I] read {} in shape of {}'.format(filename, image.shape))
prototype = gdal.Open(str(self.modis_dir / filename))
geotrans = prototype.GetGeoTransform()
proj = prototype.GetProjection()
try:
    writeTiff(image, str(self.save_dir/filename), prototype=None, datatype=gdal.GDT_UInt16, proj=proj, geotrans=geotrans)
except:
    print("Error,",filename)
```
保存遥感影像
```
def writeTiff(im_data,savepath, prototype=None, datatype=gdal.GDT_Byte,proj=None, geotrans=None):
    Path(savepath).parent.mkdir(parents=True, exist_ok=True)
    savepath = str(savepath)

    im_bands, im_height, im_width = im_data.shape
        #创建文件
    driver = gdal.GetDriverByName("GTiff")
    if prototype is not None:
        dataset = driver.CreateCopy(savepath, prototype, 0, options=['COMPRESS=LZW'])
    else:
        dataset = driver.Create(savepath, im_width, im_height, im_bands, datatype,options=['COMPRESS=LZW'])

        dataset.SetProjection(proj)
        dataset.SetGeoTransform(geotrans)  # 写入仿射变换参数
    # dataset.SetProjection(projection[0]) #写入投影
    for i in range(im_bands):
        dataset.GetRasterBand(i+1).WriteArray(im_data[i])

    del dataset
```

拉伸影像至0-255
```
def linearstretching(img,min,max):
    img=np.where(img > min, img, min)
    img=np.where(img < max, img, max)
    img = (img - min) / (max - min) * 255
    return img
