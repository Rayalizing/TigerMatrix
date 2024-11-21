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

![手机键盘](https://github.com/Rayalizing/TigerMatrix/blob/main/hamster_keyboard_for_TM.jpg)

## 食用方法：

1. 安装 Rime 输入法（鼠须管、小狼毫）；
2. 按照虎码官方教程部署好虎码方案；
3. 将本方案 Rime 目录下的内容放入用户文件夹根目录；
4. 重新部署 Rime；
5. 在输入法中，选择本方案，即可使用。
6. 示例中的手机键盘适配 ios 端的【仓输入法】，可把文件 `hamster_keyboard_for_TM.yaml` 放入 `iPhone/Hamster/` 目录，并在输入法中`键盘布局`右上角加号中导入该文件。

## 教程：

1. 学会九宫格打字
2. 学会虎码
3. 唯一需要知道的在于如何打出辅码（看完[文章](https://zhuanlan.zhihu.com/p/107201990)中的原理你就知道了）：

    虎码是四码定长，而这里辅码的作用是在九宫格上精确选出要打的字母。

    总的来说，每打两个码选一次（即，加一个辅码）；如果码长为单数，则用三个特定符号来选择最后落单的这个码。

    * 对于原本码长为2码、4码的字词来说，辅码存在于第三位和第六位（第三位用来选原本前两位的码，第六位用来选原本后两位的码）。这样，码长变为了3码、6码。
    * 对于原本码长为单数（1和3）的字词来说，该方案使用符号来作辅码：“/”、“*”、“`”来选择落单的重码（分别对应九宫格上一个键的第一、第二、第三个字母）。这样，码长变为了2码、5码。
