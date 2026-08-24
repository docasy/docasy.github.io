---
title: Transformer 与 GAN 学习笔记
date: 2026-07-31 12:00:00 +0800
categories: [学习笔记]
tags: [transformer, gan, 深度学习]
---

## Transformer

<!-- 加架构图:把图片放到 assets/img/posts/transformer-gan/ 下,然后取消下面这行注释 -->
<!-- ![Transformer 架构图](/assets/img/posts/transformer-gan/transformer-arch.png) -->

- Query 查询矩阵，Key = token 的值(应该有 apple、1 这样的转换表示)，Value = token 可能代表的含义
- QK/根号 d 维度，代表一次语义理解，除以维度防止值太大
- FFN:好像就是再跑一遍，学习到更多特征，为了稳定(需要更多解释)
- Add:残差防止梯度消失；Norm:规范化
- 多头注意力:一次上边的组合算一次注意力，多头就是多个叠加?
- 注意力掩码就是遮盖后面内容，使得训练变成利用已有的东西生成没有的东西

## Transformer 训练

- 嵌入:文本转向量
- Transformer 层:理解句子意思，捕捉语义
- 输出:预测下一个词

## GAN

- 交叉熵损失:等于正确概率的负对数，概率越小 loss 指数级暴增
- 梯度下降:不断沿着梯度反方向更新参数让 loss 下降
- 反向传播:loss 对每一层参数求导(y1=a1x+b1，y2=a2y1+b2……)，用得到的导数更新模型参数，经过每一层网络
- 正向传播:模型从高纬度到低纬度，获取高级语义，再还原成高纬度图片
- GAN 里 G 正向得到图片，D 得到分数，都是为了获取 loss 然后反向，然后更新参数
- 参数更新:θ = θ - α·∇loss/参数
  - α 学习率:太大可能得不到最优结果，太小太慢
- SGD 随机梯度下降:随机 minibatch 取训练集数据，减少计算量
