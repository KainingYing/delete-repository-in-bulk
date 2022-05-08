# 批量删除git仓库

由于经常会在github上fork一些仓库，其中许多是没有用的，当要进行删除的时候，只能够使用setting，然后输入一遍仓库名，这种方法极其繁琐。

<div align="center">
  <img src="imgs/img_1.jpg" width="600"/>
</div>


故本文采用了github中的token进行批量删除。

## step1 申请token

访问https://github.com/settings/tokens，获取delete_repo的token。

<div align="center">
  <img src="imgs/img_2.jpg" width="600"/>
</div>

## step2 制作删除仓库的列表文件

<div align="center">
  <img src="imgs/img_3.jpg" width="600"/>
</div>

## step3

在windows环境下，启动powershell

<div align="center">
  <img src="imgs/img_4.jpg" width="600"/>
</div>

输入如下指令。

```
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
get-content D:\Desktop\research\repo\del_repo\repo.txt | ForEach-Object { Invoke-WebRequest -Uri https://api.github.com/repos/$_ -Method “DELETE” -Headers @{"Authorization"="token xxx"} }


# 例如下面，这里需要替换的是repo.txt的地址以及token后面的xxx，双引号要保留
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 
get-content D:\research\delete-repository-in-bulk\repo.txt | ForEach-Object { Invoke-WebRequest -Uri https://api.github.com/repos/$_ -Method “DELETE” -Headers @{"Authorization"="token ghp_aoJDtXrLVoKteR3kkBNVyJt4txS"} }
```

其中需要注意repo的地址以及token，这些都是需要进行替换的。

<div align="center">
  <img src="imgs/img_5.jpg" width="600"/>
</div>

运行成功！