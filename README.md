# 备忘1

### 我们需要解决的主要问题：
1. 如何从音频中提取特征？ `<- 我们在这里`
2. 如何对音频进行编码以进行训练？
	1. 重要的功能
	2. 如何减少尺寸
3. 用于训练的模型是什么？

对于当前任务，请参考存储库的[Projects](https://github.com/darknessest/gen_audio/projects/1)看板。
随时在Projects添加任何任务，或记录你当前做什么，这样就减少工作重叠。

------ 

## 1. 音频功能

原始音频包含大量信息，我们必须找到一种方法来提取该信息(特征)，然后确定对我们的任务有用的东西，由于计算和算法的限制，我们无法全部使用(请参阅 *curse of dimensionality*)。但是我们希望尝试获取尽可能多的信息，因为我们总是可以放弃其中的一些信息。

**这里的经验法则：**
> 信息越多越好。尺寸越小越好。

在以下图片中，你可以看到音频文件的最常见表示形式：
<p align="center">
	<img src="https://github.com/darknessest/gen_audio/blob/master/img/1.jpeg">
</p>

但实际上你可以提取更多特征，例如：

- Mel-frequency spectrogram:
<p align="center">
	<img src="https://github.com/darknessest/gen_audio/blob/master/img/mel-freq.png">
</p>

- MFCC:
<p align="center">
	<img src="https://github.com/darknessest/gen_audio/blob/master/img/mfcc.png">
</p>

- spectrum of frequencies:
<p align="center">
	<img src="https://github.com/darknessest/gen_audio/blob/master/img/sofreq.png">
</p>

- 还有很多...

这是必须要做的初步步骤。**如果没有完成此步骤，我们将无法前进。** 每个人都应该尝试亲手完成这一步，这样你就了解我们正在处理哪些数据。了解数据可能会为你提供进一步的见解。


#### 任务：
1. 查找用于特征提取的库" <- 当前任务"
2. 布局所有可用特征
3. 分析哪些特征是重要的
	1. 通过使用特征重要性算法
	2. 通过制作和分析具有特征的地块
4. 编写音频编码算法


#### 测试某库流程:
1. 在github上搜索库或使用搜索引擎
2. 检查是否达到我们的项目要求
3. 选择库并记录一下你正在研究某库（记到[Projects](https://github.com/darknessest/gen_audio/projects/1)的In progress）
4. 下载库
5. 测试来自`样本`的文件
6. 写一个关于图书馆可用性的小报告
	1. 最好是一个jupyter笔记本，带有代码片段和你的注释
	2. 或带有截图的.md / .pdf文件
7. 过一会，我们将讨论并决定要使用哪个库


#### 注意：
- 我们使用的是任何原始音频格式(.mp3，.wav等)，
- 我们使用Python 3编写所有内容，因此请确保你找到/编写的所有代码都可以在此环境中执行。
- 如果某些库是用其他语言编写的，那么我们总是可以编写一个连接器。
- 我建议你使用Jupyter来测试库和绘制一些数据。你可以将其与虚拟环境连接。
- 我建议你使用python虚拟环境，例如[venv](https://docs.python.org/3/library/venv.html)或[Anaconda](https://anaconda.org/anaconda/python)。
- 请确保你已安装scikit-learn和numpy。 (用于功能分析)
- 在早期阶段，当我们编写音频编码器时，你无需担心如何将该代码合并到ML项目中。它可以是我们在训练模型之前运行的独立脚本。

------

## 2.  ML模型
模型有一个输入(我们的编码数据)，将数据通过算法传递后，它应该产生一个输出。如果创建音频编码器，则你的模型只能在此数据类型的环境中工作。这意味着它不能产生不同类型的数据，并且，如果你想听音频，还必须制作音频解码器。在大多数情况下，这并不难，但关键是你要丢失一些信息。

为了对现有音频模型进行真正的改进，我们需要创建一个新的体系结构。具有LSTM的模式识别模型的集合，并且可以是GAN。但这部分是开放的 可供讨论，因为这是实际的研究部分。

#### 任务：
1. 选择几种适合我们任务的模型
2. 建立架构
3. 训练

#### 注意：
- 我们不仅限于Tensorflow或Pytorch之类的任何特定ML库
- 实验室的服务器具有多个图形卡，因此我们可以一次训练多个模型，或者创建一次使用多张显卡的模型。
- 在MIDI上有效的模型不一定在原始音频上有效，因为我们处理的是多维数据。
- 我们正在研究生成音乐模型，这与目前大多数音频相关研究不同。

...
