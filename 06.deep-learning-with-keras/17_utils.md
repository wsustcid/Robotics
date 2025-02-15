<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/utils/generic_utils.py#L21)</span>
### CustomObjectScope

```python
keras.utils.CustomObjectScope()
```

提供更改为 `_GLOBAL_CUSTOM_OBJECTS` 无法转义的范围。

`with` 语句中的代码将能够通过名称访问自定义对象。
对全局自定义对象的更改会在封闭的 `with` 语句中持续存在。
在`with`语句结束时，
全局自定义对象将恢复到 `with` 语句开始时的状态。

__例子__


考虑自定义对象 `MyObject` (例如一个类)：

```python
with CustomObjectScope({'MyObject':MyObject}):
    layer = Dense(..., kernel_regularizer='MyObject')
    # 保存，加载等操作将按这个名称来识别自定义对象
```

----

<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/utils/io_utils.py#L25)</span>
### HDF5Matrix

```python
keras.utils.HDF5Matrix(datapath, dataset, start=0, end=None, normalizer=None)
```

使用 HDF5 数据集表示，而不是 Numpy 数组。

__例子__


```python
x_data = HDF5Matrix('input/file.hdf5', 'data')
model.predict(x_data)
```

提供 `start` 和 `end` 将允许使用数据集的一个切片。

你还可以给出标准化函数（或 lambda）（可选）。
这将在检索到的每一个数据切片上调用它。

__参数__

- __datapath__: 字符串，HDF5 文件路径。
- __dataset__: 字符串，datapath指定的文件中的 HDF5 数据集名称。
- __start__: 整数，所需的指定数据集的切片的开始位置。
- __end__: 整数，所需的指定数据集的切片的结束位置。
- __normalizer__: 在检索数据时调用的函数。

__返回__

一个类似于数组的 HDF5 数据集。

### to_categorical


```python
keras.utils.to_categorical(y, num_classes=None, dtype='float32')
```


将类向量（整数）转换为二进制类矩阵。

例如，用于 categorical_crossentropy。

__参数__

- __y__: 需要转换成矩阵的类矢量
(从 0 到 num_classes 的整数)。
- __num_classes__: 总类别数。
- __dtype__: 字符串，输入所期望的数据类型 (`float32`, `float64`, `int32`...)

__例子__

```python
# 考虑一组 3 个类 {0,1,2} 中的 5 个标签数组：
> labels
array([0, 2, 1, 2, 0])
# `to_categorical` 将其转换为具有尽可能多表示类别数的列的矩阵。
# 行数保持不变。
> to_categorical(labels)
array([[ 1.,  0.,  0.],
       [ 0.,  0.,  1.],
       [ 0.,  1.,  0.],
       [ 0.,  0.,  1.],
       [ 1.,  0.,  0.]], dtype=float32)
```

__返回__

输入的二进制矩阵表示。

----

### normalize


```python
keras.utils.normalize(x, axis=-1, order=2)
```


标准化一个 Numpy 数组。

__参数__

- __x__: 需要标准化的 Numpy 数组。
- __axis__: 需要标准化的轴。
- __order__: 标准化顺序(例如，2 表示 L2 规范化)。

__Returns__

数组的标准化副本。

----

### get_file


```python
keras.utils.get_file(fname, origin, untar=False, md5_hash=None, file_hash=None, cache_subdir='datasets', hash_algorithm='auto', extract=False, archive_format='auto', cache_dir=None)
```


从一个 URL 下载文件，如果它不存在缓存中。

默认情况下，URL `origin`处的文件
被下载到缓存目录 `〜/.keras` 中，
放在缓存子目录 `datasets`中，并命名为 `fname`。
文件 `example.txt` 的最终位置为 `~/.keras/datasets/example.txt`。

tar, tar.gz, tar.bz, 以及 zip 格式的文件也可以被解压。
传递一个哈希值将在下载后校验文件。
命令行程序 `shasum` 和 `sha256sum` 可以计算哈希。

__参数__

- __fname__: 文件名。如果指定了绝对路径 `/path/to/file.txt`，
那么文件将会保存到那个路径。
- __origin__: 文件的原始 URL。
- __untar__: 由于使用 'extract' 而已被弃用。
布尔值，是否需要解压文件。
- __md5_hash__: 由于使用 'file_hash' 而已被弃用。
用于校验的 md5 哈希值。
- __file_hash__: 下载后的文件的期望哈希字符串。
支持 sha256 和 md5 两个哈希算法。
- __cache_subdir__: 在 Keras 缓存目录下的保存文件的子目录。
如果指定了绝对路径 `/path/to/folder`，则文件将被保存在该位置。
- __hash_algorithm__: 选择哈希算法来校验文件。
可选的有 'md5', 'sha256', 以及 'auto'。
默认的 'auto' 将自动检测所使用的哈希算法。
- __extract__: True 的话会尝试将解压缩存档文件，如tar或zip。
- __archive_format__: 尝试提取文件的存档格式。
可选的有 'auto', 'tar', 'zip', 以及 None。
'tar' 包含 tar, tar.gz, 和 tar.bz 文件。
默认 'auto' 为 ['tar', 'zip']。
None 或 空列表将返回未找到任何匹配。
ke xu az z'auto', 'tar', 'zip', and None.
- __cache_dir__: 存储缓存文件的位置，为 None 时默认为
[Keras 目录](/faq/#where-is-the-keras-configuration-filed-stored).

__返回__

下载的文件的路径。

----

### print_summary


```python
keras.utils.print_summary(model, line_length=None, positions=None, print_fn=None)
```


打印模型概况。

__参数__

- __model__: Keras 模型实例。
- __line_length__: 打印的每行的总长度
(例如，设置此项以使其显示适应不同的终端窗口大小)。
- __positions__: 每行中日志元素的相对或绝对位置。
如果未提供，默认为 `[.33, .55, .67, 1.]`。
- __print_fn__: 需要使用的打印函数。
它将在每一行概述时调用。
您可以将其设置为自定义函数以捕获字符串概述。
默认为 `print` (打印到标准输出)。

----

### plot_model


```python
keras.utils.plot_model(model, to_file='model.png', show_shapes=False, show_layer_names=True, rankdir='TB', expand_nested=False, dpi=96)
```


将 Keras 模型转换为 dot 格式并保存到文件中。

__参数__

- __model__: 一个 Keras 模型实例。
- __to_file__: 绘制图像的文件名。
- __show_shapes__: 是否显示尺寸信息。
- __show_layer_names__: 是否显示层的名称。
- __rankdir__: 传递给 PyDot 的 `rankdir` 参数，
一个指定绘图格式的字符串：
'TB' 创建一个垂直绘图；
'LR' 创建一个水平绘图。
- __expand_nested__: 是否扩展嵌套模型为聚类。 
- __dpi__: 点 DPI。

----

