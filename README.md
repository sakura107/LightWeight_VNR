#  LightWeight_VNR

---

## 说明

- 本项目可通过向`游戏列表`添加`游戏`从而打开，并可转区运行
- 本项目可调用`Textractor`来抓取`Galgame`的游戏文本
- 本项目可调用`Tesseract-OCR`抓取文字，支持`日文`、`简体中文`、`繁体中文`、`英文`
- 本项目可调用`JBeijing`、`有道词典`、`百度翻译`来实现翻译功能
- 本项目可调用`Yukari2`等TTS来实现文本阅读功能

---

## 使用方法

### 游戏列表
- 填好`游戏名称`、`程序目录`、`启动方式`、`特殊码`（没有可不填）后`添加`即可
    - `程序目录`、`启动方式`必须填，`游戏名称`若为空，添加时将`程序名`作为`游戏名称`
    - 转区运行需在`设置`中设置`Locale Emulator路径`
- 修改游戏信息后按`添加`即可修改信息
- 选择一项游戏后按`删除`即可删除
- 选择一项游戏后按`启动游戏`即可启动游戏，并自动启动`Textractor`注入`dll`

### Textractor
- 设置`Textractor目录`，确保目录下有`TextractorCLI.exe`和`texthook.dll`
- 点击`启动TR`，选择`游戏进程`，再`Attach`注入`dll`，之后选择`钩子`并`固定`即可
- `dll`注入后，游戏进程不关，则再次打开程序只需`启动TR`即可，无需再`Attach`
- `特殊码`使用之前必须确保`dll`已注入，且`特殊码`格式必须正确
- 若文本抓取出现问题，可尝试`终止TR`后再`启动TR`

### OCR
- 设置`Tesseract-OCR路径`
    - 确保目录下有`tessdata`、`libgcc_s_seh-1.dll.`、`libgif-7.dll`、`libgomp-1.dll`、`libjbig-2.dll`、`libjpeg-8.dll`、`liblept-5.dll`、`liblzma-5.dll`、`libopenjp2.dll`、`libpng16-16.dll`、`libstdc++-6.dll`、`libtesseract-5.dll`、`libtiff-5.dll`、`libwebp-7.dll`、`libwinpthread-1.dll`、`tesseract.exe`、`zlib1.dll`
    - 确保`tessdata`目录下有`chi_sim.traineddata`、`chi_sim_vert.traineddata`、`chi_tra.traineddata`、`chi_tra_vert.traineddata`、`eng.traineddata`、`jpn.traineddata`、`jpn_vert.traineddata`
- `截取`屏幕上的某一区域，用鼠标划定区域，划定完按`Enter`
    - 截取完会直接显示截图图片和文本
    - 若想取消划定操作，按`ESC`键
- 截取一次后按`连续`，则开始以某一间隔在同一位置进行连续识别
    - 按`结束`则结束连续识别
- 根据程序显示的图片效果，可以调整`阈值`和`阈值化方式`

### 翻译
#### JBeijing
- `JBeijing`启用并保存后，即可获得翻译文本
#### 有道
- 注意：`有道`调用的不是API，而是本地的有道词典程序（不可`最小化`）
- 设置好`有道词典路径`后，点击`启动有道`，并切换到词典`翻译`页面
- 若本程序获取的翻译文本`错位`，可尝试增加`翻译间隔`
- 可以取消`抓取翻译`，并将词典的翻译栏拖在游戏窗口下方
- 若`有道词典`的翻译有问题，可尝试`终止有道`后再`启动有道`
#### 百度
- 注意：`百度翻译`是在线翻译，需要使用百度账号免费申请api，流程如下：
1. [https://api.fanyi.baidu.com/](https://api.fanyi.baidu.com/)进入百度翻译开放平台
2. 按照指引完成api开通，只需要申请`通用翻译API`
3. 完成申请后点击顶部`管理控制台`，在申请信息一栏可获取`APP ID`与`密钥`
- 启动百度翻译前需要填写`APP ID`与`密钥`并且**保存**

### 文本
- `文本去重数`：文本重复的次数，比如`aabbcc`为重复2次
    - `智能去重`：根据句子自动判断重复次数并去重，勾上后`文本去重数`失效
- `垃圾字符表`：去除文本中含的`垃圾字符`，`垃圾字符`以`空格`分隔
- `正则表达式`：将`正则表达式`中的所有`()`部分连接，剩下的去除

### 语音
#### Yukari2
- 设置好`Yukari2路径`后，点击`启动Yukari2`即可（可`最小化`）
- `连续阅读`：连续阅读`抓取文本`，即抓取到`新文本`时读取`新文本`
- `阅读内容`：勾上的内容会读取，反之忽略
    - 判断依据：有`「`、`『`、`（`的为`角色对话`，反之为`旁白`

### 打包
- 本项目可用`Pyinstaller`打包，注意要在32位`Python`环境下，否则`JBeijing`不可用

---
## 额外说明
- 本项目作为本人业余学习`Python`的一个实战项目，同时也为了满足我对于`Galgame`的追求
- 因界面排版问题，选择`Microsoft YaHei Mono`字体
- 因所使用的的库的问题，`启动有道`或`启动yukari2`后，点击`目录`等按钮会卡死，目前无解决办法