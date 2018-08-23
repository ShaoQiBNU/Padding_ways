CNN的卷积和pool的padding方式说明
=============================

# 一. Padding

> CNN中卷积和pool均涉及到padding方式，padding有两种类型，一种是’SAME’，一种是’VALID’。两种方式的区别在于是否对影像边界进行填充，SAME会对影像边界进行0填充，VALID则不会。两种方式对影像的width和height修改如下：

```
对于SAME，the output height and width are computed as:

	out_height = ceil(float(in_height) / float(strides[1]))

	out_width = ceil(float(in_width) / float(strides[2]))


对于VALID，the output height and width are computed as:

	out_height = ceil(float(in_height - filter_height + 1) / float(strides[1]))

	out_width = ceil(float(in_width - filter_width + 1) / float(strides[2]))


其中，ceil表示向上取整，strides表示步长，filter_width和filter_height表示卷积核参数
```

# 二. SAME和VALID转换

> 有时在CNN中常涉及到SAME方式来替代VALID的情况，例如：

```
输入影像 27 x 27 ，卷积核 5 x 5， stride=1， pad=2(表示在影像上下左右添加两行/列0)， padding方式为valid

按照普通VALID方式，输出影像大小为 (27+4-5+1)/1=27

按照SAME方法，SAME会自动对影像进行填充0操作，输出影像大小为 27/1

```
> 两种方式出来的影像大小一样，并且操作等效，实际编程中，常常为了方便，将卷积方式统一成SAME。


