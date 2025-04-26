## Modification of Terrain
There is an option in the WRF namelist called surface_input_source which, if set to 1, will recompute surface inputs in real.exe. If you want to make changes in geogrid output and ensure they are not overwritten in real, you will need to set surface_input_source to 3.

## Hybrid Vertical Coordinate 混合坐标
### 混合垂直坐标

- v3.9  
从WRF v3.9 发行版（2017年春季）开始，在WRF模式中将混合垂直坐标Hybrid Vertical Coordinate (HVC) 选项加入到了现有的地形跟随Terrain Following (TF) 垂直坐标。随着v3.9，HVC选项要求用户同时激活编译时和运行时标志。

- v4.0  
从WRF v4.0 发行版（2018年夏季）开始，混合垂直坐标Hybrid Vertical Coordinate (HVC) 和最初的地形跟随坐标Terrain Following Coordinate (TFC)都可以通过namelist设置可用。这两种选项的代码编译到了模式中。

“强烈”警告用户不要在WRF模型中添加任何直接使用柱气压cloumn pressure的代码（例如mu、mub等）。

### HVC: 它是什么，它有什么

- HVC选项是一个“混合”垂直坐标，因为eta层次是在近地面地形跟随，然后向高空等压面放松。此坐标选项的目的是减少地形对模式顶部的人为影响。real程序和WRF模式需要使用相同的运行时设置（要么TFC，要么HVC）。如果用户混用real和WRF之间（或ideal和WRF之间）的垂直坐标运行时设置，则代码将停止。  
- 已将v4.0 WRF代码修改为使用v4.0之前的输入和横向边界文件，但仅用于选择TF（地形跟随）坐标选项的运行时。  
- 所有ARW-WRF大气测试例子的都能使用HVC选项。自从第一次发布HVC选项以来，为所有ideal cases提供初始化的工作已经完成。对于v4.0，现在所有ideal和real cases都可以使用hybrid_opt=2。

###   选择TF 或 HVC选项

- 要打开HVC运行时选项，在namelist.input文件中设置一个开关：  
&dynamics  
hybrid_opt = 2  
/  
这是一个单条目值，默认情况下通过Registry将其设置为“2”（激活混合坐标选项）。为了完整起见，要显式关闭namelist.input文件中的HVC选项（打开TFC选项），请执行以下操作：  
&dynamics  
hybrid_opt = 0  
/

- 第二个运行时选项可用于HVC功能，它允许用户选择WRF模式表面完全等压的eta 层。设置此值不是凭感觉的，已经把一个应该在全局范围内管用的合理值设置为默认值。为了对模式结果进行敏感性实验，使其达到模型eta坐标变为等压的水平，用户可以修改在namelist.input文件中定义的临界eta层次：  
&dynamics  
etac = 0.2  
/

- 随着etac值的增加（从0增加到1），更多的eta层次随着层次（从模式顶向下）数量的增加受到影响。一方面，这是一件好事，这种“坐标曲面的展平”是HVC选项的全部目的。然而，在地势较高的地区（不一定陡峭或复杂），当etac值大于约etac=0.22时，垂直eta水平被过度压缩。在喜马拉雅高原上，使用10 hPa模式盖时，etac=0.25的值会导致模型故障。在全球范围内，0.2的值被认为是“安全的”。美国东海岸可以使用etac=0.30，而纯海洋区域可能使用etac=0.40。

## 重力波拖曳方案介绍
- WRF 模式中次网格地形重力波拖曳参数化方案中，包含重力波破碎和阻塞拖曳两种作用（Kim and Doyle, 2005），即在 **"gwd_opt = 1"**  设置下，可开启两种参数化方案.  
- 在较新的 WRFv4.3 版中，追加了小尺度重力波拖曳和湍流地形拖曳两种效应，从而使得模式中的 GWD 方案考虑四种作用，此时在 WRF 中的参数化选项为

> “gwd_opt=3”


# Errors in runing WRF

## real.exe  

In Tianhe Starlight cluster (TSC):

>  ----------------- ERROR -------------------
namelist    : NUM_LAND_CAT =         21
input files : NUM_LAND_CAT =         24 (from geogrid selections).
d01 2023-07-22_18:00:00 ---- ERROR: Mismatch between namelist and wrf input files for dimension NUM_LAND_CAT
NOTE:       1 namelist vs input data inconsistencies found.

## geog folder on Tianhe-Starlight cluster

>  **/APP/u22/x86/WRF/geog/**

Add the  folder into the **namelist.wps** file

## Segmentation fault - invalid memory reference
- S it occurs at the first 10 min, 

> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5OTkzNTM5OTldfQ==
-->