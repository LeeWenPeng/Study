## 1  jupyter

### 1.1  jupyter 导出为其他格式文件

#### 1.1.1  方式一：借助工具 `nbconvert`

安装方式

```shell
pip install nbconvert
```

使用方式

1. 进入文件所在文件夹
2. 进行转换

   ```shell
   jupyter nbconvert --to [format] [文件名].ipynb
   ```

注意事项：

1. nbconvert 使用时，借助了其他工具，如果需要转换的格式为 pdf 或者是 html 则需要安装其他依赖
   参考文章：[安装 nbconvert（转换jupyter notebook）_蔚蓝慕的博客-CSDN博客](https://blog.csdn.net/acktomas/article/details/124980002)
