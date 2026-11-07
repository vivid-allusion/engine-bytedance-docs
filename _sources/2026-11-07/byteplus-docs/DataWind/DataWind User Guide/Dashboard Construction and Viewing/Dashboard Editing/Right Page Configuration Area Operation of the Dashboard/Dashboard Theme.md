---
title: "Dashboard Theme"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dashboard_Theme"
---

<span id="_1-概述"></span>
# 1. Overview

The dashboard supports configuration of dashboard themes. After selecting the corresponding dashboard theme, you can uniformly configure the color scheme, control styles, chart styles, fonts, and more for the charts on the dashboard, allowing you to quickly create visually appealing dashboards. Currently, the dashboard supports multiple official themes and custom theme functionality.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5797a5446b54bc5aa6bd609d508e6fa~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-系统官方主题配置"></span>
# 2. Configuring system official themes

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c42f3c5c6b84c1da8c1c80131a55c81~tplv-goo7wpa0wc-image.image) </span>

(1) On the dashboard editing page, click a blank area and select the dashboard theme on the left. To remove the dashboard theme, click Reset in the upper right corner.

The system official themes include Classic, Light, Dark, Tech Blue, and Elegant Purple. Different styles are suitable for different scenarios. The "Classic" theme is available only in V2.58.0 and later versions.

(2) Click a chart on the dashboard. In the chart configuration page on the right, you can select the option for component element styles to follow the dashboard theme. If selected, the chart's theme will change with the dashboard theme; if not selected, the chart will display its own style (this option appears only when a theme is set for the dashboard).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ed6b61b2fea46a595e34a65ee90e597~tplv-goo7wpa0wc-image.image) </span>

(3) If the chart on the dashboard is an existing chart added from history, the option for element styles to follow the dashboard theme is selected by default.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71381ee6ffce4e6e93754f9dc11fb7fd~tplv-goo7wpa0wc-image.image) </span>

(4) If creating a new chart, you can choose to have the chart style follow the dashboard theme when saving the chart. If selected, the chart style will automatically follow the theme settings of the dashboard it is saved to; otherwise, it will display its own style.

<span id="_3-自定义主题"></span>
# 3. Custom themes

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The custom dashboard theme feature is supported in V2.56.1 and later versions.</div>


<span id="_3-1-编辑自定义主题"></span>
## 3.1 Edit custom themes

(1) On the dashboard editing page, click the "+" icon in the upper right corner of the page configuration and select Create new theme.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62e2bf7453124290acdf88de680189df~tplv-goo7wpa0wc-image.image) </span>

(2) After clicking, the dashboard theme configuration page will appear on the right.

Supported configuration items:


* Dashboard: Basic settings, layout mode, canvas background, inner padding, appearance.

* Charts: chart titles, discrete data color schemes, continuous data color schemes, line styles, legends, table styles, and metric card styles.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7ee7534ffff4e0381c36eaf4bab8b3f~tplv-goo7wpa0wc-image.image) </span>


The specific operations are as follows:

<span id="_3-1-1-仪表盘配置项"></span>
### 3.1.1 Dashboard configuration items


* Basic settings: You can set a theme name for a newly created dashboard theme (up to 15 characters); the sharing scope of the dashboard theme can be set to personal, project, or system.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a22e733d84b248bcae9fa0aa43b08414~tplv-goo7wpa0wc-image.image) </span>


* Set the layout method: Supports tile layout and free layout. For details, see the above [Operations in the Central Canvas Area of the Dashboard](https://docs.byteplus.com/docs/DataWind/Operations_in_the_Central_Canvas_Area_of_the_Dashboard).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d10c703ad00a42e7a5b62d1543dd0135~tplv-goo7wpa0wc-image.image) </span>


* Set canvas background: Supports adjusting the background color, transparency, and more.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5288fe8a1d304c5499b4204158edf52c~tplv-goo7wpa0wc-image.image) </span>


* Set padding: Supports adjusting the top, bottom, left, and right padding of the dashboard.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e929fa8d9404455dad2bd1e96d0b78ee~tplv-goo7wpa0wc-image.image) </span>


* Set appearance: Supports adjusting the fill color, border color, border thickness, and corner radius of the dashboard.

   Support for the "adaptive control color" configuration is available in V2.58.0 and later versions. When selected, if the container background color changes, the components inside will no longer remain white. The component background color and text color will adapt to the container background color.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/875517602fcc4c138ea8bc16068d244d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-2-图表配置项"></span>
### 3.1.2 Chart configuration items


* Set chart title: Supports configuring how the chart title is displayed. You can choose to display global content, display custom content, or display nothing. Supports configuring the font size, font weight, italicization, underline, and color of the chart title.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba3ea381185647d3bb5a5a4e85b4831e~tplv-goo7wpa0wc-image.image) </span>


* Set discrete data color scheme: Supports selecting color schemes provided by the system, personal configurations, or public configurations. Custom color schemes are also supported.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2ce3669035448178bf42a0e56ea7ca0~tplv-goo7wpa0wc-image.image) </span>


* Set continuous data color scheme: Supports custom color schemes.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45d789cd745349d4800851ffe8d0a6cb~tplv-goo7wpa0wc-image.image) </span>


* Set line style: Supports selecting the line style and marker style for chart lines.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a202471416b4fb6991f41b3e181308f~tplv-goo7wpa0wc-image.image) </span>


* Set legend: Supports selecting whether to display the legend, the legend display position, legend alignment, maximum number of columns, and legend label font.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e378ca9f4a94fd2aec3f57318892532~tplv-goo7wpa0wc-image.image) </span>


* Set table style: Supports configuring the font size, font weight, italicization, underline, color, and background color of the table header text and table text.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f260bea0be74632b5a318c45b4b8cbb~tplv-goo7wpa0wc-image.image) </span>


* Configure indicator card style: Supports configuring the font and color of the indicator name and indicator value for both primary and secondary indicators.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e14fb135668f443288da77bc1b16cb55~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-应用仪表盘主题"></span>
## 3.2 Apply dashboard theme

(1) Users can view the personal category under theme categories, and in the personal category, find and apply custom themes shared with them.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ec73f3047b1417b8d28f81636d1c56d~tplv-goo7wpa0wc-image.image) </span>

(2) After applying a custom theme by clicking on it, users can also modify the layout method and configure the view mode.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/350ffa43e3bc428aa6a39f9004debfeb~tplv-goo7wpa0wc-image.image) </span>


* Configure layout method: The entire page layout supports switching between tile layout and free layout. When switching the dashboard from free layout to tile layout, the current dashboard layout style may change.

* View canvas background: The canvas background follows the dashboard theme and cannot be modified.

* Configure view mode: Supports selecting whether navigation anchors are expanded by default, whether the toolbar is displayed in view mode, whether prompt icons are displayed in view mode, whether view mode adapts to width, and whether to enable scheduled refresh.
