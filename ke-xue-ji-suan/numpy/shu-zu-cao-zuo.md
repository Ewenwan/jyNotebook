# 数组操作例程

## 基本操作

| [`copyto`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.copyto.html#numpy.copyto)（dst，src \[，cast，where\]） | 将值从一个数组复制到另一个数组，并根据需要进行广播。 |
| :--- | :--- |


## 改变数组形状

| [`reshape`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.reshape.html#numpy.reshape)（a，newshape \[，order\]） | 为数组提供新形状而不更改其数据。 |
| :--- | :--- |
| [`ravel`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ravel.html#numpy.ravel)（a \[，order\]） | 返回一个连续的扁平数组。 |
| [`ndarray.flat`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.flat.html#numpy.ndarray.flat) | 数组上的一维迭代器。 |
| [`ndarray.flatten`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.flatten.html#numpy.ndarray.flatten)（\[订购\]） | 将折叠的数组的副本返回到一个维度。 |

## 类似转置的操作

| [`moveaxis`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.moveaxis.html#numpy.moveaxis)（a，来源，目的地） | 将阵列的轴移动到新位置。 |
| :--- | :--- |
| [`rollaxis`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.rollaxis.html#numpy.rollaxis)（a，轴\[，开始\]） | 向后滚动指定的轴，直到它位于给定位置。 |
| [`swapaxes`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.swapaxes.html#numpy.swapaxes)（a，axis1，axis2） | 交换阵列的两个轴。 |
| [`ndarray.T`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ndarray.T.html#numpy.ndarray.T) | 与self.transpose（）相同，只是如果self.ndim &lt;2则返回self。 |
| [`transpose`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.transpose.html#numpy.transpose)（a \[，轴\]） | 置换数组的维度。 |

## 更改维数

| [`atleast_1d`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.atleast_1d.html#numpy.atleast_1d)（\* arys） | 将输入转换为至少具有一个维度的数组。 |
| :--- | :--- |
| [`atleast_2d`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.atleast_2d.html#numpy.atleast_2d)（\* arys） | 将输入视为具有至少两个维度的数组。 |
| [`atleast_3d`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.atleast_3d.html#numpy.atleast_3d)（\* arys） | 将输入视为具有至少三维的数组。 |
| [`broadcast`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.broadcast.html#numpy.broadcast) | 制作一个模仿广播的对象。 |
| [`broadcast_to`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.broadcast_to.html#numpy.broadcast_to)（数组，形状\[，测试\]） | 将数组广播到新形状。 |
| [`broadcast_arrays`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.broadcast_arrays.html#numpy.broadcast_arrays)（\* args，\*\* kwargs） | 相互广播任意数量的数组。 |
| [`expand_dims`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.expand_dims.html#numpy.expand_dims)（a，轴） | 展开数组的形状。 |
| [`squeeze`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.squeeze.html#numpy.squeeze)（a \[，轴\]） | 从数组的形状中删除一维条目。 |

## 改变数组的种类

| [`asarray`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.asarray.html#numpy.asarray)（a \[，dtype，order\]） | 将输入转换为数组。 |
| :--- | :--- |
| [`asanyarray`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.asanyarray.html#numpy.asanyarray)（a \[，dtype，order\]） | 将输入转换为ndarray，但通过ndarray子类。 |
| [`asmatrix`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.asmatrix.html#numpy.asmatrix)（数据\[，dtype\]） | 将输入解释为矩阵。 |
| [`asfarray`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.asfarray.html#numpy.asfarray)（a \[，dtype\]） | 返回转换为float类型的数组。 |
| [`asfortranarray`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.asfortranarray.html#numpy.asfortranarray)（a \[，dtype\]） | 返回在内存中以Fortran顺序布局的数组。 |
| [`ascontiguousarray`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.ascontiguousarray.html#numpy.ascontiguousarray)（a \[，dtype\]） | 在内存中返回一个连续的数组（C顺序）。 |
| [`asarray_chkfinite`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.asarray_chkfinite.html#numpy.asarray_chkfinite)（a \[，dtype，order\]） | 将输入转换为数组，检查NaN或Infs。 |
| [`asscalar`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.asscalar.html#numpy.asscalar)（一个） | 将大小为1的数组转换为标量等效数组。 |
| [`require`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.require.html#numpy.require)（a \[，dtype，要求\]） | 返回满足要求的提供类型的ndarray。 |

## 连接数组

| [`concatenate`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.concatenate.html#numpy.concatenate)（（a1，a2，...）\[，轴，out\]） | 沿现有轴加入一系列数组。 |
| :--- | :--- |
| [`stack`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.stack.html#numpy.stack)（数组\[，轴，出\]） | 沿新轴加入一系列数组。 |
| [`column_stack`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.column_stack.html#numpy.column_stack)（TUP） | 将1-D阵列作为列堆叠成2-D阵列。 |
| [`dstack`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.dstack.html#numpy.dstack)（TUP） | 按顺序深度堆叠阵列（沿第三轴）。 |
| [`hstack`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.hstack.html#numpy.hstack)（TUP） | 按顺序堆叠数组（列式）。 |
| [`vstack`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.vstack.html#numpy.vstack)（TUP） | 垂直堆叠数组（行方式）。 |
| [`block`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.block.html#numpy.block)（阵列） | 从嵌套的块列表中组装nd数组。 |

## 拆分数组

| [`split`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.split.html#numpy.split)（ary，indices\_or\_sections \[，轴\]） | 将数组拆分为多个子数组。 |
| :--- | :--- |
| [`array_split`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.array_split.html#numpy.array_split)（ary，indices\_or\_sections \[，轴\]） | 将数组拆分为多个子数组。 |
| [`dsplit`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.dsplit.html#numpy.dsplit)（ary，indices\_or\_sections） | 沿第3轴（深度）将数组拆分为多个子阵列。 |
| [`hsplit`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.hsplit.html#numpy.hsplit)（ary，indices\_or\_sections） | 将数组水平拆分为多个子数组（按列）。 |
| [`vsplit`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.vsplit.html#numpy.vsplit)（ary，indices\_or\_sections） | 将数组垂直拆分为多个子数组（逐行）。 |

## 平铺数组

| [`tile`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.tile.html#numpy.tile)（A，代表） | 通过重复A重复给出的次数来构造数组。 |
| :--- | :--- |
| [`repeat`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.repeat.html#numpy.repeat)（a，重复\[，轴\]） | 重复数组的元素。 |

## 添加和删​​除元素

| [`delete`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.delete.html#numpy.delete)（arr，obj \[，轴\]） | 返回一个新数组，其子轴数组沿轴被删除。 |
| :--- | :--- |
| [`insert`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.insert.html#numpy.insert)（arr，obj，values \[，axis\]） | 在给定索引之前沿给定轴插入值。 |
| [`append`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.append.html#numpy.append)（arr，值\[，轴\]） | 将值附加到数组的末尾。 |
| [`resize`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.resize.html#numpy.resize)（a，new\_shape） | 返回具有指定形状的新数组。 |
| [`trim_zeros`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.trim_zeros.html#numpy.trim_zeros)（感觉\[，修剪\]） | 从1-D数组或序列中修剪前导和/或尾随零。 |
| [`unique`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.unique.html#numpy.unique)（ar \[，return\_index，return\_inverse，...\]） | 找到数组的唯一元素。 |

## 重新排列元素

| [`flip`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.flip.html#numpy.flip)（m \[，轴\]） | 沿给定轴反转数组中元素的顺序。 |
| :--- | :--- |
| [`fliplr`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.fliplr.html#numpy.fliplr)（M） | 向左/向右翻转阵列。 |
| [`flipud`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.flipud.html#numpy.flipud)（M） | 向上/向下翻转阵列。 |
| [`reshape`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.reshape.html#numpy.reshape)（a，newshape \[，order\]） | 为数组提供新形状而不更改其数据。 |
| [`roll`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.roll.html#numpy.roll)（a，shift \[，axis\]） | 沿给定轴滚动数组元素。 |
| [`rot90`](https://docs.scipy.org/doc/numpy/reference/generated/numpy.rot90.html#numpy.rot90)（m \[，k，axes\]） | 在轴指定的平面中将数组旋转90度 |



