1. 确认项目没有bug
2. 用'pip freeze &gt; requiements.txt'将当前环境的包导出到'requirements.txt'文件中，方便在布署的时候安装
3. 将项目上传到服务器上的'/srv/'目录下。这里以'git'的形式为例
   * git init
   * git remote add origin xxx.git
   * git pull origin master --allow-unrelated-histories
   * git add
   * git commit -m "first commit"
   * git push origin master



