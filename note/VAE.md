### 定义

VAE包括Encoder编码器和Decoder解码器，用于图像从像素空间到潜空间的转换，或者叫降维或升维，由于用于降维的VAE Encoder 只在训练模型的阶段使用，推理过程（图像生成）只需要VAE Decoder解码器就ok了，而网上常见的VAE文件，就是对这个VAE Decoder解码器的微调改进版本，用于解决角色面部眼睛等细节方面的问题。
