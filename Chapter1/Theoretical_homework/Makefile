# LaTeX编译器设置
LATEX = pdflatex
BIBTEX = bibtex

# 自动检测主TeX文件（查找包含\documentclass的文件）
MAIN_TEX = $(shell grep -l '\\documentclass' *.tex | head -1)
MAIN = $(basename $(MAIN_TEX))
PDF = $(MAIN).pdf

# 如果自动检测失败，手动指定
ifeq ($(MAIN_TEX),)
    MAIN_TEX = main.tex  # 默认文件名
    MAIN = main
endif

# 中间文件扩展名（包含 latexmk 和 recorder 生成的文件）
AUX_EXTENSIONS = .aux .log .out .toc .lof .lot .bbl .blg \
                 .nav .snm .vrb .synctex.gz \
                 .fls .fdb_latexmk .run.xml .bcf

INTERMEDIATE_FILES = $(addprefix $(MAIN), $(AUX_EXTENSIONS))

# 默认目标
all: $(PDF)

# 主要编译规则
$(PDF): $(MAIN_TEX)
	@echo "第一次编译LaTeX..."
	@$(LATEX) $(MAIN_TEX)
	@if [ -f $(MAIN).aux ]; then \
		echo "编译BibTeX（如果存在参考文献）..."; \
		$(BIBTEX) $(MAIN) || true; \
	fi
	@echo "第二次编译LaTeX..."
	@$(LATEX) $(MAIN_TEX)
	@echo "第三次编译LaTeX..."
	@$(LATEX) $(MAIN_TEX)
	@echo "PDF文件生成完成: $(PDF)"

# 主要目标：编译并清理
report: $(PDF)
	@echo "清理中间文件..."
	@rm -f $(INTERMEDIATE_FILES)
	@echo "编译完成，中间文件已清理"

clean:
	@echo "清理中间文件..."
	@rm -f $(INTERMEDIATE_FILES)

distclean: clean
	@echo "清理PDF文件..."
	@rm -f $(PDF)

help:
	@echo "可用命令:"
	@echo "  make report    - 编译LaTeX并清理所有中间文件"
	@echo "  make all       - 编译LaTeX但保留中间文件"
	@echo "  make clean     - 仅清理中间文件"
	@echo "  make distclean - 清理所有生成文件"
	@echo "  检测到的主文件: $(MAIN_TEX)"

.PHONY: all report clean distclean help