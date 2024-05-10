# ASSFont
自动化提取 ASS 字幕字体，并可实现字体子集化并进行视频混流。

# 使用说明
提前声明，我自己没用过 Python 写图形化程序，也没有专门学过 Python 。
只是平时混流和提取字幕嫌麻烦所以一直想写一个自动化的脚本。

## 子集化字体
将字幕使用的字体全部进行子集化，提取出必要的字形，可以大幅降低字体所占附件体积。
开启此选项的同时会生成专用的字幕文件(将原字幕中所有相关字体名称替换为子集化后的名称)，与子集化字体一起放在 result 文件夹中。

## 使用缓存
程序检测 C:\Windows\Fonts (需要以管理员身份安装字体到此目录)中所有的字体(包括子文件夹中的字体)。
每次重新读取字体名称会非常耗时，所以会生成一个简单的文件保存名称信息以加速后续获取，关闭此功能以重新生成缓存。

## 混流输出文件的视频属性标识
混流时会读取原mkv文件名称(去后缀)，将此名称设为混流输出视频的标题。
并且在此名称之后加上一个空格和此设置项的属性标识作为混流输出视频的文件名。

## 混流轨道的语言设置
可以设置为其它语言。中文请设zh，日文请设ja。

## 混流轨道的名称
mkv中每个轨道都可以加上一个名称。

## 混流视频轨道的分辨率
其实可以想办法获取mkv中视频轨的分辨率，但是加上别的库可能exe太大了，所以需要自行设置。

## 混流音频轨道的延迟
冷知识，mkv中可以设置轨道延迟。并且一般会造成的延迟都是写入音频轨中，所以加入这个设置。
例如按帧剪切视频之后，音频大概率剪切不到相同的时间，只能切到临近的一个时间，于是音视频之间就有了一个相对延迟。
如果你不知道怎么获取此延迟值也可以不管，因为那个延迟值高也不太会到上百毫秒，动画本身音视频就有一定“错位”，所以这点延迟也不是那么重要。

## 混流字幕轨道判定的标识符
例如判定简日的标识符为\[CHS_JPN\]，那么只要字幕文件名中包含该值就判定为简日字幕。

## 混流字幕轨道名称分割符
这个算是我们自己会用到所以加的判定。
如果一个字幕文件名为 \[KyokuSai\] Yume \[CHS_JPN\].kawaii.ass 则判定 style 为 kawaii 。
在字幕轨道名称为 简日双语-CHS_JPN 时，最终为轨道命名会是 简日双语-CHS_JPN<分隔符>kawaii 。
如果不想加上此分隔符和 style ，字幕名称中不要出现多个小数点即可。

## 混流字幕轨道有多style时判定默认轨道的style名
在简/繁/日无多 style 时，每个语言只有一个字幕，则该轨道会设为默认轨道。
如果单语言有多字幕，会将与该设置项的 style 对应的字幕设置为默认轨道，这样在有多个样式时观众打开视频会载入推荐样式。

## 子集化字体之后添加的警告标识
很多观众因为不了解子集化，所以很容易安装子集化后残缺的字体。
我个人觉得有必要加一个警告。
另外子集化字体名称会在此警告之后加上一个随机字符串，以防止在播放器中打开时遇到同一个字体名称而使用缓存文件的问题。
附件名称则包含有原字体名，如果观众好奇某个字体是什么也至少有个方法知道字体名字。
