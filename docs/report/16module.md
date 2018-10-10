# 16模块图像中遇到的问题集合
探测器几何：

* L=33.4mm
* I_radius=99mm
* num_ring=1
* num_block_per_ring=16
* block_size=20x33.4x33.4 mm<sup>3</sup>
* block_grid=1x10x10
* crystal_size=20x3.34x3.34 mm<sup>3</sup>

重建图像：

* image_size= 167x167x33.4 mm<sup>3</sup>
* image_grid= 100x100x10

重建图像如下：
![avatar](../picture/16module_with_problems.png)

## 重建图像横竖黑线问题
原因说明：当晶体crystal size为图像pixel size的倍数（2倍）时，会出现有规律的横竖黑线问题；当z轴方向pixel size等于crystal size时，黑线问题最严重。
解决方法：
a.改变图像pixel size的尺寸，使之与crystal size不成倍数关系
下图是将每个pixel size大小设置为2 mm*2 mm*2 mm,得到结果
![avatar](../picture/16module_without_line.png)

b.将每个晶体上的事件的位置作高斯分布，而非归类到晶体中心位置



## 重建图像中黑色圆环问题
原因说明：当每个block上的晶体数量为10*10或者20*20的时候，出现圆环状的伪影。
解决方法：
a.将每个block上的晶体数量改为15*15
下图是重建结果
![avatar](../picture/16module.png)




# 16模块实际数据重建结果记录
