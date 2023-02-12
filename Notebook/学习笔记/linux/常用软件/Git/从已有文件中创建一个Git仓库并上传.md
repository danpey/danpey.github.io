# 从已有文件中创建一个Git仓库并上传

例如一个仓库名为vnotebook的gitee仓库：

``` bash
# 进入要创建git仓库的已有文件下
cd vnotebook
# 初始化git仓库
git init
# 添加当前路径下的所有文件
git add .
# 提交仓库
git commit -m "first commit"
# 将仓库与远程仓库关联
git remote add origin https://gitee.com/danpe/vnotebook.git
# 上传至远程主仓库
git push -u origin master
```

