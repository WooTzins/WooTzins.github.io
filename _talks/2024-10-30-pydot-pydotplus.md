---
title: "DeBug: pydot failed to call graphviz"
collection: talks
type: "DeBug"
permalink: /talks/2024-10-30-pydot-pydotplus
date: 2024-10-30
location: "Shanghai, China"

---

一般情况下，遇到`pydot failed to call graphviz`, `please pip install pydot or graphviz`这类问题问题的解决方案：\\

### 方案 ①
`pip uninstall pydot` \\
`pip install pydotplus` \\

### 方案 ②
如果上述方案不可行，再使用该方案, \\

找到当前环境下 `pydotplus` 包的存储位置，将包名更改为 `pydot` (会有两个文件包，`pydotplus` 和 `pydotplus-2.0.2.dist-info` , 只要修改前一个包名就可以了). \\

例如：我的存储位置在 `D:\ProgramData\Anaconda3\Lib\site-packages\pydotplus` , 修改为 `D:\ProgramData\Anaconda3\Lib\site-packages\pydot`. \\

再打开 `pydot` 文件夹中的 parser.py文件，将 `import pydotplus` 改成 `import pydot`. \\

紧接着，打开 `pydot` 文件夹中的 `graphviz.py` 文件，找到 `find_graphviz()` 函数。将 `#Method 3 (Windows only)` 这行之后的代码替换为下列代码:

```python
# Method 3 (Windows only)
#
if os.sys.platform == 'win32':
    # Try and work out the equivalent of "C:\Program Files" on this
    # machine (might be on drive D:, or in a different language)
    #
    if False:  # os.environ.has_key('PROGRAMFILES'):
        # Note, we could also use the win32api to get this
        # information, but win32api may not be installed.
        path = os.path.join(os.environ['PROGRAMFILES'], 'ATT', 'GraphViz', 'bin')
    else:
        # Just in case, try the default...
        path = r"D:\Graphviz\bin"
    progs = __find_executables(path)
 
    if progs is not None:
        # print "Used default install location"
        return progs
 
for path in (
        '/usr/bin', '/usr/local/bin',
        '/opt/bin', '/sw/bin', '/usr/share',
        '/Applications/Graphviz.app/Contents/MacOS/'):
    progs = __find_executables(path)
 
    if progs is not None:
        # print "Used path"
        return progs
# Failed to find GraphViz
#
 
return None
```
