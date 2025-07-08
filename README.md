# JxLang 0.3.126
<a href="README_en.md">English</a> | 简体中文<br><br>
一个轻量级的自定义编程语言，专为简单性和交互式脚本设计而打造。基于 Python 构建，`jxlang` 提供了 REPL 环境，支持基本的编程结构，包括变量、循环、函数和库导入等功能，由于其基于多层语言，如同虚拟机中的虚拟机一般，因此该语言只适合无聊的时候玩玩，不能用于开发项目。

## 安装

### 方法一：通过 PyPI 安装
```bash
pip install jxlang
```

### 方法二：通过清华源安装（推荐国内用户使用）
```bash
pip install jxlang -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## 更新
如果您已经安装过`jxlang`了，那么您可以直接使用下面的命令更新至最新版本的`jxlang`。
```bash
pip install --upgrade jxlang==0.3.126
```
## 更新内容
<ul>
<li>新增灵活的动态结构体功能</li>
<li>优化多行输入显示效果</li>
<li>修复变量类型显示问题</li>
</ul>

## 特性

- **单行注释**：使用 `#` 进行单行注释
- **变量声明**：使用 `let` 声明变量
- **循环结构**：支持基于范围的 `for` 循环
- **输入输出**：`enter()` 用于输入，`say()` 用于输出
- **库导入**：通过 `cite` 导入 Python 库，支持别名设置
- **列表/表格结构**：创建和操作列表（`table(...)`）
- **函数支持**：定义和调用自定义函数
- **多行输入**：在 REPL 中支持多行代码输入，显示效果优化
- **动态结构体**：创建和操作灵活的数据结构
- **类型检查**：使用 `shape()` 检查变量类型
- **退出会话**：使用 `endend()` 退出当前会话
- **REPL 支持**：提供交互式环境进行快速测试

## 快速示例

### 1. 变量声明和打印
```python
let x: 5
say(x + 3)  # 输出：8
# 在给变量赋值字符串时，可以使用双引号或单引号
let a: "你好"
say(a)      # 你好
let a: '世界'
say(a)      # 世界
```

### 2. 循环
```python
(i -> 1 && 5).for(
    say(i)
    )
# 输出：1 2 3 4 5
```

### 3. 函数定义和调用
```python
func(x && y -> add):
    out x + y

say(add(5 && 3))  # 输出：8

# 多行函数定义
func(x && y -> calculate):
    let temp: x * 2
    out temp + y

say(calculate(3 && 4))  # 输出：10
```

### 4. 输入和输出
```python
let name: enter()  # 用户输入 "张三"
say("你好，" + name)  # 输出：你好，张三
```

### 5. 导入 Python 库（支持别名）
```python
cite math as m
say(m.sqrt(25))  # 输出：5.0

cite numpy as np
let a: np.array([1,2,3])
say(a)          # 输出：[1,2,3]

# 导入特定模块并设置别名
cite pandas as pd
let df: pd.DataFrame({'A': [1,2,3]})
say(df)         # 输出：包含 A 列的 DataFrame

# 使用 matplotlib 进行数据可视化
cite matplotlib.pyplot as plt
let x: np.linspace(0, 10, 100)
let y: np.sin(x)
plt.plot(x, y)
plt.title("正弦波")
plt.show()      # 显示图形
```
<p>* JxLang 只能调用已安装在 Python 环境中的库。</p>

### 6. 列表和表格操作
```python
let lst: table(1, 2, 3)
say(lst[0])       # 输出：1
say(lst)          # 输出：[1,2,3]

let tbl: table(1, 2; 3, 4)
say(tbl)          # 输出：[[1, 2], [3, 4]]

# 列表操作
push 1 -> lst     # 在列表末尾添加 1
say(lst)          # [1,2,3,1]

push tbl -> lst
say(lst)          # [1,2,3,1,[[1,2],[3,4]]]

out 1 -> lst      # 移除第一个 1 并存储在 outlist 中
say(lst)          # [2,3,[[1,2],[3,4]]]
say(lst.outlist)  # [1,1]

throw 2 -> lst    # 永久移除列表中的 2
say(lst)          # [3,[[1,2],[3,4]]]

let lst[0]: 2     # 将索引 0 处的元素替换为 2
say(lst)          # [2,[[1,2],[3,4]]]
```
<p>* JxLang 使用 n 个分号创建 n+1 维列表。</p>

### 7. 动态结构体和类型检查
```python
# 定义结构体
struct Person {
    name: string,
    age: int,
    address: string
}

# 创建结构体实例
let person: Person {
    name: "张三",
    age: 30,
    address: "北京"
}

# 创建嵌套结构体
struct Info {
    info: Person
}

let i: Info {
    info: Person {
        name: "张三",
        age: 30,
        address: "北京"
    }
}

# 访问结构体成员
say(person->name)      # 输出：张三
say(person->age)       # 输出：30
say(i->info->name)     # 输出：张三
say(i->info->age)      # 输出：30

# 动态修改结构体的值
let person->name: '李四'
let person->age: 40
say(person->name)     # 输出：李四
say(person->age)      # 输出：40
```

### 8. 查看元素类型
```python
let a: 100
let b: 'Alice'
let c: table(1,2,3)

func (i -> add):
    out i

# 显示类型
shape(a)    # 输出：int
shape(b)    # 输出：string
shape(c)    # 输出：list
shape(add)  # 输出：function

# 其余类型的元素同理使用shape方法即可查看
```

## 使用 REPL

通过以下命令启动交互式环境：
```bash
jxlang
```

多行输入示例：
```
jxlang> func(x && y -> add):
    ... out x + y
jxlang> say(add(5, 3))
8
jxlang> endend(0)  # 可以使用 0 到 9 的数字作为 endend() 的参数
Exiting with code 0
```

## 贡献

欢迎贡献代码！请 fork 本仓库并提交 pull request。  
对于重大更改，请先开 issue 讨论您的想法。

## 许可证

本项目采用 Apache 许可证。

---

祝您编码愉快！🚀 
