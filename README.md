# 批量删除git仓库

由于经常会在github上fork一些仓库，其中许多是没有用的，当要进行删除的时候，只能够使用setting，然后输入一遍仓库名，这种方法极其繁琐。

![image-20210713112108217](C:\Users\Administrator.DESKTOP-EASJP9H\AppData\Roaming\Typora\typora-user-images\image-20210713112108217.png)

故本文采用了github中的token进行批量删除。

## step1 申请token

访问https://github.com/settings/tokens，获取delete_repo的token。

![image-20210713112255812](C:\Users\Administrator.DESKTOP-EASJP9H\AppData\Roaming\Typora\typora-user-images\image-20210713112255812.png)

## step2 制作删除仓库的列表文件

![image-20210713112344220](C:\Users\Administrator.DESKTOP-EASJP9H\AppData\Roaming\Typora\typora-user-images\image-20210713112344220.png)

## step3

在windows环境下，启动powershell

![image-20210713112426236](C:\Users\Administrator.DESKTOP-EASJP9H\AppData\Roaming\Typora\typora-user-images\image-20210713112426236.png)

输入如下指令。

```
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
get-content D:\Desktop\research\repo\del_repo\repo.txt | ForEach-Object { Invoke-WebRequest -Uri https://api.github.com/repos/$_ -Method “DELETE” -Headers @{"Authorization"="token xxx"} }

```

其中需要注意repo的地址以及token，这些都是需要进行替换的。

![image-20210713112551129](C:\Users\Administrator.DESKTOP-EASJP9H\AppData\Roaming\Typora\typora-user-images\image-20210713112551129.png)

运行成功！