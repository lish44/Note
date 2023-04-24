### ControlNet

参数说明

<div style="text-align: left; font-size: 25px;">
Enable：启用 ControlNet

Low VRAM：低显存模式优化，建议 8G 显存以下开启

Guess mode：猜测模式，可以不设置提示词，自动生成图片

Preprocessor：选择预处理器，主要有 OpenPose、Canny、HED、Scribble、Mlsd、Seg、Normal Map、Depth

Model：ControlNet 模型，模型选择要与预处理器对应

Weight：权重影响，使用 ControlNet 生成图片的权重占比影响
</div>


<div style="text-align: left; font-size: 25px;">
Guidance strength(T)：引导强度，值为 1 时，代表每迭代 1 步就会被 ControlNet 引导 1 次

Annotator resolution：数值越高，预处理图像越精细

Canny low/high threshold：控制最低和最高采样深度

Resize mode：图像大小模式，默认选择缩放至合适

Canvas width/height：画布宽高

Create blank canvas：创建空白画布

Preview annotator result：预览注释器结果，得到一张 ControlNet 模型提取的特征图片

Hide annotator result：隐藏预览图像窗口
</div>



预处理器

就是把图片通过一些算法模型输出成需要的贴图-> 如线框图,法线贴图等


![pic](https://raw.githubusercontent.com/lish44/pic/main/res/202304241142990.png)

[link](https://github.com/lllyasviel/ControlNet-v1-1-nightly) 

预处理器位置: `extensions/sd-webui-controlnet/annotator/` 


ControlNet插件视频介绍
<iframe src="//player.bilibili.com/player.html?aid=439259217&bvid=BV1vL411X7U9&cid=1078074179&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

[最新模型](https://github.com/lllyasviel/ControlNet-v1-1-nightly) 




[网站示意图](https://www.uisdc.com/stable-diffusion-2) 

[网站示意图知乎](https://zhuanlan.zhihu.com/p/616898673) 
