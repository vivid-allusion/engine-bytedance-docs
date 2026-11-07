---
title: "Color processing functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Color-processing-functions"
---

This topic describes the syntax of color processing functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="2bcdff93"></span>
## List of functions


|Function |Function Syntax |Description |
|---|---|---|
|BAR |BAR(x, width) |Returns a part of an ANSI bar chart whose start color is red and end color is green. The width parameter specifies the width of the ANSI bar chart. The x parameter specifies the part to be returned. |
||BAR(x, width, low_color, high_color) |Returns a part of an ANSI bar chart with a specified start color and end color. The width parameter specifies the width of the ANSI bar chart. The x parameter specifies the part to be returned. |
|COLOR |COLOR(string) |Converts a color string to a color type. |
||COLOR(x, low, high, low_color, high_color) |Returns a hybrid color based on the portions of high_color and low_color. The portions are determined by the proportion of x between high and low. |
||COLOR(y, low_color, high_color) |Returns a hybrid color based on the portions of high_color and low_color. The portions are determined by y. |
|RENDER |RENDER(boolean expression) |Returns results using default color rendering. If the Boolean expression evaluates to true, the function returns a green tick. Otherwise, the function returns a red cross. |
||RENDER(x, color) |Returns results using custom color rendering. |
|RGB |RGB(red, green, blue) |Returns a color value based on a specified RGB value. |


<span id="df185457"></span>
## BAR

The BAR function returns an ANSI bar chart.

<span id="0cdfe601"></span>
### Function **syntax**


* Syntax format

   * Returns a part of an ANSI bar chart whose start color is red and end color is green. The width parameter specifies the width of the ANSI bar chart. The x parameter specifies the part to be returned.

      ```SQL
      BAR(x, width)
      ```
      

   * Returns a part of an ANSI bar chart with a specified start color and end color. The width parameter specifies the width of the ANSI bar chart. The x parameter specifies the part to be returned.

      ```SQL
      BAR(x, width, low_color, high_color)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |The proportion of the part returned by the function to the ANSI bar chart. The value is of the Double type. Valid values: [0,1]. |
   |width |The width of the ANSI bar chart. |
   |low_color |The RGB value of the start color. |
   |high_color |The RGB value of the end color. |
   

* Return value description

   The return value is of the Varchar type.


<span id="1f05e335"></span>
### Example


* Scenario

   Get an ANSI bar chart at the proportion of 50%.

* Query and analysis statement

   ```SQL
   * | SELECT BAR(0.5, 100)
   ```
   

* Query and analysis results in the console

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72bfb7a92a564821a4269fad7f8b5bda~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis results on the terminal

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c90cfbcfe8e4ec6855e3c284eb4718c~tplv-goo7wpa0wc-image.image) </span>


<span id="abb24621"></span>
## COLOR

The COLOR function returns the color of a value.

<span id="c86b8623"></span>
### Function **syntax**


* Syntax format

   * Converts a color string to a color type.

      ```SQL
      COLOR(string)
      ```
      

   * Returns a hybrid color based on the portions of high_color and low_color. The portions are determined by the proportion of x between high and low.

      ```SQL
      COLOR(x, low, high, low_color, high_color)
      ```
      

   * Returns a hybrid color based on the portions of high_color and low_color. The portions are determined by y.

      ```SQL
      COLOR(y, low_color, high_color)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |The value is of the Double type. |
   |y |The value is of the Double type. Valid values: [0,1]. |
   |low |The minimum value. The value is of the Double type. |
   |high |The maximum value. The value is of the Double type. |
   |low_color |The RGB value of the start color. |
   |high_color |The RGB value of the end color. |
   |string |The string. Valid values: black, red, green, yellow, blue, magenta, cyan, and white. The value can also be an RGB value in the Cascading Style Sheet (CSS) format, such as #000. |
   

* Return value description

   The return value is of the Color type.


<span id="7bbfc93e"></span>
### Example


* Example 1

   * Scenario

      Convert a color string to a color type.

   * Query and analysis statement

      ```SQL
      * | SELECT COLOR('#000')
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c13b9bac1df4dbcaaecc98f9aef2b6b~tplv-goo7wpa0wc-image.image) </span>

* Example 2

   * Scenario

      Get a color based on a specified proportion.

   * Query and analysis statement

      ```SQL
      *|SELECT COLOR(5, 0, 10, RGB(255,0,0), RGB(0,255,0))
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25210743c94e4c84943be6edef3f7e12~tplv-goo7wpa0wc-image.image) </span>


<span id="86fff8d0"></span>
## RENDER

The RENDERING function returns results using color rendering.

<span id="e5a36ead"></span>
### Function **syntax**


* Syntax format

   * Returns results using default color rendering. If the Boolean expression evaluates to true, the function returns a green tick. Otherwise, the function returns a red cross.

      ```SQL
      RENDER(boolean expression)
      ```
      

   * Returns results using custom color rendering.

      ```SQL
      RENDER(x, color)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |boolean expression |The value is of the Boolean type. |
   |x |The X coordinate. The value is of the Integer type. |
   |color |The color. The value is of the Color type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="c5ed820d"></span>
### Example


* Example 1

   * Scenario

      Use the RENDER function to verify whether the value of `count(*)` is less than 1,000. If so, a green tick is returned.

   * Query and analysis statement

      ```SQL
      * | SELECT RENDER(count(*)<1000)
      ```
      

   * Query and analysis results in the console

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad1fb14475704acb8bd2673fb0c2f895~tplv-goo7wpa0wc-image.image) </span>

   * Query and analysis results on the terminal

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5205d2fb045645d3a4bd5dca3286f886~tplv-goo7wpa0wc-image.image) </span>


<span id="f6e215dc"></span>
## RGB

The RGB function returns a color value based on a specified RGB value.

<span id="afba1f72"></span>
### Function **syntax**


* Syntax format

   ```SQL
   RGB(red, green, blue)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |red |The portion of red. Valid values: [0,255]. The value is of the Integer type. |
   |green |The portion of green. Valid values: [0,255]. The value is of the Integer type. |
   |blue |The portion of blue. Valid values: [0,255]. The value is of the Integer type. |
   

* Return value description

   The return value is of the Color type.


<span id="bddff200"></span>
### Example


* Scenario

   Get a color based on an RGB value.

* Query and analysis statement

   ```SQL
   *|SELECT RGB(255,0,0)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f84deb6a8d543df8091ca19f54a86b2~tplv-goo7wpa0wc-image.image) </span>
