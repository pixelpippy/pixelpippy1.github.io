# L0G1000
1. TOC{:toc}

## 创建开发机并进行SSH连接

### 创建开发机

首先进入[InternStudio](https://aicarrier.feishu.cn/wiki/QtJnweAW1iFl8LkoMKGcsUS9nld#share-LeUxdm8Z0opL8exaZwGcNet7n2J)官网，登录账号后找到创建开发机的位置

<img src="书生第四期.assets/image-20241105213030879.png" alt="image-20241105213030879" style="zoom: 67%;" />

填写开发机名称和选择开发机镜像（镜像可以理解为软件的运行环境，InternStudio将运行环境打包成一个镜像，不需要手动一个一个配置运行，方便我们进行后期开发）

<img src="书生第四期.assets/image-20241105214021250.png" alt="image-20241105214021250" style="zoom: 50%;" />

这里镜像选择比较新的cuda版本的镜像

<img src="书生第四期.assets/image-20241105214103508.png" alt="image-20241105214103508" style="zoom:50%;" />

第一个作业不需要很强的GPU算力，选择第一个10% A100就可以了

<img src="书生第四期.assets/image-20241105214339744.png" alt="image-20241105214339744" style="zoom: 67%;" />

选择预计开发机运行时间，第一个作业一般半小时就可以足够，如果觉得时间不够的话可以自行调整

<img src="书生第四期.assets/image-20241105214502061.png" alt="image-20241105214502061" style="zoom: 80%;" />

有时候可能需要排队，稍微等一下

![image-20241105223252680](书生第四期.assets/image-20241105223252680.png)

#### 使用 vscode 进行SSH连接

vscode 是一个非常方便好用的集成开发软件，我们使用它进行SSH连接远程开发机

当成功分配开发机资源之后，可以点击右边的SSH连接，SSH是一种安全的连接方式，通过这种协议连接远程的开发机（服务器）

![image-20241105223508717](书生第四期.assets/image-20241105223508717.png)

**添加公钥**的作用是，方便以后再次连接服务器的时候不用输入密码，添加公钥之后，服务器就记住了你的电脑连接过服务器，下次再连接服务器就不需要输入密码了。如果是第一次连接服务器，一般还是需要先输入账号和密码的。

<img src="书生第四期.assets/image-20241105223800410.png" alt="image-20241105223800410" style="zoom:67%;" />

打开 vscode，并安装好 **SSH-remote 插件**，按照提示点击左边栏上的插件按钮，然后点击➕号新建一个连接，把刚才复制的**登录命令**和**密码**依次输入进 vscode上方弹出的窗口中

![image-20241105224424779](书生第四期.assets/image-20241105224424779.png)

输入**登录命令**之后，右下角会弹出连接的提示

![image-20241105224621222](书生第四期.assets/image-20241105224621222.png)

之后会弹出一个新窗口，上方提示需要输入**密码**

![image-20241105224820098](书生第四期.assets/image-20241105224820098.png)

右下角提示正在安装 vscode 服务器，稍微等一下

![image-20241105224918105](书生第四期.assets/image-20241105224918105.png)

左下角有这个SSH文字提示说明连接成功了

![image-20241105225240716](书生第四期.assets/image-20241105225240716.png)

### 进行端口映射和运行hello_world.py

按图示点击就可以打开开发机的终端

<img src="书生第四期.assets/image-20241105230341352.png" alt="image-20241105230341352" style="zoom: 67%;" />

创建 hello_world.py文件

运行 hello_world.py文件

![image-20241105235834247](书生第四期.assets/image-20241105235834247.png)

vscode 自动进行了端口映射，打开浏览器可以看到开发机运行的 hello_world.py 程序的输出

<img src="书生第四期.assets/image-20241105235743197.png" alt="image-20241105235743197" style="zoom:50%;" />



端口转发

![image-20241105235901949](书生第四期.assets/image-20241105235901949.png)

也可以手动改变映射到本地端口的地址

![image-20241106000201741](书生第四期.assets/image-20241106000201741.png)

### Linux 基础命令

![image-20241106000619871](书生第四期.assets/image-20241106000619871.png)

![image-20241106000724816](书生第四期.assets/image-20241106000724816.png)

## L0G2000

#### Leetcode 383

##### 代码

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        def count_letters(s):
            count_dict = {}
            for letter in s:
                if letter in count_dict:
                    count_dict[letter] += 1
                else:
                    count_dict[letter] = 1
            return count_dict

        def compare_counts(a, b):
            for key in a:
                if key not in b or a[key] > b[key]:
                    return False
            return True
        # 计算每个字母的出现次数
        dict_a = count_letters(ransomNote)
        dict_b = count_letters(magazine)

        # 比较两个字典中字母出现的次数
        result = compare_counts(dict_a, dict_b)
        return(result)
```



##### 通过截图

<img src="书生第四期.assets/image-20250211170210067.png" alt="image-20250211170210067" style="zoom: 67%;" />



#### debug

下图是查看debug信息

<img src="书生第四期.assets/image-20250211175946966.png" alt="image-20250211175946966" style="zoom:67%;" />

查看res的值：

```
res='根据提供的模型介绍文字，以下是提取的关于该模型的信息，以JSON格式返回：\n\n```json\n{\n  "模型名字": "书生浦语InternLM2.5",\n  "开发机构": "上海人工智能实验室",\n  "提供参数版本": "1.8B、7B和20B",\n  "上下文长度": "1M"\n}\n```\n\n这个JSON对象包含了模型名字、开发机构、提供参数版本以及上下文长度这四个关键信息。'
```

发现输出的信息不止包括json信息，估需要修改提示词，让模型只输出json信息，不输出多余的描述

修改提示词之后输出的res值：

```
'```json\n{\n  "model_name": "书生浦语InternLM2.5",\n  "development_institution": "上海人工智能实验室",\n  "parameter_versions": ["1.8B", "7B", "20B"],\n  "context_length": "1M"\n}\n```'
```

还是不行，模型会输出多余的头和尾，仅通过修改提示词的方式无法完全解决

故使用字符串表达式删除输出信息中多余的 \```json\n 和 \n```

```
res = res.replace('```json\n', '', 1).rstrip('\n```')
```

<img src="书生第四期.assets/image-20250212000230377.png" alt="image-20250212000230377" style="zoom:67%;" />

通过上述方法解决bug



## L0G4000

### 模型下载

使用Hugging Face平台下载模型

仅下载 config.json 文件、model.safetensors.index.json 文件

打开[Github CodeSpace](https://github.com/codespaces)

![image-20250217195707623](书生第四期.assets/image-20250217195707623.png)

选择进入网页版vscode界面，在下方终端中安装依赖库

![image-20250217200205829](书生第四期.assets/image-20250217200205829.png)

创建下载模型的配置文件，并保存，然后运行，可以看到已经从 hugging face 下载了相应的 json 文件到 codespace 中了

![image-20250217200625903](书生第四期.assets/image-20250217200625903.png)

### 模型上传

首先在codespace终端里运行安装git lfs的命令

![image-20250217201251461](书生第四期.assets/image-20250217201251461.png)

去[hugging face](https://huggingface.co/settings/tokens)创建access tokens

![image-20250217201513672](书生第四期.assets/image-20250217201513672.png)

然后使用token登录到 hugging face

![image-20250217201730024](书生第四期.assets/image-20250217201730024.png)

创建一个hugging face项目，命名为intern_study_L0_4，然后克隆到本地，接下来上传config.json文件和README.md文件到克隆的文件夹中，最后用git提交到hugging face远程仓库

![image-20250217204245815](书生第四期.assets/image-20250217204245815.png)

可以在Hugging Face的个人profile里面看到这个model，至此模型上传成功

![image-20250217204505409](书生第四期.assets/image-20250217204505409.png)



### Space上传

打开hugging face的spaces网页，创建一个新的space

![image-20250217204812185](书生第四期.assets/image-20250217204812185.png)

将space克隆到本地，然后修改文件夹中的index.html文件，然后提交push到远程仓库上，space会自动更新页面

![image-20250217205308453](书生第四期.assets/image-20250217205308453.png)

至此space上传成功

![image-20250217205352422](书生第四期.assets/image-20250217205352422.png)



## L1G1000

本次课程深入介绍了书生·浦语（Informer）大模型的开源开放体系及其发展历程。 

- **技术亮点**：涵盖从数据采集、模型训练到实际应用场景的全流程解决方案，并实现了显著性能提升及创新功能突破。例如，最新版Informer LM 2.5拥有卓越的推理能力和长达百万级别的上下文容量，在某些指标上甚至超过同类开源模型。 
- **核心优势**：强调高性能模型的全面覆盖，从小规模至大规模均适用；同时推出了一系列配套工具，诸如高效的微调框架、自动标签系统Label LLM等，极大简化开发者的工作流。
- **应用前景**：不仅限于基础研究领域，还积极拓展到了具体业务场景的应用探索，特别是Mind Search智能搜索平台展示了利用大型语言模型进行复杂查询的独特潜力。
- **社区建设**：重点阐述了围绕Informer LM建立的庞大生态系统，涵盖了丰富的数据资源、多样化的培训框架和详尽的测试标准，确保每个参与者都能从中受益并贡献自身力量。 

<img src="书生第四期.assets/image-20250217205831166.png" alt="image-20250217205831166" style="zoom:67%;" />

## L1G2000

基础任务

### MindSearch

<img src="书生第四期.assets/image-20250218203539063.png" alt="image-20250218203539063" style="zoom:67%;" />



### 书生·浦语

<img src="书生第四期.assets/image-20250218204559643.png" alt="image-20250218204559643" style="zoom:67%;" />

### 书生·万象

<img src="书生第四期.assets/image-20250218205654883.png" alt="image-20250218205654883" style="zoom:67%;" />

## L1G3000

### 基础任务

<img src="书生第四期.assets/image-20250218214352356.png" alt="image-20250218214352356" style="zoom: 80%;" />

### 进阶任务

科幻小说生成

提示词1：

```
你是一名科幻小说创作助手，负责引导作者构建一个独特而引人入胜的科幻世界。

技能：
- 📊 分析：分析科幻小说的历史和常见主题，以及当前科幻文学的发展趋势。
- 写作：创作详细的故事背景、角色设定和情节发展，确保故事既富有创意又结构严谨。
- 编码：利用逻辑和创意构建复杂的情节线索，确保故事的连贯性和吸引力。
- 🚀 自动执行任务：快速生成多个故事版本，以便作者选择最合适的情节。

# 💬 输出要求：
- 结构化输出内容：提供清晰的故事大纲，包括背景设定、主要角色、关键事件和结局。
- 为文章提供详细、准确和深入的内容：确保每个细节都经过精心设计，以增强故事的沉浸感。
- 其他基本输出要求：包括设定科学的合理性和技术细节的准确性。

# 🔧 工作流程：
1. 仔细深入地思考和分析用户的内容和意图，理解作者希望传达的核心主题和情感。
2. 逐步工作并提供专业和深入的回答，从宏观到微观，逐步构建故事框架。
3. 与用户保持沟通，根据反馈调整故事细节，确保最终作品符合作者的期望。

# 🌱 初始化：
欢迎用户，友好地介绍自己并引导用户使用。
```

<img src="书生第四期.assets/image-20250223204243427.png" alt="image-20250223204243427" style="zoom:80%;" />

提示词2：

```
你是专业的科幻小说创作助手，负责帮助用户构思和撰写高质量的科幻小说内容。
- 技能：
  - 📊 想象力丰富，能够构建独特的世界观和设定。
  - 🚀 熟悉科幻文学的经典元素和现代趋势，能够结合创新点。
  - ✍ 擅长叙事，能够通过引人入胜的剧情和角色塑造吸引读者。
# 💬 输出要求：
- 提供完整的故事框架，包括世界观设定、主要角色、核心冲突和情节发展。
- 结构化输出内容，按照章节或情节划分。
- 为故事提供**详细、准确和深入**的背景信息，确保故事的逻辑性和连贯性。
- 使用生动的语言和丰富的细节，增强故事的沉浸感。
# 🔧 工作流程：
- 仔细深入地思考用户提供的主题或创意，挖掘其潜力。
- 结合经典科幻元素和前沿科学概念，构建独特的故事世界。
- 逐步构建情节，确保故事有起伏、冲突和高潮。
- 提供角色背景和动机，使角色形象立体且真实。
# 🌱 初始化：
欢迎使用科幻小说创作助手！请告诉我您想要创作的科幻小说主题、风格或核心创意，我会帮您打造一个精彩的故事框架。
```

<img src="书生第四期.assets/image-20250223205001836.png" alt="image-20250223205001836" style="zoom:80%;" />

没有使用系统提示词：

<img src="书生第四期.assets/image-20250223205100448.png" alt="image-20250223205100448" style="zoom:80%;" />

由此可见，使用系统提示词可以使回复：

- 更好的文字创作能力（更明显的风格、更优美的文字、更准确的格式、更流畅的对话）
- 更准确的回答能力
- 更准确的流程遵循能力

## L1G4000

### LlamaIndex+InternLM API 实践

打开开发机并创建新conda环境

![image-20250224171135542](书生第四期.assets/image-20250224171135542.png)

#### 安装python 依赖包

![image-20250224171212022](书生第四期.assets/image-20250224171212022.png)

#### 安装 Llamaindex

安装 Llamaindex和相关的包

![image-20250224190921667](书生第四期.assets/image-20250224190921667.png)

#### 下载 NLTK 相关资源

我们在使用开源词向量模型构建开源词向量的时候，需要用到第三方库 `nltk` 的一些资源。正常情况下，其会自动从互联网上下载，但可能由于网络原因会导致下载中断，此处我们可以从国内仓库镜像地址下载相关资源，保存到服务器上。 我们用以下命令下载 nltk 资源并解压到服务器上：

![image-20250224190751883](书生第四期.assets/image-20250224190751883.png)

#### 不使用 LlamaIndex RAG（仅API）

![image-20250224192158424](书生第四期.assets/image-20250224192158424.png)

#### 使用 API+LlamaIndex

![image-20250224193042098](书生第四期.assets/image-20250224193042098.png)

#### LlamaIndex web

![image-20250224193436353](书生第四期.assets/image-20250224193436353.png)
