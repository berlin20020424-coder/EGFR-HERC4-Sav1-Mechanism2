# 🚀 Diabetic Retinopathy Analysis: EGFR-HERC4-Sav1 Axis

本项目旨在探讨在糖尿病视网膜病变（DR）过程中，**EGFR-HERC4-Sav1 轴**的表达演变及其与组织纤维化（Fibrosis）的相关性。分析流程整合了 **Bulk RNA-seq**、**scRNA-seq** 以及实验验证数据（**qPCR**）。

---

## 📊 分析流程概览

### 1. Bulk RNA-seq 表达趋势分析 (GEO: GSE313176)

通过对不同时间点（1M, 3M, 6M）的糖尿病鼠与正常鼠视网膜数据进行差异分析，揭示核心基因的表达演变。

* **标准化方法**：DESeq2 (Size Factors normalization)
* **ID 转换**：使用 `org.Mm.eg.db` 将 Ensembl ID 转换为 Gene Symbol。
* **可视化**：展示 EGFR, HERC4, Sav1 在不同疾病阶段的动态趋势。

### 2. 轴系相关性与纤维化研究

重点分析 6M（晚期）样本，探索目标轴系基因与经典纤维化标志物（*Fn1, Col1a1, Acta2*）的相关性。

* **统计学方法**：Pearson 相关系数。
* **可视化**：相关性热图 (`ggcorrplot`) 与 线性回归图 (`ggpubr`)。

### 3. 单细胞转录组验证 (scRNA-seq)

利用单细胞测序数据精准定位 RPE 细胞亚群，验证目标基因在特定细胞类型中的表达改变。

* **流程**：Seurat 整合 -> 降维聚类 (UMAP) -> RPE 亚群提取。
* **指标**：通过 `VlnPlot` 对比 Control 与 STZ 组的表达强度。

### 4. 体外实验验证 (qPCR)

对过表达（Overexpression）实验数据进行可视化，验证质粒转染效率。

* **特色**：使用 `ggbreak` 处理高动态范围的表达量数据（过表达倍数过大时的 Y 轴截断处理）。

---

## 🛠️ 环境要求

确保你的 R 环境中安装了以下核心包：

```r
# 生物信息核心包
BiocManager::install(c("DESeq2", "org.Mm.eg.db", "Seurat"))

# 绘图与数据处理
install.packages(c("tidyverse", "ggpubr", "ggcorrplot", "ggbreak"))

```

---

## 📂 项目结构

```text
├── data/               # 存放从 GEO 下载的原始 txt.gz 和 mtx 文件
├── scripts/            # 分析脚本 (Bulk_analysis.R, SingleCell_analysis.R)
├── figures/            # 导出的 PDF/PNG 结果图
└── README.md           # 项目说明

```

---

## 📈 核心结果展示

<img width="403" height="275" alt="EGFR-HERC4-SAV1 Axis Trend" src="https://github.com/user-attachments/assets/53c1f4d5-773f-4f0f-9718-89e6b747f60c" />
<img width="403" height="275" alt="Rplot" src="https://github.com/user-attachments/assets/32b5ac6b-9aa5-4932-aebc-3d56688a9f65" />
<img width="403" height="275" alt="Correlation" src="https://github.com/user-attachments/assets/586c3542-b7f8-4de0-8113-c384731a16c8" />
<img <img width="403" height="275" alt="Corelation2" src="https://github.com/user-attachments/assets/365c0d20-6c10-45d7-8aa0-dedf5bae9b95" />
width="403" height="275" alt="Rplot01" src="https://github.com/user-attachments/assets/fe27fe90-9ad7-4869-806b-9b970f0e1ca8" />


---
## 📝 使用说明

1. **数据准备**：将 GSE313176 的 RAW 文件解压至 `E:/GSE313176_RAW`。
2. **运行脚本**：按照 `Bulk -> Correlation -> SingleCell -> qPCR` 的顺序执行代码。
3. **注意**：在单细胞分析步骤中，请根据 `DimPlot` 结果确认 RPE 所在的 Cluster 编号（默认为 5）。

---

