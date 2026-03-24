# OpenCode Demo 项目规范

## 项目概述

这是一个演示项目，包含一个 PDF 合并工具（基于 Python tkinter 和 PyPDF2）。

## 环境要求

- Python 3.x
- PyPDF2: `pip install PyPDF2`

## 构建与运行

### 安装依赖

```bash
pip install PyPDF2
```

### 运行应用

```bash
python merge_pdfs_gui.py
```

### 代码检查

```bash
# Python 语法检查
python -m py_compile merge_pdfs_gui.py

# 使用 flake8 检查代码风格
pip install flake8
flake8 merge_pdfs_gui.py

# 使用 black 格式化代码
pip install black
black merge_pdfs_gui.py
```

## 测试命令

由于本项目目前没有单元测试，如需添加测试：

```bash
# 安装 pytest
pip install pytest

# 运行所有测试
pytest

# 运行单个测试文件
pytest test_merge_pdfs.py

# 运行单个测试函数
pytest test_merge_pdfs.py::test_merge_two_pdfs -v
```

## 代码风格指南

### 1. 基础规范

- 使用 UTF-8 编码
- 缩进：4 空格
- 每行最大长度：100 字符
- 文件末尾保留一个换行符

### 2. 命名规范

#### 文件命名
- Python 文件：使用小写字母和下划线（snake_case）
- 示例：`merge_pdfs_gui.py`、`pdf_processor.py`

#### 变量命名
- 变量名：使用小写字母和下划线（snake_case）
- 示例：`pdf_files`、`output_file`、`merge_result`

#### 函数命名
- 函数名：使用小划线命名（snake_case），动词开头
- 示例：`merge_pdfs()`、`get_file_path()`、`validate_input()`

#### 类命名
- 类名：使用大驼峰命名（PascalCase）
- 示例：`PdfMergerApp`、`FileHandler`

#### 常量命名
- 常量：使用全大写字母和下划线
- 示例：`MAX_FILE_SIZE`、`DEFAULT_OUTPUT_DIR`

### 3. 导入规范

```python
# 标准库导入
import os
import sys
from tkinter import filedialog, messagebox

# 第三方库导入
from PyPDF2 import PdfMerger

# 本地模块导入
from .utils import helper_function
from .models import DataModel
```

导入顺序：
1. 标准库
2. 第三方库
3. 本地模块

每组之间用空行分隔。

### 4. 函数规范

```python
def function_name(param1: type, param2: type) -> return_type:
    """函数说明文字。
    
    Args:
        param1: 参数1说明
        param2: 参数2说明
    
    Returns:
        返回值说明
    
    Raises:
        ExceptionType: 异常情况说明
    """
    # 函数体
    pass
```

### 5. 类型注解

- 鼓励使用类型注解提高代码可读性
- 复杂类型使用 TypeAlias 定义
- 泛型使用 typing 模块

```python
from typing import List, Optional, Dict

def process_files(files: List[str]) -> Dict[str, bool]:
    pass
```

### 6. 错误处理

```python
try:
    # 可能会失败的操作
    result = risky_operation()
except SpecificException as e:
    # 处理特定异常
    logger.error(f"操作失败: {e}")
    raise CustomException("自定义错误信息") from e
except Exception as e:
    # 捕获其他异常
    logger.exception("未预期的错误")
    raise
```

- 优先捕获具体异常，而非通用 Exception
- 始终在异常处理中记录日志
- 使用 `from e` 保留原始异常链

### 7. 注释规范

#### 行内注释

```python
x = x + 1  # 补偿基准偏移
```

#### 函数文档

```python
def calculate_total(items: List[float]) -> float:
    """计算购物车总金额。
    
    Args:
        items: 商品价格列表
    
    Returns:
        所有商品的总金额
    
    Example:
        >>> calculate_total([10.5, 20.0, 5.5])
        36.0
    """
    return sum(items)
```

### 8. 格式化

使用 Black 自动格式化：

```bash
black .
```

或手动格式化：

```python
# 列表推导式
result = [x for x in items if x > 0]

# 字典推导式
new_dict = {k: v for k, v in old_dict.items()}

# 多行参数
def long_function(
    arg1: int,
    arg2: str,
    arg3: bool,
) -> None:
    pass
```

### 9. Git 提交规范

提交信息格式：

```
<类型>: <简短描述>

<详细描述>

<关闭的Issue>
```

类型：
- `feat`: 新功能
- `fix`: bug 修复
- `docs`: 文档更新
- `style`: 代码格式调整
- `refactor`: 重构
- `test`: 测试相关
- `chore`: 维护工作

示例：

```
feat: 添加 PDF 批量合并功能

新增支持同时选择多个 PDF 文件进行合并，
并在合并完成后显示成功提示。

关闭 #123
```

### 10. 目录结构

```
项目根目录/
├── merge_pdfs_gui.py    # 主程序
├── test.txt             # 测试文件
├── README.md            # 项目说明
├── AGENTS.md            # 智能体规范（本文件）
└── tests/               # 测试目录
    ├── __init__.py
    └── test_merge.py
```

## 智能体工作流程

1. 阅读相关文件后再修改
2. 修改前确认现有代码风格
3. 运行测试验证修改
4. 确保 lint 通过
5. 提交时遵循提交规范
