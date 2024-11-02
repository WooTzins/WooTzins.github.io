---
title: "VS Code: Cann't find custom package"
collection: talks
type: "DeBug"
permalink: /talks/vs_code-path_problem
date: 2024-11-02
location: "Shanghai, China"

---

在使用VS code的时候，往往会自己定义包，并在包内放入自己设定的类的 `.py` 文件，但在运行时，往往会报错：`cann't find XXXX`.
 
这类问题问题的解决方案：  

在代码的最前面输入下面这段代码
`XXX` 表示当前目录的绝对路径.
```python
import os
import sys
sys.path.append(os.path.abspath(r'XXXX'))
```


