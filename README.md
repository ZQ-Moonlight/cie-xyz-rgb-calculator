# CIE 1931 色彩空间分析工具  
**CIE Color Space Analyzer**
## 🌊 Built with "Vibe Coding"

[![在线演示](https://img.shields.io/badge/在线试用-点我-brightgreen?style=for-the-badge&logo=github)](https://zq-moonlight.github.io/cie-xyz-rgb-calculator/)

## 项目一句话介绍

一个**纯前端（HTML + CSS + JavaScript）** 的 CIE 1931 色彩空间转换与交互分析工具，支持：

- 多白点（D65 / D50 / A / E 等）
- 多种常见 RGB 色彩空间（sRGB / Adobe RGB / Display P3 / Rec.2020 / ProPhoto 等）
- 色度适应变换（Bradford / Von Kries / XYZ Scaling / 无适应）
- 正反向转换：RGB ↔ XYZ ↔ xyY ↔ Lab ↔ LCH(ab) ↔ Luv ↔ LCH(uv) ↔ CCT
- 交互式 CIE 1931 xy 色度图（点击/拖动选点 + 色域三角 + 背景亮度渲染 + 出色域警告）
- 实时同步 / 手动计算切换 + 中英双语界面

## 核心功能一览

| 功能                          | 实现方式                  | 备注                                      |
|-------------------------------|---------------------------|-------------------------------------------|
| RGB → XYZ / XYZ → RGB         | 手动矩阵 + 转移函数       | 支持 gamma / sRGB / Rec.709 / ProPhoto 等 |
| 色度适应（Chromatic Adaptation）| Bradford / Von Kries 等   | 手动构建适应矩阵                          |
| CIE Lab / LCH(ab) / Luv / LCH(uv) | 标准公式，手动实现     | 包含非线性压缩                            |
| CCT（相关色温）               | McCamy 近似 + 逆向迭代    | 双向转换                                  |
| CIE 1931 xy 交互图            | Canvas 像素填充 + 谱轨迹  | 背景为 sRGB 最大亮度渲染，点击自动转换    |
| 出色域警告（Out of Gamut）    | 线性 RGB 是否 <0 或 >1    | 红色警告文字                              |
| 中英双语切换                  | data-zh / data-en 属性    | 一键切换                                  |
| 实时 / 手动计算模式           | checkbox 控制             | 适合调试公式                              |

## 技术栈 & 依赖

- **纯前端**：HTML5 + CSS（变量 + 现代布局） + Vanilla JavaScript
- **零外部库**：没有引入任何 color 库（如 colour-science / chroma.js），全部手动实现
- Canvas 用于 CIE 图渲染（背景预计算一次，拖动只重绘点和三角）

## 核心参考资料（强烈推荐）

几乎所有公式都直接或间接来自以下权威来源：

1. **Bruce Lindbloom 的网站**（本项目圣经）  
   - 主页：http://www.brucelindbloom.com  
   - 公式集合：http://www.brucelindbloom.com/Math.html  
   - CIE 转换器演示：http://www.brucelindbloom.com/ColorCalculator.html  
   → 大部分矩阵、转移函数、Lab/Luv/CCT 公式都直接抄自这里

2. **CIE 官方标准**  
   - CIE 1931 2° 标准观察者谱轨迹坐标（我用的精简版来自公开表格）

3. **RGB 色彩空间原色坐标**（primaries & white point）  
   - sRGB / Rec.709：IEC 61966-2-1  
   - Adobe RGB (1998)  
   - Display P3 / DCI-P3  
   - Rec.2020 (BT.2020)  
   - ProPhoto RGB (ROMM RGB)

4. **色适应变换矩阵**  
   - Bradford / Von Kries 来自 Lindbloom 和 CIE Publication 15:2004

## 已知局限 & 待优化

- CCT 计算用的是 McCamy 近似（4000 K 以下精度较好，高色温有偏差）
- 谱轨迹坐标是精简版（约 30 个点），足够平滑但不是 CIE 官方 1 nm 间隔
- 背景渲染目前固定用 sRGB（可以改成当前选中的 RGB 空间，但计算量会变大）
- 没有处理极低亮度（Y≈0）时的数值不稳定


Happy color hacking! 🌈

ZQ @ 2026
