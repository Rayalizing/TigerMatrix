# TigerMatrix

虎码的【九键无重码】方案，是六码定长形码方案，通过增加两个码长，在九宫格上实现和虎码原生方案（Tiger/Tigress）**相同**的重码率（也就是几乎无重）。

本方案基于 [Rime](https://github.com/rime) 引擎和[虎码](https://tiger-code.com/)输入方案，感谢大佬们的优秀开源。

九键无重的巧妙思路，参考自知乎答主<同志请烧点水>的文章[九宫格双拼的无重码排布](https://zhuanlan.zhihu.com/p/107201990)。

## 该方案的优势：

没有多余的记忆成本和学习成本。

* 只要你会虎码，则该方案的记忆成本为零——因为其码表(除去增加的两个辅码之外)和虎码原生方案完全相同；
* 只要你知道一点坐标系概念，则辅码的学习成本为零。

## 适用范围：

适用于电脑小键盘（数字键盘）、手机九键键盘（最好配合自定义布局的键盘使用）。

## 自用手机键盘示例：

![手机键盘](https://github.com/Rayalizing/TigerMatrix/blob/main/hamster_keyboard_for_TM.jpeg)

## 食用方法：

1. 安装 Rime 输入法（鼠须管、小狼毫）；
2. 按照虎码官方教程部署好虎码方案；
3. 将本方案 Rime 目录下的内容放入用户文件夹根目录；
4. 重新部署 Rime；
5. 在输入法中，选择本方案，即可使用。
6. 示例中的手机键盘适配 ios 端的【仓输入法】，若使用该布局，可把文件 `hamster_keyboard_for_TM.yaml` 放入 `iPhone/Hamster/` 目录，并在输入法中`键盘布局`右上角加号中导入该文件。

## 教程：

学习路线：

1. 了解如何用九宫格打字
2. 学会虎码 (官网有详细教程)
3. 学会如何打出辅码
4. 如果想使用我定制的键盘布局，需要了解各个键位。

### 如何打出辅码

九宫格的优点在于按键大，防误触；可实现单手打字；键位规整，可实现盲打。但是，要将原本 26 键的虎码方案转移到只有 9 键的九宫格上，意味着同一次击键映射了更多的重码字。为了避免重码，需要增加 1 到 2 个码长，以精确选出要打的字母。这就是辅码的作用。

本方案使用[文章](https://zhuanlan.zhihu.com/p/107201990)的原理，为每两个码增加一个`行列码`。对于原本的虎码来说，每打两个原码，新增一个`行列码`用于字母选择。

九宫格按键布局：

| 1 qw  | 2 abc | 3 def |
| ------- | ------- | ------- |
| 4 ghi | 5 jkl | 6 mno |
| 7 prs | 8 tuv | 9 xyz |

公式：编码 = 2个原码 + 行列码（+ 2个原码 + 行列码）

九宫格上任意一个数字键都包含3个以内的字母，因此用1、2、3即可选出每个字母的位置。但是每敲一个键都要打一次1/2/3，码长会让人不堪重负。但当我们从视角转到二维，就简单了：

行列码也是九宫格上的任意一个数字键。这个**键的位置**包含了行和列两个坐标信息，两个坐标信息就可以一次选出两个字母的位置。比如数字 4 在九宫格的第二行第一列，它的坐标信息依次为 `2` ，`1`。

* 举例：

  要打出汉字`九`，`九`的虎码是 `kj`，在九宫格中应依次打出`55`。而`k`是`5`键的**第二个**字母，`j`是`5`键的**第一个**字母，所以在`55`之后加一个位置为**第二行第一列**的行列码，这个键是`4`，所以`九`的九宫格虎码是`554`。

  同理，`宫`字的虎码是`wddk`,前两个码`wd`在九宫格中应依次打出`13`。`w`是`1`键的**第二个**字母，`d`是`3`键的**第一个**字母，所以在`13`之后加一个位置为**第二行第一列**的行列码，这个键是`4`，所以打出`134`。接着要打`dk`，在九宫格中应依次打出`35`，`d`是`3`键的**第一个**字母，`k`是`5`键的**第二个**字母，所以`35`之后加一个位置为**第一行第二列**的行列码，这个键是`2`，所以`宫`的九宫格虎码是`134352`。

综上，每打两个码后加一个行列码，即可将原方案在九宫格上打出和26键一样的效果。

那如果码长为单数怎么办？本方案采用三个特定符号（斜杠`/`、星号`*`、反引号`` ` ``）来选择落单的这个码（这一项是方案自带，如果你追求纯粹的九宫格打字，你可以修改相关代码将这三个符号也改为九宫格上的数字（比如1、2、3）。**但这样会增加重码**）。

`/`、`*`、`` ` ``分别对应数字键上的第 1、第 2、第 3 位置的字母

* 举例：

  `的`字的虎码是`u`，在九宫格中应打出`8`，`u`是`8`的第二个字母，所以在`8`之后打出`*`键，所以`的`的最后编码是`8*`。

  `记`字的虎码是`svj`，在九宫格中先打出`sv`对应的`78`，`s`是`7`键的**第三个**字母，`v`是`8`键的**第三个**字母，所以在`78`之后加一个位置为**第三行第三列**的`9`键；接着打出`j`对应的`5`键，`j`是`5`键的**第一个**字母，所以继续打出`/`键。因此`记`字的最终编码为`7895/`。

总结：

* 对于原本码长为2码、4码的字词来说，辅码存在于第三位和第六位（第三位用来选原本前两位的码，第六位用来选原本后两位的码）。这样，码长变为了3码、6码。
* 对于原本码长为单数（1和3）的字词来说，本方案使用三个特定符号来作辅码。这样，码长变为了2码、5码。

此外，本方案依旧支持分号`;`二选上屏、单引号`'`三选上屏，进一步避免选码。在不含 emoji 的情况下基本实现了“不从候选窗口选码”的极致效果。

综上所述，本方案能在不改变原方案码表的情况下，将原方案在九宫格上打出和26键一样的效果。上述效果由`xxx.schema.yaml`文件中相关的拼写运算部分实现。因为行列码编码的是“位置信息”，所以该部分可直接复制粘贴到其他方案（比如拼音方案）中，实现全键到九键的丝滑转换。

### 支持电脑数字键打字

部署本方案后，可以实现用数字小键盘打字，注意键位已经将 1 到 9 映射成从上到下的排列（以同步手机九键的输入习惯）

键位图如下：

![电脑数字键盘](https://github.com/Rayalizing/TigerMatrix/blob/main/numpad.png)

### 定制版手机键盘布局

这个布局：

* 为适配九键虎码和 Markdown 文本编辑而定制（布局中容易打出的符号都是 Markdown 语法的常用符号）。
* 出于兼容性考虑，选择`/`、`*`、`` ` ``、`;`、`'`作为主要符号：

  * `/`还支持输入lua命令和 emoji 表情（虎码官方自带）
  * 反引号可以拼音反查（虎码官方自带）；
  * 星号是 Markdown 编辑最常用的符号；
  * 分号`;`除二选上屏外还支持快符（详见`xxx.extended.dict.yaml`）中的`标点符号 快符`区；
  * 单引号`'`除三选上屏外还支持挂接英文输入法（虎码官方自带）。
* 支持通过划动精确打字母。
  九宫格数字键：上划是数字（上划数字会直接上屏）；左、下、右划分别对应该键的第一、二、三个字母（这些字母由 Rime 控制，方便进行拼音反查和使用`/`斜杠功能）
* 上划反引号打出的`=`号由 rime 控制，有计算器功能。
* 结合划动上屏以及`;`引导的快符，这个布局可打出标准电脑键盘中**所有**中、英符号。
  （此处省略图示，请安装后自行点击、划动查看各个键。）
* 这些布局思路值得注意：

  1. 包括配套的中文全键在内，大部分上划符号由Rime控制（打出中文符号），下划打出英文符号；中文符号也是尽可能都设为半角，以提高兼容性。
  2. 左侧 Markdown 符号区：除要用到 rime 功能的特殊符号`` =/*` ``外，都是直接上屏英文符号；
  3. 点击数字键`2`/`3`后按回车，会打出`@`/`#`（这个设定是为了留出位置以满足`;`二选和`'`三选功能）；
  4. 斜杠`/`：左右划动可选择输入方案；
  5. 星号`*`：左右划动可在候选框中开关 emoji（改自虎码方案）；
  6. 反引号`` ` ``：左右划动快速定位行首、行尾；
  7. 空格：上划是数字0，左右划动是英文的问号和叹号；
  8. 边缘（最左列和最右列）的键只能向内划，无法向边缘划动。