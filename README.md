0.介绍

大部分为转载,集思广益,将网络上的部分解决方案做了一些统一,以及优化.

本版本主要使用Google Tesseract的OCR图像识别功能,运行ADB调取Android截图.或WDA调iOS截屏.

然后进行百度搜索, 根据词频判断优先答案, 肯定会有相关问题, 具体选项还是要靠自己抉择.

相关内容链接:

tesseract python:

https://github.com/madmaze/pytesseract

http://blog.csdn.net/u010670689/article/details/78374623

https://github.com/tesseract-ocr/tesseract/wiki

Android手机调试ADB:

https://www.jianshu.com/p/1b3fb1f27b67

--------------------------------------------------------------------------------

1.Android准备工作

我这边环境是:

Mac OS:10.12.6 /  Android Phone Huwei P10 / python-3.6.4

a.

terminal终端里先使用homebrew安装ADB:

brew cask install android-platform-tools

b.

安装完成后,terminal终端运行 adb devices,成功如下图:




c.

安装python3,选择自己适用的版本下载:

https://www.python.org/downloads/

然后,命令行安装所需的依赖包(mac默认python版本2.7,故pip3为python3做准备):

pip3 install pillow

pip3 install requests

pip3 install colorama

d.

安装tesseract:

Mac系统:

brew install tesseract

pip3 install pytesseract

到https://github.com/tesseract-ocr/tessdata/blob/master/chi_sim.traineddata下载中文简体语言包,放到/usr/local/Cellar/tesseract/3.05.01/share/tessdata 目录下面(非常重要!!!).

Windows系统:

推荐使用安装版，在安装时选择增加中文简体语言包

● 安装版： https://digi.bib.uni-mannheim.de/tesseract/tesseract-ocr-setup-3.05.01.exe

● 免安装版： https://github.com/parrot-office/tesseract/releases/download/3.5.1/tesseract-Win64.zip 免安装版需要下载中文语言包，放置到Tesseract的tessdata目录下

e.

修改  common/ocr.py 代码相应目录信息(若从我的git上下载,则无需更改)
# win环境
# tesseract 路径

pytesseract.pytesseract.tesseract_cmd = 'C:\\Program Files (x86)\\Tesseract-OCR\\tesseract'

# 语言包目录和参数

tessdata_dir_config = '--tessdata-dir "C:\\Program Files (x86)\\Tesseract-OCR\\tessdata" --psm 6'

# mac 环境 记得自己安装训练文件

# tesseract 路径

#pytesseract.pytesseract.tesseract_cmd = '/usr/local/Cellar/tesseract/3.05.01/bin/tesseract'

# 语言包目录和参数

#tessdata_dir_config = '--tessdata-dir "/usr/local/Cellar/tesseract/3.05.01/share/tessdata/" --psm 6'



IOS

部分朋友成功

需要安装 WDA 进行截图，参考

iOS 真机如何安装 WebDriverAgent

Android 和 iOS 操作步骤

安装 python-wda

其他步骤相同。

python GetQuestionTessIos.py

--------------------------------------------------------------------------------

2.运行脚本

python3 GetQuestionTessAndroid.py

成功入下图,如有报错,请留言相关error.



注： 可以用 GetImgTool.py 调整题目截取位置 可以到这里查看部分手机截图设置

若屏幕分辨率不同,可能导致选项不能都识别出来，请在 ocr.py    line45行中自行修改代码即可

# 切割题目和选项位置，左上角坐标和右下角坐标,自行测试分辨率,如果嫌烦可以多试几次即可.

question_im = image.crop((50, 350, 1000, 560)) # huawei P10

choices_im = image.crop((75, 535, 990, 1200))
![](https://github.com/MacMan/AnswerQuestions/raw/master/resources/WX20180113-163457@2x.png)  2018


3.加群闲聊,一起答题,毕竟机器是没有灵魂的,还是需要人来操作~

Q群:592332973或扫下面二维码.


