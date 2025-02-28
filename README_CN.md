![CogDL](docs/source/_static/cogdl-logo.png)
===

[![PyPI Latest Release](https://badge.fury.io/py/cogdl.svg)](https://pypi.org/project/cogdl/)
[![Build Status](https://travis-ci.org/THUDM/cogdl.svg?branch=master)](https://travis-ci.org/THUDM/cogdl)
[![Documentation Status](https://readthedocs.org/projects/cogdl/badge/?version=latest)](https://cogdl.readthedocs.io/en/latest/?badge=latest)
[![Downloads](https://pepy.tech/badge/cogdl)](https://pepy.tech/project/cogdl)
[![Coverage Status](https://coveralls.io/repos/github/THUDM/cogdl/badge.svg?branch=master)](https://coveralls.io/github/THUDM/cogdl?branch=master)
[![License](https://img.shields.io/github/license/thudm/cogdl)](https://github.com/THUDM/cogdl/blob/master/LICENSE)
[![Code Style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/ambv/black)

**[主页](https://cogdl.ai/zh)** | **[论文](https://arxiv.org/abs/2103.00959)** | **[100篇GNN论文](./gnn_papers.md)** | **[排行榜](./results.md)** | **[文档](https://cogdl.readthedocs.io)** | **[数据集](./cogdl/datasets/README.md)** | **[加入我们的Slack](https://join.slack.com/t/cogdl/shared_invite/zt-b9b4a49j-2aMB035qZKxvjV4vqf0hEg)** | **[English](./README.md)**

CogDL是一款图深度学习工具包，基于[PyTorch](https://github.com/pytorch/pytorch)框架。CogDL允许研究人员和开发人员可以轻松地训练和比较基线算法或自定义模型，以进行结点分类，链接预测，图分类，社区发现等基于图结构的任务。 它提供了许多流行模型的实现，包括：非图神经网络算法例如Deepwalk、LINE、Node2vec、NetMF、ProNE、methpath2vec、PTE、graph2vec、DGK等；图神经网络算法例如GCN、GAT、GraphSAGE、FastGCN、GTN、HAN、GIN、DiffPool等。它也提供了一些下游任务，包括结点分类（分为是否具有节点属性），链接预测（分为同构和异构），图分类（分有监督和⽆监督）以及为这些任务构建各种算法效果的排行榜。

CogDL的特性包括：

- 高效性：CogDL支持使用优化好的算子来加速GNN模型的训练。
- 易用性：CogDL提供了非常易用的API来在给定的模型和数据集上运行实验。
- 扩展性：用户可以基于CogDL已有的框架来扩展新的数据集、模型。

## ❗ 最新

- 最新的 **v0.5.3 release** 支持混合精度(fp16)训练，提供了[Jittor](https://github.com/Jittor/jittor)的初步支持（见[example](https://github.com/THUDM/cogdl/blob/master/examples/jittor/gcn.py)）。这个版本更新了文档中的使用教程，修复了一部分数据集的下载链接，修复了某些算子在不同环境下可能的问题。

- 最新的 **v0.5.2 release** 给ogbn-products数据集添加了GNN样例，更新了geom数据集。这个版本同时修复了一些潜在的问题，包括设置不同device，使用cpu进行预测等。

- 最新的 **v0.5.1 release** 添加了一些高效的算子，包括cpu版本的SpMM和cuda版本的scatter_max。这个版本同时增加了很多用于节点分类的[数据集](./cogdl/datasets/rd2cd_data.py)。 🎉

- 最新的 **v0.5.0 release** 为图神经网络的训练设计了一套统一的流程. 这个版本去除了原先的`Task`类，引入了`DataWrapper`来准备training/validation/test过程中所需的数据，引入了`ModelWrapper`来定义模型training/validation/test的步骤. 🎉

<details>
<summary>
历史
</summary>
<br/>

- 最新的 **v0.4.1 release** 增加了深层GNN的实现和推荐任务。这个版本同时提供了新的一些pipeline用于直接获取图表示和搭建推荐应用。欢迎大家参加我们在KDD 2021上的tutorial，时间是8月14号上午10:30 - 12:00（北京时间）。 更多的内容可以查看 https://kdd2021graph.github.io/. 🎉

- 最新的 **v0.4.0版本** 重构了底层的数据存储（从`Data`类变为`Graph`类），并且提供了更多快速的算子来加速图神经网络的训练。这个版本还包含了很多图自监督学习的算法。同时，我们很高兴地宣布我们将在8月份的KDD 2021会议上给一个CogDL相关的tutorial。具体信息请参见[这个链接](https://kdd2021graph.github.io/). 🎉

- CogDL支持图神经网络模型使用混合专家模块（Mixture of Experts, MoE）。 你可以安装[FastMoE](https://github.com/laekov/fastmoe)然后在CogDL中尝试 **[MoE GCN](./cogdl/models/nn/moe_gcn.py)** 模型!

- 最新的 **v0.3.0版本** 提供了快速的稀疏矩阵乘操作来加速图神经网络模型的训练。我们在arXiv上发布了 **[CogDL paper](https://arxiv.org/abs/2103.00959)** 的初版. 你可以加入[我们的slack](https://join.slack.com/t/cogdl/shared_invite/zt-b9b4a49j-2aMB035qZKxvjV4vqf0hEg)来讨论CogDL相关的内容。🎉

- 最新的 **v0.2.0版本** 包含了非常易用的`experiment`和`pipeline`接口，其中`experiment`接口还支持超参搜索。这个版本还提供了`OAGBert`模型的接口（`OAGBert`是我们实验室推出的在大规模学术语料下训练的模型）。这个版本的很多内容是由开源社区的小伙伴们提供的，感谢大家的支持！🎉

- 最新的 **v0.1.2版本** 包括了预训练任务、各种使用样例、OGB数据集、知识图谱表示学习算法和一些图神经网络模型。CogDL的测试覆盖率增加至80%。正在开发和测试一些新的API，比如`Trainer`和`Sampler`。

- 最新的 **v0.1.1版本** 包括了知识图谱链接预测任务、很多前沿的模型，支持使用`optuna`进行超参搜索。我们同时发布了一篇[推送](https://mp.weixin.qq.com/s/IUh-ctQwtSXGvdTij5eDDg)来介绍CogDL。

</details>

## 安装说明

### 系统配置要求

- Python 版本 >= 3.7
- PyTorch 版本 >= 1.7.1

请根据如下链接来安装PyTorch (https://github.com/pytorch/pytorch#installation)。

PyTorch安装好之后，cogdl能够直接通过pip来安装：
```bash
pip install cogdl
```

通过如下指令来从github源来安装：

```bash
pip install git+https://github.com/thudm/cogdl.git
```

或者先将CogDL下载下来然后通过以下指令安装：

```bash
git clone git@github.com:THUDM/cogdl.git
cd cogdl
pip install -e .
```

## 使用说明

### API用法

您可以通过CogDL API进行各种实验，尤其是`experiment`。[quick_start.py](https://github.com/THUDM/cogdl/tree/master/examples/quick_start.py)这是一个快速入门的代码。您也可以使用自己的数据集和模型进行实验。[examples/](https://github.com/THUDM/cogdl/tree/master/examples/) 文件夹里提供了一些例子。

```python
from cogdl import experiment

# basic usage
experiment(dataset="cora", model="gcn")

# set other hyper-parameters
experiment(dataset="cora", model="gcn", hidden_size=32, epochs=200)

# run over multiple models on different seeds
experiment(dataset="cora", model=["gcn", "gat"], seed=[1, 2])

# automl usage
def search_space(trial):
    return {
        "lr": trial.suggest_categorical("lr", [1e-3, 5e-3, 1e-2]),
        "hidden_size": trial.suggest_categorical("hidden_size", [32, 64, 128]),
        "dropout": trial.suggest_uniform("dropout", 0.5, 0.8),
    }

experiment(dataset="cora", model="gcn", seed=[1, 2], search_space=search_space)
```

您也可以通过`pipeline`接口来跑一些有趣的应用。下面这个例子能够在[pipeline.py](https://github.com/THUDM/cogdl/tree/master/examples/pipeline.py)文件中找到。

```python
from cogdl import pipeline

# load OAGBert model and perform inference
oagbert = pipeline("oagbert")
outputs = oagbert(["CogDL is developed by KEG, Tsinghua.", "OAGBert is developed by KEG, Tsinghua."])
```

有关OAGBert更多的用法可以参见[这里](./cogdl/oag/README.md).

### 命令行
基本用法可以使用 `python train.py --dataset example_dataset --model example_model` 来在 `example_data` 上运行 `example_model`。

- --dataset, 运行的数据集名称，可以是以空格分隔开的数据集名称的列表,现在支持的数据集包括 cora, citeseer, pumbed, ppi, wikipedia, blogcatalog, dblp, flickr等。
- --model, 运行的模型名称,可以是个列表，支持的模型包括 gcn, gat, deepwalk, node2vec, hope, grarep, netmf, netsmf, prone等。

如果你想在 Cora 数据集上运行 GCN 和 GAT 模型并且设置5个不同的随机种子，你可以使用如下的命令

```bash
python scripts/train.py --dataset cora --model gcn gat --seed 0 1 2 3 4
```

预计得到的结果如下：

| Variant          | test_acc       | val_acc        |
|------------------|----------------|----------------|
| ('cora', 'gcn')  | 0.8050±0.0047  | 0.7940±0.0063  |
| ('cora', 'gat')  | 0.8234±0.0042  | 0.8088±0.0016  |

如果您在我们的工具包或自定义步骤中遇到任何困难，请随时提出一个github issue或发表评论。您可以在24小时内得到答复。

## ❗ 常见的问答

<details>
<summary>
如何给CogDL贡献代码？
</summary>
<br/>

如果您有一个性能优秀的模型，并愿意在我们的工具包中实现它，以帮助更多的人，您可以[开启一个issue](https://github.com/THUDM/cogdl/issues)然后创建一个pull request，详细信息可见[该页面](https://help.github.com/en/articles/creating-a-pull-request)。

在提交修改之前，请先运行`pre-commit install`来设置检查代码格式(`black`)和风格(`flake8`)的钩子，然后`pre-commit`会在执行`git commit`的时候自动运行。关于`pre-commit`的详细信息请参考[这里](https://pre-commit.com/)。
</details>

<details>
<summary>
如何启用快速的图神经网络的训练方式？
</summary>
<br/>
CogDL提供了一种快速的稀疏矩阵乘的操作（[GE-SpMM](https://arxiv.org/abs/2007.03179)）来加速图神经网络模型在GPU上的训练效率。
如果这个特性在当前环境下可用的话，它会自动开启。
需要注意的是这个特性仍在测试阶段，可能在某些CUDA版本下无法正常使用。
</details>

<details>
<summary>
如何使用多个 GPU 同时进行多组实验？
</summary>
<br/>
如果你想使用多个 GPU 同时在 Cora 数据集上运行 GCN 和 GAT 模型，可以使用如下指令:

```bash
$ python scripts/train.py --dataset cora --model gcn gat --devices 0 1 --seed 0 1 2 3 4
```

预计得到的结果如下:

| Variant         | Acc           |
| --------------- | ------------- |
| ('cora', 'gcn') | 0.8236±0.0033 |
| ('cora', 'gat') | 0.8262±0.0032 |
</details>

<details>
<summary>
如何使用其他图深度学习库中的模型？
</summary>
<br/>
如何你对其他图深度学习库（比如PyTorch Geometric）比较熟悉，你可以基于这些库的模块来在CogDL里实现相关模型。
你可以通过下述的指南来安装相应的库，例如PyTorch Geometric (https://github.com/rusty1s/pytorch_geometric/#installation)。
对于如何使用PyG的模块来实现模型，你可以在示例中找到一些参考：[examples/pyg](https://github.com/THUDM/cogdl/tree/master/examples/pyg/)。
</details>

## CogDL团队
CogDL是由[清华大学, 浙江大学, 北京智源, 阿里达摩院, 智谱.AI](https://cogdl.ai/zh/about/)开发并维护。

CogDL核心开发团队可以通过[cogdlteam@gmail.com](mailto:cogdlteam@gmail.com)这个邮箱来联系。

## 引用CogDL

如果你觉得我们的代码或结果对你的研究有所帮助，请引用[CogDL论文](https://arxiv.org/abs/2103.00959)。

```
@article{cen2021cogdl,
    title={CogDL: A Toolkit for Deep Learning on Graphs},
    author={Yukuo Cen and Zhenyu Hou and Yan Wang and Qibin Chen and Yizhen Luo and Zhongming Yu and Hengrui Zhang and Xingcheng Yao and Aohan Zeng and Shiguang Guo and Yuxiao Dong and Yang Yang and Peng Zhang and Guohao Dai and Yu Wang and Chang Zhou and Hongxia Yang and Jie Tang},
    journal={arXiv preprint arXiv:2103.00959},
    year={2021}
}
```
