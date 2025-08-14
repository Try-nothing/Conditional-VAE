# 📂 Conditional Variational Autoencoder (CVAE) 项目说明

🎯 项目目标

本项目实现了一个条件变分自编码器(CVAE)，用于生成可控的手写数字图像。模型通过在MNIST数据集上训练，实现了：
1. 高质量的数字图像重建
2. 基于条件标签的特定数字生成
3. 潜在空间操作与可视化

🧠 模型架构

该CVAE模型包含以下核心组件：

1. 编码器(Encoder)
   • 输入层：784像素 + 10维独热编码标签

   • 隐藏层：512 -> 256维非线性变换

   • 输出层：潜在空间的均值(μ)和对数方差(logσ²)

2. 重参数化技巧(Reparameterization Trick)
   • 使用z = μ + ε·σ实现梯度可微分

   • 其中ε ~ N(0,1)

3. 解码器(Decoder)
   • 输入层：20维潜在向量 + 10维标签

   • 隐藏层：256 -> 512维非线性变换

   • 输出层：784像素的重建图像(Sigmoid激活)

⚙️ 训练过程

模型训练包含以下关键元素：
• 损失函数：重建损失(BCE) + KL散度
  loss = BCE + KLD = 
    reconstruction_error + KL(q(z|x)||N(0,I))
  
• 优化器：Adam优化器(lr=1e-3)

• 学习率调度：ReduceLROnPlateau动态调整

• 训练循环：20个epoch，每轮记录训练/测试损失

• 可视化：每轮保存重建对比和生成样本

📊 结果可视化

项目实现了全面的可视化功能：

1. 训练监控
   • 训练/测试损失曲线

   • 逐轮重建质量对比图

2. 样本生成
   • 各epoch的条件样本生成(0-9的完整序列)

   • 随机样本生成

3. 潜在空间探索
   • 潜在向量插值动画(GIF格式)

   • 条件控制下的风格迁移

4. 额外分析
   • 原始训练样本可视化

   • 重建质量对比图

   • 学习曲线分析

🚀 运行说明

1. 依赖安装：
   pip install torch torchvision numpy matplotlib imageio tqdm
   

2. 项目结构：

   CVAE-MNIST/
   ├── results/                  # 输出目录
   │   ├── reconstructions/      # 重建对比图
   │   ├── samples/              # 生成样本
   │   └── loss_curve.png        # 损失曲线
   └── cvae_mnist.ipynb          # Jupyter Notebook
   

3. 训练命令：
   • 在Jupyter Notebook中顺序执行所有单元格

   • 训练结束后查看results目录下的输出

📈 性能分析

• 最终测试损失达到约100-120

• 在20个epoch内达到稳定重建

• 生成样本质量随训练轮次显著提升

此项目展示了条件生成模型在控制图像生成方面的强大能力，特别适用于需要指定属性生成的应用场景。
