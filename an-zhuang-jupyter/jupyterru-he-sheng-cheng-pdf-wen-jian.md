### 相关资源下载

* _Pandoc_:[http://so.csdn.net/so/search/s.do?q=pandoc&t=doc&o=&s=all&l=null](http://so.csdn.net/so/search/s.do?q=pandoc&t=doc&o=&s=all&l=null)
* _Miktex_:[https://miktex.org/](https://miktex.org/)

下载相关资源即可生成pdf文件

### 中文乱码处理

* ipython nbconvert --to latex xxx.ipynb

* 修改tex

  ```
  双击打开转换的文件在\documentclass{article}后面插入 
  \usepackage{fontspec, xunicode, xltxtra} 
  \setmainfont{Microsoft YaHei} 
  \usepackage{ctex}
  ```

  ![](/assets/jy-4.1.4.1-1.png)

* 编译tex，生成pdf

  ```
  xelatex xxx.tex
  ```



