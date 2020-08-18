# 如何更改matplotlib的字体


### 1.找到路径

![image-20200724143025685](https://img2.ibolee.com/git_blog/image-20200724143025685.png)

把下载好的windows字体复制到这个文件夹下的ttf文件夹

### 2.修改文件



修改上图文件路径如下:

![image-20200724143801871](https://img2.ibolee.com/git_blog/image-20200724143801871.png)

最后一处修改为下图样式,并去掉前面的#号:

![image-20200724144014250](https://img2.ibolee.com/git_blog/image-20200724144014250.png)



### 3.删除缓存文件

C:\Users\Administrator\ .matplotlib

  ### 4.重启annaconda

### 5.重启以后在anaconda中添加代码:

```
plt.rcParams['font.sans-serif'] = ['SimHei']
```


