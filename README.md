CNN的卷积和pool的padding方式说明
=============================

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

