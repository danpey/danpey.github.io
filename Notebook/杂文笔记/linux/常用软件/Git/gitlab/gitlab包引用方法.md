# gitlab包引用方法
## 基础知识/工具

```
powershell的脚本编写
nuget批处理命令
nuget package explorer 打包文件生成工具
```

## 创建一个新的仪器库包流程

### 创建符合包名称的仓库

```
创建属于eol_package_group的仓库，仓库名为：Device_M88XX
```

### 找到原有的或新建的仪器封装库项目

```
新建一个符合命名规则的Solution
拷贝原来库的project到新建仓库目录
目录结构可参考《Device_GPD2303S》
拷贝《Device_GPD2303S》中的yml（GITLAB自动集成的脚本文件）、Device_GPD2303S.nuspec、readme
将Device_GPD2303S.nuspec重命名为Device_GPD2303S.nuspec
```

### 添加nuget源并引用对应的依赖库

```
添加nuget包引用com_device_base的库
```

### 使用nuget package explorer修改Device_M88XX.nuspec

#### 先确认当前solution的框架版本

#### 确认当前solution依赖的nuget包及其版本

```
在prject目录中的packages.config中查看
```

#### 修改并添加framework文件夹以及对应的dll文件

#### 保存metadata到Device_M88XX.nuspec

#### 需要修改file标签下文件的路径

#### 可以使用powershell脚本测试打包是否成功

#### 修改yml文件中PROJECT_ID以及SLN_NAME

#### 在gitlab的项目中点击代码->标签

```
添加新的版本标签
注意标签命名目前的规则为v1.0.0或者v*.*.*
```

#### 查看结果

```
1、构建->流水线，可以查看创建标签后的流水线作业是否成功
2、部署->发布；部署->软件包库，是否成功发布包和锁定release代码版本
```

#### 包在使用时，更新或者引用时出现更新不了，提示异常（具体根据异常情况决定），有些时候需要清空Nuget缓存，在tools->options->nuget包管理常规中，清除缓存