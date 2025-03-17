此教程是在Gemini辅助下完成的（）

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

第二种方案是使用第三方网址提供的密钥

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

2. 来到(https://github.com/SillyTavern/SillyTavern/releases)往下翻

3. 点击图片中的圈起来的文件下载,然后解压,解压后双击 `Start.bat` 文件就可以了
![image](https://github.com/user-attachments/assets/037b8fd9-992c-4b45-9497-19288f4acde1)

## 2. 正式开始前的设置
