### Stable Diffusion 简介


+ Stable Diffusion 是 Stability AI 公司开发的一款文本到图像的产品模型
+ 是由 Runway 的 Patrick Esser 和慕尼黑大学机器视觉与学习研究小组的 Robin Rombach（以前是海德堡大学的 CompVis 实验室）领导的，基于他们之前在 CVPR'22 上的潜在扩散模型工作，并结合了社区的支持在 Eleuther AI、LAION 和 Stability 生成 AI 团队


+ 它类似于 DALL-E 2，因为它是一个 Diffusion 模型，可以用来从文本提示中生成图像。与 DALL-E 2 不同的是，它是开源的，有 PyTorch 实现[1]和 HuggingFace[2]上的预训练版本。它是用 LAION-5B 数据集[3]训练的



### 安装问题


本地安装

[原地址](https://github.com/AUTOMATIC1111/stable-diffusion-webui) 

[mac 安装地址](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Installation-on-Apple-Silicon) 


### 启动时报错

socket 问题
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202304091531621.png)
fix: 网络问题,检查代理是否全局


端口问题
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202304091534211.png)
fix: 默认7860,检查端口是否被占用


Generate报错
<div style="text-align: center; font-size: 30px;">

<font color=#bf616a>RuntimeError: "LayerNormKernelImpl" not implemented for 'Half'</font> 

Reason: 无法识别gpu

fix: 把 `export COMMANDLINE_ARGS="--skip-torch-cuda-test --precision full --no-half"` 添加进 `web-user.sh` 

i.e. 上面指令意思就是生成时忽略CURA显卡测试 使用cpu渲染
</div>


[中文切换设置](https://github.com/VinsonLaro/stable-diffusion-webui-chinese) 


[google colab 在线安装](https://github.com/camenduru/stable-diffusion-webui-colab) 



### 基础


文字转图参数说明
![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202304231038151.jpg)


提示词实例

+ Self-Portrait by Egon Schiele 席勒自画像

+ illustration print of horse head sculpture, super detailed, by dan mumford, by aaron horkey, high contrast, low poly style 铜马

+ thick coated oil painting close-up portrait of sad boy, by ben quilty, by hikari shimoda 厚涂油画


+ illustration of close-up street view of gothic town, night, by peter mohrbacher, by alex andreev, by jacek yerka, large depth of field, super detailed, digital art, trending on artstation, minimalism 哥特式小镇的特写

+ fine silver badge, baroque pattern, relief angry cat, medieval, merchandise display, photorealistic, hyper realistic, octane render 猫


#### 文本描述 tag用法

1. `,` 分隔tag
2. `(tag)` 单括号加权重 比值 1.1倍
3. `((tag))` 双括号double 1.1 * 1.1 => 1.21倍
4. `(tag:1.2)` 直接写倍数
5. `tag|tag tag` 混合 i.e. red|blue hair => 红色加蓝色混合的头发
6. `[tag:tag:0.5] tag` 渐变 i.e. [white:gray:0.5] hair => 白色渐变到灰色
 
[更多用法](https://tags.novelai.dev/) 


[采样器](https://zhuanlan.zhihu.com/p/612572004) (Sampling method)

在目前阶段(unix:1681105120000), 使用最多,比较高效, 效果最好的是
+ DPM++ 2M Karras i.e. 二次元风格
+ DPM++ SED Karras i.e. 写实风格


#### 采样步数(Sampling steps)

设置过低出图可能是模糊的,过高会出现一些奇怪的东西,总的来说控制在20~30之间效果最好, 可以细微调整


#### 提示词引导系数(CFG Scale)

用来控制提示词的匹配吻合度


#### 分辨率

在选主模型时查看 base model 的版本, 一般SD 1.5 或者没特殊标注的都是 512 * 512, 有特殊标注的如 SD 2.1 768, 就是 768 * 768的, 如果再生成时选择了过高的分辨率, 可能会出现几个头几个手

[ControlNet](ControlNet.md) 基本介绍


[UI端启动配置项目](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Command-Line-Arguments-and-Settings) 


sd基础模型版本现在有1和2

+ 1 用的是OPEN AI 的CLIP,其模型本身开源,但是训练clip的数据集不开源 -> 可能会有版权问题
+ 2 用的是OPEN CLIP,是clip的开源版本,过滤了NSFW图像 -> 无版权问题
+ sd基础模型的特点就是多样性,但是具体细节风格不稳定


一些名词概念
 
+ VAE 是一种编码解码模型,负责图像处理
+ U_net 是一种卷积神经网络, 用来预测噪音,工作在浅空间中,
+ clip 文字处理模型,把文字转化为u_net能理解的状态,并在解码时不停地和u_net"做插值"来影响噪音,使其达到文字生成图片效果
+ checkpoint 是一种微调模型,和sd基础模型训练后的带有独特风格的模型
+ dreambooth 是一个深度学习模型,用来微调现有的文声图模型,google在2022年研发,原理是用指定的3~8张图片进行针对性训练
+ [loar](loar.md) 是微调模型,可以用dreambooth来训练,主要是任务特征的训练,画风训练,基本原理是输入一组特定的风格的照片,从而生成一些特定的 **描述词和标签**,简单说通过特定的描述词可以影响最后出图效果,类似加滤镜
+ Embedding
+ Hypernetwork

主要有三个部分构成
1. VAE
2. U-NET
3. CLIP


+ 大模型(主模型)
	+ [VAE](VAE.md) i.e. 简单理解为滤镜,加深细节
+ 小模型(微调模型)
	+ [loar](loar.md)
	+ Embedding
	+ Hypernetwork
	+ dreambooth
