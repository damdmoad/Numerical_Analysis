# 安装 latexmk（如果未安装）
sudo apt install latexmk

# 一键编译
latexmk -xelatex main.tex

# 清理中间文件
latexmk -c main.tex    # 保留 PDF
latexmk -C main.tex    # 删除所有（包括 PDF）

# 现在可以使用
lmk Chapter1.tex

# 可参考的项目结构
my-paper/
├── main.tex          # LaTeX 主文档
├── refs.bib          # 参考文献数据库
├── figures/          # 存放图片
│   └── example.pdf   # 示例图片（可用任何格式：.png, .jpg, .pdf）
└── notes.md          # Markdown 写作笔记（可选）

latexmk -c Chapter1.tex    
latexmk -xelatex Chapter1.tex    # 编译



@book{ZQH_NPDE2025,
  author = {Zhang Qinghai},
  title = {Notes on Numerical Analysis and Numerical Methods for Differential Equations},
  year = {2025
}