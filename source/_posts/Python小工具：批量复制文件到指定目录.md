---
title: Python小工具：批量复制文件到指定目录
date: 2022-05-07 16:19:43
tags: Tools
categories: Python
---
### 从指定目录批量复制特定类型文件到指定目录

<!--more-->

```Python
import os
from shutil import copy

def TraversalDir(path):
    result = []
    for file in os.listdir(path):
        file_path = os.path.join(path,file)
        if os.path.isdir(file_path):
            result += TraversalDir(file_path)
        if os.path.isfile(file_path):
            result.append(file_path)
    return result

root = input('请输入要遍历的目录：')

files = TraversalDir(root)

output_dir = input('请输入要保存的新目录：')
if not os.path.exists(output_dir):
    os.makedirs(output_dir)

for file in files:

    _,ext = os.path.splitext(file)
    if ext == '.pdf' or ext == '.html':  #指定要复制的文件类型
        copy(file,output_dir)

print("复制结束")

```