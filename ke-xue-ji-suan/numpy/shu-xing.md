### 

### 属性

数据类型由以下`dtype`属性描述：

| `dtype.type` | 用于实例化此数据类型的标量的类型对象。 |
| :--- | :--- |
| `dtype.kind` | 标识一般数据类型的字符代码（'biufcmMOSUV'之一）。 |
| `dtype.char` | 21种不同内置类型中每种类型的唯一字符代码。 |
| `dtype.num` | 21种不同内置类型中每种类型的唯一编号。 |
| `dtype.str` | 此数据类型对象的array-protocol typestring。 |

数据大小依次描述如下：

| `dtype.name` | 此数据类型的位宽名称。 |
| :--- | :--- |
| `dtype.itemsize` | 此数据类型对象的元素大小。 |

此数据的字节顺序：

| `dtype.byteorder` | 一个字符，指示此数据类型对象的字节顺序。 |
| :--- | :--- |


有关结构化数据类型中子数据类型的信息：

| `dtype.fields` | 为此数据类型定义的命名字段字典，或`None`。 |
| :--- | :--- |
| `dtype.names` | 有序的字段名称列表，或者`None`没有字段。 |

对于描述子数组的数据类型：

| `dtype.subdtype` | 如果这描述了一个子数组，则为元组，否则为None。`(item_dtype,shape)dtype` |
| :--- | :--- |
| `dtype.shape` | 如果此数据类型描述子数组，则子数组的形状元组，`()`否则。 |

提供附加信息的属性：

| `dtype.hasobject` | 布尔值，指示此dtype是否包含任何字段或子数据类型中的任何引用计数对象。 |
| :--- | :--- |
| `dtype.flags` | 描述如何解释此数据类型的位标志。 |
| `dtype.isbuiltin` | 整数表示此dtype与内置dtypes的关系。 |
| `dtype.isnative` | 布尔值，指示此dtype的字节顺序是否为平台本机。 |
| `dtype.descr` | PEP3118接口描述了数据类型。 |
| `dtype.alignment` | 根据编译器，此数据类型所需的对齐（字节）。 |



