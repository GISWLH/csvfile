![csvfile：站点表格数据](assets/readme/banner.svg)

# csvfile

用于地理数据分析练习的站点 CSV 集合，包含中国站点表和全球站点表。仓库以轻量表格提供输入数据，可用于坐标检查、空间分布绘制和后续统计分析。

## 数据文件

| 文件 | 表头 | 说明 |
| --- | --- | --- |
| [Chinastation.csv](data/Chinastation.csv) | `Station, Lon, Lat, data` | 含站点标识、经纬度和一个数据字段 |
| [worldstation.csv](data/worldstation.csv) | `lat, lon, soil`，以及一个空列名 | 含经纬度和土壤相关字段；读取时留意末尾空列 |

表头中的 `data` 和 `soil` 没有随库提供的单位、采样时间或字段字典。使用这些数值作定量分析时，应先核对原始数据来源与字段定义；不能仅凭文件名推断其单位或代表范围。

## 读取方式

使用 Python 和 pandas，在仓库根目录读取：

```python
import pandas as pd

china = pd.read_csv("data/Chinastation.csv")
world = pd.read_csv("data/worldstation.csv")

# 忽略 CSV 末尾分隔符产生的未命名列。
world = world.loc[:, ~world.columns.str.startswith("Unnamed:")]
print(china.columns.tolist())
print(world.columns.tolist())
```

绘制位置前，先检查经纬度列的缺失值、数值类型和取值范围。两个文件的经纬度列大小写不同，合并处理时需统一字段名。

## 许可证与图形源文件

仓库包含 [MIT License](LICENSE)。横幅的可编辑源文件为 [banner.excalidraw](assets/readme/banner.excalidraw)。
