尽管我觉得可能都没人来看这教程，但以防万一，不要把这个教程大范围传播，也不要说是我写的教程（

## 0. 前言

本教程面向具备一定电脑基础和动手能力的人员。因此，基础操作将不再赘述。

本教程介绍的AI翻译方法，并非直接将文本全自动翻译，而是**分段**使用AI进行翻译，并由人工进行**校对**和**修正**。  **强烈建议**不要直接采用AI的翻译结果，人工检查至关重要，以避免AI可能出现的错误。

通常情况下，AI在意义理解上不会出现偏差。即使出现错误，结合上下文也容易发现。

因此，使用AI辅助翻译对日语基础要求不高。 即使像我一样，仅能听懂日语而无法阅读的人，也可以通过逐句听取并借助机翻软件进行核对，来确认翻译的准确性。实践表明，AI在意义翻译上出错的情况极少。

Ps：哪怕不打算汉化，只打算用ai整点涩涩也可以看下此教程（）

## 1. 基础需求
开始翻译，您需要准备两样工具：可用的AI模型以及SillyTavern


## 1.1 可用的AI模型

在AI的选择方面，我们通常有两种方案：一是本地部署AI模型，二是使用他人提供的在线AI服务。

考虑到本地部署AI模型以达到与在线AI相近效果所需的硬件配置过高，本教程暂不推荐此方案。 本教程将以相对容易获取且免费的谷歌AI模型 Gemini 2.0 Pro 为基础进行编写。  

以下我将提供两种免费获取 Gemini 2.0 Pro 的方式。

第一种方案是使用谷歌官方提供的 Gemini API。

操作步骤如下（需要梯子，但到使用的时候可以通过修改Host避免使用梯子  ）：

1.  访问 [Google AI Studio](https://aistudio.google.com/)
2.  点击![image](https://github.com/user-attachments/assets/bdbeb835-dd25-406e-a792-ef1e24e31e5d)
使用你的谷歌账号登录。
3.  在页面中找到并点击 ![image](https://github.com/user-attachments/assets/9d8008e0-7d86-4191-ba2b-76ac0da990ec)
4.  创建一个新的 API 密钥。
5.   密钥创建完成后，**复制** 你的 API 密钥。 请妥善保管，不要泄露。
6.  **检查免费额度:**  如果页面下方显示您的方案不是免费的，请**刷新页面**。 刷新后，您的方案应显示为免费。
这样你就得到了能够免费使用Gemini 2.0 Pro的密钥，理论上限是每天50次，但我没使用到上限过，所以我并不清楚具体是多少次。但另外一种方法可提供每日200次Pro模型

以下任选其一加入Host文件中便可正常使用,没用请换一个试试
47.103.15.240 generativelanguage.googleapis.com
142.251.223.35 generativelanguage.googleapis.com
120.26.207.106 generativelanguage.googleapis.com
都失效的话可使用(https://github.com/Ponderfly/GoogleTranslateIpCheck),在config.json里添加generativelanguage.googleapis.com扫描


第二种方案是使用第三方网址提供的密钥(目前这个方式暂时有点问题,容易莫名其妙的截断)

操作步骤如下：

1.  **访问 [openrouter](https://openrouter.ai/)**
2.  **点击右上角的Sign in登录，可使用你的谷歌账号登录。**
3.  **然后来到(https://openrouter.ai/settings/keys)创建一个新的 API 密钥。**
5.  **密钥创建完成后，**复制** 您的 API 密钥。 请妥善保管，不要泄露。**

以上两种密钥的具体使用方式后续会讲

## 1.2 SillyTavern

SillyTavern（简称ST）是一个本地安装的用户界面，它允许你与文本生成的大型语言模型（LLMs）、图像生成引擎和TTS语音模型进行交互。目标是尽可能地赋予用户对其大型语言模型提示尽可能多的实用性和控制权，并将陡峭的学习曲线视为乐趣的一部分。

（反正你只要理解这是一个可以方便破除ai限制或添加一些要求的玩意，主要用处是使用ai进行角色扮演，包括涩涩）

通过Git安装SillyTavern

安装步骤

1. **安装NodeJS(https://nodejs.org/en) (推荐安装最新的LTS版本)**

2. **安装Git for Windows(https://gitforwindows.org/)**

3. **打开Windows资源管理器** (Win+E)

4. **浏览或创建一个文件夹**，该文件夹不受Windows控制或监控。(例如：C:\MySpecialFolder)

5. **在该文件夹内打开命令提示符**。方法是点击顶部地址栏，输入`cmd`，然后按Enter键。

6. **当黑色框 (命令提示符) 弹出后**，在其中输入**以下命令之一**，然后按Enter键:
    - **发布分支:** `git clone https://github.com/SillyTavern/SillyTavern -b release`
    - **预发布分支:** `git clone https://github.com/SillyTavern/SillyTavern -b staging`

7. **克隆完成后**，双击 `Start.bat` 文件以使NodeJS安装其依赖项。

8. 服务器将启动，SillyTavern将在您的浏览器中弹出。

如果不会使用以上操作进行安装,下面则是一个简易版本的安装步骤,缺点是**无法自动更新**

1. 还是安装NodeJS

2. 来到(https://github.com/SillyTavern/SillyTavern/releases) 往下翻

3. 点击图片中的圈起来的文件下载,然后解压,解压后双击 `Start.bat` 文件就可以了
![image](https://github.com/user-attachments/assets/037b8fd9-992c-4b45-9497-19288f4acde1)

## 2. 正式开始前的设置（如果要涩涩，请到类脑Discord之类的地方找到合适的预设和角色卡导入，我会在最下面提供类脑的地址）

## 2.1 预设和接口
首先在SillyTavern 界面点击上方的插头标志![image](https://github.com/user-attachments/assets/8165f634-12d2-41e8-bf0f-3c4bb9a4f61b) 将Api切换为聊天补全![image](https://github.com/user-attachments/assets/454fb1df-c4d0-43fa-a5f4-aa3a4722c3e5)

再点击![image](https://github.com/user-attachments/assets/71ffb68e-a071-41be-ada2-f189f7c0df8e) 点击此处导入我提供的翻译用预设![image](https://github.com/user-attachments/assets/a630e9a8-89f8-4777-b7bb-1e25d1697a02)

预设导入完毕后,再点击插头,将谷歌官方密钥填入![image](https://github.com/user-attachments/assets/0892fd1f-807d-45f4-8b25-dd0a95d94d4b)

或者将聊天不全来源切换至自定义,将 https://openrouter.ai/api/v1 填入代理服务器URL,再将openrouter的密钥填入自定义API密钥中,模型选择google/gemini-2.0-pro-exp-02-05:free,提示词后处理改为严格

连接后请点击发送测试消息确认接口是否可使用

## 2.1 正则和角色卡
点击![image](https://github.com/user-attachments/assets/97bdfb2b-1b3c-44ed-a3ea-59430d0f11f9),再点击正则,导入我提供的正则

最后点击![image](https://github.com/user-attachments/assets/ffdcac3a-4b39-4559-9440-e1ab2caa680a),点击此处导入我提供的角色卡![image](https://github.com/user-attachments/assets/dd104a10-1f18-4b6c-b8f8-747d0472dbec),再点击此处导入世界书![image](https://github.com/user-attachments/assets/e232f763-d77b-4448-adcb-ff84e921d7ca)


## 3. 开始翻译

这一步就很简单了,复制需要翻译的内容到此处后![image](https://github.com/user-attachments/assets/9e4ed1e5-83a4-4676-b396-f0d36a52082a)

点击纸飞机标志发送即可,然后等待一会就会翻译完成(出现错误请参考之后我列出的常见错误列表),之后重复以上操作进行翻译,这样后续翻译会和之前的翻译风格统一

如图所示

![image](https://github.com/user-attachments/assets/6e2028f0-7d7f-45bd-9841-03387e0e1881)
![image](https://github.com/user-attachments/assets/11863640-07e4-493f-964a-2dac53edb181)

## 4. 可自定义的部分
右边的角色描述中的Translation Guidelines是可修改,你有任何特殊的要求都可以写在那里

预设中往下翻看到的条目点击![image](https://github.com/user-attachments/assets/3dd012c0-68f6-4e6a-b892-3de598706188) 也是可修改的,你能理解干什么用的部分都可以修改

## 4. 1 世界书
点击此图标![image](https://github.com/user-attachments/assets/734a8c4d-d38d-4c14-9cab-6a2e6a579991) 将会弹出世界书界面,里面有我觉得需要给ai解释的部分,如果你也有需要向ai解释的部分,也可以添加条目

![image](https://github.com/user-attachments/assets/b83f9288-791b-44b0-938f-69612bed8aff)

如图所示,蓝灯是会一直发送给ai的部分,绿灯则是触发关键词才会发生给ai的部分

![image](https://github.com/user-attachments/assets/ab540adc-53b8-4cc7-b058-b444f00aef55)

此处则是调整这些资料发生给ai的时候在什么位置,ai也是有记忆上限和注意力的,一般来讲越靠后的资料,ai记得越清楚

角色定义之后会在World Info (after)中

@D ⚙ 则是会作为系统提示发生给ai,1代表会在Chat History倒数第二条位置

![image](https://github.com/user-attachments/assets/f877f1fd-65d7-44dd-a6b7-0b218c8688c1)

## 5. 翻译过程需要处理的情况

如果ai翻译出现小错误或者对某一处的翻译效果不满意,请点击对话界面右上角的![image](https://github.com/user-attachments/assets/890c2601-ba75-4d8b-a48c-52f4a0cbde5b) 可修改ai输出的译文.

请记住必须及时修改这些,如果不修改类似的问题会在后续翻译中反复出现,因此最开始几次的翻译效果很关键,他们将决定后续翻译的效果.

## 5.1 报错

当ai出现报错时候,可在如图所示的窗口查看报错资料

![image](https://github.com/user-attachments/assets/1e42aad0-e110-4d8c-b25a-556ff890b42c)

以下是几种常见报错和处理方式

1.429，当出现这个错误时，意味着你在短时间里进行太多次请求，api每分钟可请求的次数是有上限的，但有时候，特别是使用梯子的时候会出现不管使用什么模型，隔多久使用也会报429，这一般是你所使用的IP异常有问题或者使用Gemini的人过多了

2.OTHER，当报错资料里会有个很显眼的OTHER时，意味着你的输入的内容被阻断了，这一般是有什么过于敏感的内容，不过我觉得正常翻译很难触发这个问题，解决办法是加强破限（但预设我还在慢慢改，且我没怎么遇到这个问题，所以之后再说，咕咕咕），还有一种情况是谷歌抽风，之前有段时间有个bug Gemini一输出中文就会自动截断，这种官方的问题只能等

3.Empty，当报错资料里会有个很显眼的Empty时，意味着ai的输出内容被阻断了，和OTher一样，不过大部分时候点右下角的右箭头或着点左下角菜单栏里面的重新生成再输出一遍就能解决，还有不要开流式输出。

## 6. 一些资源地址

Chub(https://chub.ai/) 这是一个国外的角色卡网站，尽管角色卡是英文，但通过预设什么的要求，ai是会输出中文的，或者你翻译一下开场和世界书就行

类脑(https://discord.gg/6kdVgVgcRx) 尽管类脑里的傻逼不少，管理人员甚至光明正大的搞岁月史书，但不得不说类脑确实是目前中文圈里极为大型的ai社区了，好东西不少，多翻翻能发现很多有意思的东西，但搞岁月史书的那帮b还是傻逼

旅途(https://discord.gg/elysianhorizon) 旅途是类脑的存放角色卡的频道
