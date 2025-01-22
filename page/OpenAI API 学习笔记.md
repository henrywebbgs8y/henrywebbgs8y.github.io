## 获得 OpenAI API Key

### 获得 OpenAI 账号

如果之前使用过 ChatGPT，那么 ChatGPT 的账号就是 OpenAI 账号，可以直接使用。

如果没有账号，可以通过以下方式注册：

- 由于国内访问限制，注册可能较为复杂。可以参考网上的注册教程。
- 如果觉得麻烦，可以通过第三方平台购买账号，或者直接购买有额度的 API Key。

### 获取 OpenAI API Key

1. 登录 OpenAI 后，鼠标移动到页面左侧，弹出侧边栏。
2. 点击侧边栏中的 **API Keys** 进入 API Keys 页面。
3. 点击 **Create new secret key** 创建新的 API Key，命名后点击确认。
4. 弹出的对话框中会显示新创建的 Key，请务必保存下来。关闭对话框后将无法再次查看。
5. 保存完成后，点击 **Done**，即可在页面中看到新创建的 API Key。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)

---

## 获取 API 使用额度

### 额度查询

1. 点击侧边栏中的 **Usage** 进入使用页面。
2. 页面左侧显示每日花费，右侧显示额度：
   - 灰色：未使用；
   - 绿色：已使用；
   - 红色：已过期。

只有当额度处于未使用状态（灰色）时，API Key 才能成功调用 API。

### 额度充值

1. 点击侧边栏中的 **Setting** 下的 **Billing** 进入账单页面。
2. 在页面中可以管理充值相关事项：
   - 添加支付方式：点击 **Payment methods** 管理支付方式。
   - 国内 Visa 卡可能无法使用，可以选择国外卡或虚拟卡。
   - 推荐使用 [WildCard](https://bit.ly/bewildcard)，支持便捷支付。

3. 添加支付方式后，回到 **Overview** 页面，点击 **Add to credit balance** 进行充值。
4. 充值完成后，回到 **Usage** 页面即可查看可用额度的变化。

---

## Python 使用测试

### 配置 Python 环境

- Python 版本需为 3.7.1 以上。
- 推荐使用 Anaconda 创建虚拟环境。

### 安装 OpenAI 库

通过 pip 安装 OpenAI 库：

bash
pip install openai


### 设置你的 API Key

OpenAI 默认从环境变量中读取 `OPENAI_API_KEY`，可以通过以下两种方式设置：

1. **为所有项目设置**  
   在系统环境变量中添加 `OPENAI_API_KEY`，然后通过命令行验证：

   bash
   echo %OPENAI_API_KEY%
   

2. **为单个项目设置**  
   在项目根目录创建 `.env` 文件，内容如下：

   plaintext
   OPENAI_API_KEY=你的Key
   

   使用 `dotenv` 加载环境变量。

### 发送请求测试

以下是一个简单的 GPT-3.5 Chat 请求示例：

python
import os
import openai
from dotenv import load_dotenv

load_dotenv()

openai.api_key = os.getenv("OPENAI_API_KEY")

response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a poetic assistant."},
        {"role": "user", "content": "Compose a poem about recursion in programming."}
    ]
)

print(response['choices'][0]['message']['content'])


在 [Usage 页面](https://platform.openai.com/usage) 可以查看请求的花费和 Token 数量（可能有延迟）。

---

## 功能介绍（以 Python 为例）

### 文本生成（Text Generation）

OpenAI 提供强大的文本生成功能，可以理解语言并返回文字。以下是一个示例：

python
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Who won the world series in 2020?"},
        {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
        {"role": "user", "content": "Where was it played?"}
    ]
)

print(response['choices'][0]['message']['content'])


#### 输入参数说明

- **system**：设置 AI 的行为或个性。
- **user**：用户输入的信息。
- **assistant**：AI 的回复，可以作为上下文。

#### 输出参数说明

- **finish_reason**：表示回复的完成状态：
  - `stop`：正常完成；
  - `length`：达到最大 Token 限制；
  - `content_filter`：内容被过滤。

---

## 总结

通过以上步骤，您可以快速上手 OpenAI API 的使用，包括获取 API Key、管理使用额度以及在 Python 中进行集成和测试。如果需要便捷的支付方式，可以尝试 [WildCard](https://bit.ly/bewildcard)，轻松解决支付难题。