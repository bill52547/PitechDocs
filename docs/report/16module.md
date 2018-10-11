# 16模块图像中遇到的问题集合
探测器几何：

* L=33.4mm
* I_radius=99mm
* num_ring=1
* num_block_per_ring=16
* block_size=20\*33.4\*33.4 mm<sup>3</sup>
* block_grid=1\*10\*10
* crystal_size=20\*3.34\*3.34 mm<sup>3</sup>

重建图像：

* image_size= 167\*167\*33.4 mm<sup>3</sup>
* image_grid= 100\*100\*10

重建图像如下：
![avatar](../picture/16module_with_problems.png)
![avatar](../picture/16module_with_problems(2).png)
![avatar](../picture/16module_with_problems(3).png)

实际数据中也是有相同的问题
![avatar](../picture/d12_with_line.png)
![avatar](../picture/d12_with_line(2).png)
![avatar](../picture/d12_with_line(3).png)

## 重建图像横竖黑线问题
原因说明：当晶体crystal size为图像pixel size的倍数（2倍）时，会出现有规律的横竖黑线问题；当z轴方向pixel size等于crystal size时，黑线问题最严重。
解决方法：
a.改变图像pixel size的尺寸，使之与crystal size不成倍数关系
下图是将每个pixel size大小设置为2 mm\*2 mm\*2 mm,得到结果
![avatar](../picture/16module_without_line.png)
![avatar](../picture/16module_without_line(2).png)
![avatar](../picture/16module_without_line(3).png)

b.将每个晶体上的事件的位置作高斯分布，而非归类到晶体中心位置


## 重建图像中黑色圆环问题
原因说明：当每个block上的晶体数量为10\*10或者20\*20的时候，出现圆环状的伪影。
解决方法：
a.将每个block上的晶体数量改为15\*15
下图是重建结果
![avatar](../picture/16module.png)
![avatar](../picture/16module(2).png)
![avatar](../picture/16module(3).png)


# 16模块实际数据重建结果记录
重建图像：

* image_size= 180\*180\*20 mm<sup>3</sup>
* image_grid= 90\*90\*10

## 12 cm直径flood phantom重建错误图像
![avatar](../picture/d12_with_problems.png)
![avatar](../picture/d12_with_problems(2).png)
![avatar](../picture/d12_with_problems(3).png)


## 15 cm直径flood phantom重建错误图像


重建结果如下所示：
![avatar](../picture/d15_some_problems.png)
![avatar](../picture/d15_some_problems(2).png)
![avatar](../picture/d15_some_problems(3).png)

其中两两模块之间符合事件统计如下所示：
![avatar](../picture/d15ruili.png)

手动使用其他模块数据补充到第4模块，得到的两两模块之间符合事件统计如图：
![avatar](../picture/d15ruili_modified.png)

得到的相应重建结果如下图所示：
![avatar](../picture/d15_modified.png)
![avatar](../picture/d15_modified(2).png)
![avatar](../picture/d15_modified(3).png)


##  18 cm直径flood phantom重建错误图像
重建结果如下所示：
![avatar](../picture/d18_with_problems.png)
![avatar](../picture/d18_with_problems(2).png)
![avatar](../picture/d18_with_problems(3).png)