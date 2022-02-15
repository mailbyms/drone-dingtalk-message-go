

# 注意：项目因不支持 windows 编译成 docker 镜像，已废弃，改成自实现的 Java 项目 https://github.com/mailbyms/drone-dingtalk-message

### 修改说明
代码来自 [lddsb/drone-dingtalk-message](https://github.com/lddsb/drone-dingtalk-message) 


根据项目需要，修改了 markdown 消息的模板  
- 标题颜色：成功和失败分别用绿色和红色区分
- 标题中的 repo 改成 full_repo  

![image](https://user-images.githubusercontent.com/16809751/121153678-d891da00-c878-11eb-9494-da584f43d075.png)


### 使用说明
添加一个`step`到你的`.drone.yml`中，下面是例子：

```yaml
steps:
...
  - name: 发送钉钉消息
    image: mailbyms/drone-dingtalk-message
    pull: if-not-exists
    settings:
      token:
        from_secret: dingtalk_token
      type: markdown
    when:
      status: [failure, success]
```

### 参数说明
`dingtalk_token`机器的 access_token，必填

PC 版钉钉，点击主界面左上角的用户图像 -> `机器人管理` -> `自定义`，填写相关信息，钉钉会提示 webhook 的地址，如：`
https://oapi.dingtalk.com/robot/send?access_token=aabbccddeewf`  
其中，此 `access_token` 参数就对应 上面的 `dingtalk_token`  
![image](https://user-images.githubusercontent.com/16809751/121153859-02e39780-c879-11eb-9ae5-ded0ddbd82e5.png)

### 开发注意
钉钉的 markdown 消息，只支持如下[语法](https://developers.dingtalk.com/document/app/develop-enterprise-internal-robots/title-mno-3qd-5f9)：
```
标题
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
 
引用
> A man who stands for nothing will fall for anything.
 
文字加粗、斜体
**bold**
*italic*
 
链接
[this is a link](https://www.dingtalk.com/)
 
图片
![](http://name.com/pic.jpg)
 
无序列表
- item1
- item2
 
有序列表
1. item1
2. item2
```

### 本地调试
修改本 github 的 docker-compose.yml 文件里面的参数，使用 `docker-compose up` 即可发送消息：  
```
PLUGIN_TOKEN：设置为上面 access_token 的值
DRONE_BUILD_STATUS：设置为 failure 或者 success
```
