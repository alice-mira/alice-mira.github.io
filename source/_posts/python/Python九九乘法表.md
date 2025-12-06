---
title: Python九九乘法表
tags: [后端,python]
date: 2025-12-06 06:18:08
---

# Python九九乘法表

```python
# 九九乘法表打印程序

# 外层循环控制行数（1-9）
for i in range(1, 10):
    # 内层循环控制列数（1-i）
    for j in range(1, i+1):
        # 使用f-string格式化输出，保持对齐
        print(f"{j} × {i} = {i*j:2}", end="  ")
    # 每行结束后换行
    print()
```

程序说明：
1. 外层循环变量i表示乘法表的行数（1-9）
2. 内层循环变量j表示每行的列数（1到当前行数i）
3. 格式化输出：
   - `{j}`表示乘数
   - [`{i}`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.i.md)表示被乘数
   - [`{i*j:2}`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.i.md)表示乘积，:2表示占2位右对齐
4. `end="  "`让每次打印不换行，用两个空格分隔
5. 内层循环结束后print()实现换行

输出示例：
1 × 1 =  1  
1 × 2 =  2  2 × 2 =  4  
1 × 3 =  3  2 × 3 =  6  3 × 3 =  9  
...
1 × 9 =  9  2 × 9 = 18  3 × 9 = 27  ...  9 × 9 = 81

进阶应用：
1. 可以修改为右对齐格式：[`print(f"{i*j:>2}", end=" ")`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md)
2. 可以添加行号：[`print(f"第{i}行:", end=" ")`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md)
3. 可以输出为HTML表格格式，用于网页展示