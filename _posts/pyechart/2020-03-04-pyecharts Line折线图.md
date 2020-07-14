---
layout: post
title:  pyecharts Line 折线图
date:   2020-03-04
categories: pyecharts
tags:  [pyecharts,Line]
---
* content
{:toc}
Line 折线图







## [Line：折线/面积图](https://pyecharts.org/#/zh-cn/rectangular_charts?id=line：折线面积图)

```python
class pyecharts.charts.Line(RectChart)


class Line(
    # 初始化配置项，参考 `global_options.InitOpts`
    init_opts: opts.InitOpts = opts.InitOpts()
)
```

```python
func pyecharts.charts.Line.add_yaxis

def add_yaxis(
    # 系列名称，用于 tooltip 的显示，legend 的图例筛选。
    series_name: str,

    # 系列数据
    y_axis: Sequence,

    # 是否选中图例
    is_selected: bool = True,

    # 是否连接空数据，空数据使用 `None` 填充
    is_connect_nones: bool = False,

    # 使用的 x 轴的 index，在单个图表实例中存在多个 x 轴的时候有用。
    xaxis_index: Optional[Numeric] = None,

    # 使用的 y 轴的 index，在单个图表实例中存在多个 y 轴的时候有用。
    yaxis_index: Optional[Numeric] = None,

    # 系列 label 颜色
    color: Optional[str] = None,

    # 是否显示 symbol, 如果 false 则只有在 tooltip hover 的时候显示。
    is_symbol_show: bool = True,

    # 标记的图形。
    # ECharts 提供的标记类型包括 'circle', 'rect', 'roundRect', 'triangle', 
    # 'diamond', 'pin', 'arrow', 'none'
    # 可以通过 'image://url' 设置为图片，其中 URL 为图片的链接，或者 dataURI。
    symbol: Optional[str] = None,

    # 标记的大小，可以设置成诸如 10 这样单一的数字，也可以用数组分开表示宽和高，
    # 例如 [20, 10] 表示标记宽为 20，高为 10。
    symbol_size: Union[Numeric, Sequence] = 4,

    # 数据堆叠，同个类目轴上系列配置相同的　stack　值可以堆叠放置。
    stack: Optional[str] = None,

    # 是否平滑曲线
    is_smooth: bool = False,

    # 是否显示成阶梯图
    is_step: bool = False,

    # 是否开启 hover 在拐点标志上的提示动画效果。
    is_hover_animation: bool = True,

    # 折线图所有图形的 zlevel 值。
    # zlevel用于 Canvas 分层，不同zlevel值的图形会放置在不同的 Canvas 中，Canvas 分层是一种常见的优化手段。
    # zlevel 大的 Canvas 会放在 zlevel 小的 Canvas 的上面。
    z_level: types.Numeric = 0,

    # 折线图组件的所有图形的z值。控制图形的前后顺序。z值小的图形会被z值大的图形覆盖。
    # z 相比 zlevel 优先级更低，而且不会创建新的 Canvas。
    z: types.Numeric = 0,

    # 标记点配置项，参考 `series_options.MarkPointOpts`
    markpoint_opts: Union[opts.MarkPointOpts, dict, None] = None,

    # 标记线配置项，参考 `series_options.MarkLineOpts`
    markline_opts: Union[opts.MarkLineOpts, dict, None] = None,

    # 提示框组件配置项，参考 `series_options.TooltipOpts`
    tooltip_opts: Union[opts.TooltipOpts, dict, None] = None,

    # 标签配置项，参考 `series_options.LabelOpts`
    label_opts: Union[opts.LabelOpts, dict] = opts.LabelOpts(),

    # 线样式配置项，参考 `series_options.LineStyleOpts`
    linestyle_opts: Union[opts.LineStyleOpts, dict] = opts.LineStyleOpts(),

    # 填充区域配置项，参考 `series_options.AreaStyleOpts`
    areastyle_opts: Union[opts.AreaStyleOpts, dict] = opts.AreaStyleOpts(),

    # 图元样式配置项，参考 `series_options.ItemStyleOpts`
    itemstyle_opts: Union[opts.ItemStyleOpts, dict, None] = None,
)
```

# [Line - Line_base](http://gallery.pyecharts.org/#/Line/line_base?id=line-line_base)

```python
import pyecharts.options as opts
from pyecharts.charts import Line
from pyecharts.faker import Faker

c = (
    Line()
    .add_xaxis(Faker.choose())
    .add_yaxis("商家A", Faker.values())
    .add_yaxis("商家B", Faker.values())
    .set_global_opts(title_opts=opts.TitleOpts(title="Line-基本示例"))
    .render("line_base.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527093454.png"/></center>




# [Line - Basic_line_chart](http://gallery.pyecharts.org/#/Line/basic_line_chart?id=line-basic_line_chart)

```python
import pyecharts.options as opts
from pyecharts.charts import Line
from pyecharts.globals import CurrentConfig, NotebookType
CurrentConfig.NOTEBOOK_TYPE = NotebookType.JUPYTER_LAB


x_data = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
y_data = [820, 932, 901, 934, 1290, 1330, 1320]

line = (
    Line()
    .add_xaxis(xaxis_data=x_data)
    .add_yaxis(series_name="",
               y_axis=y_data,
               symbol='emptyCircle',
               is_symbol_show=True,
               label_opts=opts.LabelOpts(is_show=False))

    .set_global_opts(
        tooltip_opts=opts.TooltipOpts(is_show=False),
        xaxis_opts=opts.AxisOpts(type_='category'),
        yaxis_opts=opts.AxisOpts(type_='value',
                                 
                                 # 是否显示刻度线
                                 axistick_opts=opts.AxisTickOpts(is_show=True),
                                 
                                 # 是否显示网格线
                                 splitline_opts=opts.SplitLineOpts(is_show=True))
    )

)
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527093117.png"/></center>




# [Line - Line_smooth](http://gallery.pyecharts.org/#/Line/line_smooth?id=line-line_smooth)

```python
import pyecharts.options as opts
from pyecharts.charts import Line
from pyecharts.faker import Faker

c = (
    Line()
    .add_xaxis(Faker.choose())
    .add_yaxis("商家A", Faker.values(), is_smooth=True)
    .add_yaxis("商家B", Faker.values(), is_smooth=True)
    .set_global_opts(title_opts=opts.TitleOpts(title="Line-smooth"))
    .render("line_smooth.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527093620.png"/></center>


# [Line - Line_markpoint](http://gallery.pyecharts.org/#/Line/line_markpoint?id=line-line_markpoint)

```python
import pyecharts.options as opts
from pyecharts.charts import Line
from pyecharts.faker import Faker

c = (
    Line()
    .add_xaxis(Faker.choose())
    .add_yaxis(
        "商家A",
        Faker.values(),
        markpoint_opts=opts.MarkPointOpts(data=[opts.MarkPointItem(type_="min")]),
    )
    .add_yaxis(
        "商家B",
        Faker.values(),
        markpoint_opts=opts.MarkPointOpts(data=[opts.MarkPointItem(type_="max")]),
    )
    .set_global_opts(title_opts=opts.TitleOpts(title="Line-MarkPoint"))
    .render("line_markpoint.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527094455.png"/></center>


# [Line - Line_markpoint_custom](http://gallery.pyecharts.org/#/Line/line_markpoint_custom?id=line-line_markpoint_custom)

自定义标记点，首先给出对应轴的数据，例如只有一个数据可以用 x, y 标记。这样自定义标记的时候 就可以用索引的方式标记对应的坐标

```python
import pyecharts.options as opts
from pyecharts.charts import Line
from pyecharts.faker import Faker

# 给出对应轴的数据
x, y = Faker.choose(), Faker.values()
c = (
    Line()
    .add_xaxis(x)
    .add_yaxis(
        "商家A",
        y,
        markpoint_opts=opts.MarkPointOpts(
            data=[opts.MarkPointItem(name="自定义标记点", coord=[x[2], y[2]], value=y[2])]
        ),
    )
    .set_global_opts(title_opts=opts.TitleOpts(title="Line-MarkPoint（自定义）"))
    .render("line_markpoint_custom.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527101113.png"/></center>






# [Line - Line_markline](http://gallery.pyecharts.org/#/Line/line_markline?id=line-line_markline)

```python
import pyecharts.options as opts
from pyecharts.charts import Line
from pyecharts.faker import Faker

c = (
    Line()
    .add_xaxis(Faker.choose())
    .add_yaxis(
        "商家A",
        Faker.values(),
        markline_opts=opts.MarkLineOpts(data=[opts.MarkLineItem(type_="average")]),
    )
    .add_yaxis(
        "商家B",
        Faker.values(),
        markline_opts=opts.MarkLineOpts(data=[opts.MarkLineItem(type_="average")]),
    )
    .set_global_opts(title_opts=opts.TitleOpts(title="Line-MarkLine"))
    .render("line_markline.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527095913.png"/></center>


# [Line - Line_style_and_item_style](http://gallery.pyecharts.org/#/Line/line_style_and_item_style?id=line-line_style_and_item_style)

```python
import pyecharts.options as opts
from pyecharts.charts import Line

(
    Line(init_opts=opts.InitOpts(width="1280px", height="720px"))
    .add_xaxis(xaxis_data=["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"])
    .add_yaxis(
        series_name="",
        y_axis=[120, 200, 150, 80, 70, 110, 130],
        symbol="triangle",	# 标记类型
        symbol_size=20,		# 标记大小
        
        # 线的参数设置
        linestyle_opts=opts.LineStyleOpts(color="green", width=4, type_="dashed"),
        label_opts=opts.LabelOpts(is_show=False),
        # 标记的颜色, 边框, 边框颜色等设置
        itemstyle_opts=opts.ItemStyleOpts(
            border_width=3, border_color="yellow", color="blue"
        ),
    )
    .set_global_opts(
        xaxis_opts=opts.AxisOpts(type_="category"),
        yaxis_opts=opts.AxisOpts(
            type_="value",
            axistick_opts=opts.AxisTickOpts(is_show=True),
            splitline_opts=opts.SplitLineOpts(is_show=True),
        ),
        tooltip_opts=opts.TooltipOpts(is_show=False),
    )
    .render("line_style_and_item_style.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527102448.png"/></center>
# [Line - Stacked_line_chart](http://gallery.pyecharts.org/#/Line/stacked_line_chart?id=line-stacked_line_chart)

```python
import pyecharts.options as opts
from pyecharts.charts import Line

"""
Gallery 使用 pyecharts 1.1.0
参考地址: https://echarts.baidu.com/examples/editor.html?c=line-stack

目前无法实现的功能:

暂无
"""


x_data = ["周一", "周二", "周三", "周四", "周五", "周六", "周日"]
y_data = [820, 932, 901, 934, 1290, 1330, 1320]


(
    Line()
    .add_xaxis(xaxis_data=x_data)
    .add_yaxis(
        series_name="邮件营销",
        stack="总量",
        y_axis=[120, 132, 101, 134, 90, 230, 210],
        label_opts=opts.LabelOpts(is_show=False),
    )
    .add_yaxis(
        series_name="联盟广告",
        stack="总量",
        y_axis=[220, 182, 191, 234, 290, 330, 310],
        label_opts=opts.LabelOpts(is_show=False),
    )
    .add_yaxis(
        series_name="视频广告",
        stack="总量",
        y_axis=[150, 232, 201, 154, 190, 330, 410],
        label_opts=opts.LabelOpts(is_show=False),
    )
    .add_yaxis(
        series_name="直接访问",
        stack="总量",
        y_axis=[320, 332, 301, 334, 390, 330, 320],
        label_opts=opts.LabelOpts(is_show=False),
    )
    .add_yaxis(
        series_name="搜索引擎",
        stack="总量",
        y_axis=[820, 932, 901, 934, 1290, 1330, 1320],
        label_opts=opts.LabelOpts(is_show=False),
    )
    .set_global_opts(
        title_opts=opts.TitleOpts(title="折线图堆叠"),
        
        tooltip_opts=opts.TooltipOpts(trigger="axis"),
        
        yaxis_opts=opts.AxisOpts(
            type_="value",
            axistick_opts=opts.AxisTickOpts(is_show=True),
            splitline_opts=opts.SplitLineOpts(is_show=True),
        ),
        xaxis_opts=opts.AxisOpts(type_="category", boundary_gap=False),
    )
    .render("stacked_line_chart.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527103030.png"/></center>


# [Line - Basic_area_chart](http://gallery.pyecharts.org/#/Line/basic_area_chart?id=line-basic_area_chart)

```python
import pyecharts.options as opts
from pyecharts.charts import Line

x_data = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
y_data = [820, 932, 901, 934, 1290, 1330, 1320]


(
    Line()
    .add_xaxis(xaxis_data=x_data)
    .add_yaxis(
        series_name="",
        y_axis=y_data,
        symbol="emptyCircle",
        is_symbol_show=True,
        label_opts=opts.LabelOpts(is_show=False),
        areastyle_opts=opts.AreaStyleOpts(opacity=1, color="#C67570"),
    )
    .set_global_opts(
        tooltip_opts=opts.TooltipOpts(is_show=False),
        yaxis_opts=opts.AxisOpts(
            type_="value",
            axistick_opts=opts.AxisTickOpts(is_show=True),
            splitline_opts=opts.SplitLineOpts(is_show=True),
        ),
        xaxis_opts=opts.AxisOpts(type_="category", boundary_gap=False),
    )
    # 设置 boundary_gap 的时候一定要放在最后一个配置项里, 不然会被覆盖
    .render("basic_area_chart.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527104952.png"/></center>


# [Line - Line_area_style](http://gallery.pyecharts.org/#/Line/line_area_style?id=line-line_area_style)

```python
import pyecharts.options as opts
from pyecharts.charts import Line
from pyecharts.faker import Faker

c = (
    Line()
    .add_xaxis(Faker.choose())
    .add_yaxis("商家A", Faker.values(), areastyle_opts=opts.AreaStyleOpts(opacity=0.5))
    .add_yaxis("商家B", Faker.values(), areastyle_opts=opts.AreaStyleOpts(opacity=0.5))
    .set_global_opts(title_opts=opts.TitleOpts(title="Line-面积图"))
    .render("line_area_style.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527114123.png"/></center>


# [Line - Line_areastyle_boundary_gap](http://gallery.pyecharts.org/#/Line/line_areastyle_boundary_gap?id=line-line_areastyle_boundary_gap)

```python
import pyecharts.options as opts
from pyecharts.charts import Line
from pyecharts.faker import Faker


c = (
    Line()
    .add_xaxis(Faker.choose())
    .add_yaxis("商家A", Faker.values(), is_smooth=True)
    .add_yaxis("商家B", Faker.values(), is_smooth=True)
    .set_series_opts(
        areastyle_opts=opts.AreaStyleOpts(opacity=0.5),
        label_opts=opts.LabelOpts(is_show=False),
    )
    .set_global_opts(
        title_opts=opts.TitleOpts(title="Line-面积图（紧贴 Y 轴）"),
        xaxis_opts=opts.AxisOpts(
            
            # 类目轴中在 boundaryGap 为 true 的时候有效，可以保证刻度线和标签对齐。
   			#is_align_with_label: bool = False,            
            axistick_opts=opts.AxisTickOpts(is_align_with_label=True),
            is_scale=False,
            boundary_gap=False,
        ),
    )
    .render("line_areastyle_boundary_gap.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527111601.png"/></center>






# [Line - Stacked_area_chart](http://gallery.pyecharts.org/#/Line/stacked_area_chart?id=line-stacked_area_chart)

```python
import pyecharts.options as opts
from pyecharts.charts import Line


x_data = ["周一", "周二", "周三", "周四", "周五", "周六", "周日"]
y_data = [820, 932, 901, 934, 1290, 1330, 1320]


(
    Line()
    .add_xaxis(xaxis_data=x_data)
    .add_yaxis(
        series_name="邮件营销",
        stack="总量",
        y_axis=[120, 132, 101, 134, 90, 230, 210],
        areastyle_opts=opts.AreaStyleOpts(opacity=0.5),
        label_opts=opts.LabelOpts(is_show=False),
    )
    .add_yaxis(
        series_name="联盟广告",
        stack="总量",
        y_axis=[220, 182, 191, 234, 290, 330, 310],
        areastyle_opts=opts.AreaStyleOpts(opacity=0.5),
        label_opts=opts.LabelOpts(is_show=False),
    )
    .add_yaxis(
        series_name="视频广告",
        stack="总量",
        y_axis=[150, 232, 201, 154, 190, 330, 410],
        areastyle_opts=opts.AreaStyleOpts(opacity=0.5),
        label_opts=opts.LabelOpts(is_show=False),
    )
    .add_yaxis(
        series_name="直接访问",
        stack="总量",
        y_axis=[320, 332, 301, 334, 390, 330, 320],
        areastyle_opts=opts.AreaStyleOpts(opacity=0.5),
        label_opts=opts.LabelOpts(is_show=False),
    )
    .add_yaxis(
        series_name="搜索引擎",
        stack="总量",
        y_axis=[820, 932, 901, 934, 1290, 1330, 1320],
        areastyle_opts=opts.AreaStyleOpts(opacity=0.5),
        label_opts=opts.LabelOpts(is_show=True, position="top"),
    )
    .set_global_opts(
        title_opts=opts.TitleOpts(title="堆叠区域图"),
        tooltip_opts=opts.TooltipOpts(trigger="axis", axis_pointer_type="cross"),
        yaxis_opts=opts.AxisOpts(
            type_="value",
            axistick_opts=opts.AxisTickOpts(is_show=True),
            splitline_opts=opts.SplitLineOpts(is_show=True),
        ),
        xaxis_opts=opts.AxisOpts(type_="category", boundary_gap=False),
    )
    .render("stacked_area_chart.html")
)

```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527103711.png"/></center>
# [Line - Distribution_of_electricity](http://gallery.pyecharts.org/#/Line/distribution_of_electricity?id=line-distribution_of_electricity)

```python
x_data = ["00:00",    "01:15",    "02:30",    "03:45",    "05:00",    "06:15",    "07:30",    "08:45",    "10:00",    "11:15",
          "12:30",    "13:45",    "15:00",    "16:15",    "17:30",    "18:45",    "20:00",    "21:15",    "22:30",    "23:45", ]
y_data = [300,    280,    250,    260,    270,    300,    550,    500,    400,    390,    380,    390,    400,    500,
          600,    750,    800,    700,    600,    400, ]

(
    Line(init_opts=opts.InitOpts(width="1600px", height="800px"))
    .add_xaxis(xaxis_data=x_data)
    .add_yaxis(
        series_name="用电量",
        y_axis=y_data,
        is_smooth=True,
        label_opts=opts.LabelOpts(is_show=False),
        linestyle_opts=opts.LineStyleOpts(width=2),
    )
    .set_global_opts(
        title_opts=opts.TitleOpts(title="一天用电量分布", subtitle="纯属虚构"),
        tooltip_opts=opts.TooltipOpts(trigger="axis", axis_pointer_type="cross"),
        xaxis_opts=opts.AxisOpts(boundary_gap=False),
        yaxis_opts=opts.AxisOpts(
            axislabel_opts=opts.LabelOpts(formatter="{value} W"),
            splitline_opts=opts.SplitLineOpts(is_show=True),
        ),
        visualmap_opts=opts.VisualMapOpts(
            # 是否为分段型
            is_piecewise=True,
            # 组件映射维度
            dimension=0,
            # 自定义的每一段的范围，以及每一段的文字，以及每一段的特别的样式
            pieces=[
                {"lte": 6, "color": "green"},
                {"gt": 6, "lte": 8, "color": "red"},
                {"gt": 8, "lte": 14, "color": "green"},
                {"gt": 14, "lte": 17, "color": "red"},
                {"gt": 17, "color": "green"},
            ],
        ),
    )
    .set_series_opts(
        markarea_opts=opts.MarkAreaOpts(
            data=[
                opts.MarkAreaItem(name="早高峰", x=("07:30", "10:00")),
                opts.MarkAreaItem(name="晚高峰", x=("17:30", "21:15")),
            ]
        )
    )
    .render("distribution_of_electricity.html")
)
```

<center><img src="https://raw.githubusercontent.com/HG1227/image/master/img_tuchuang/20200527113539.png"/></center>