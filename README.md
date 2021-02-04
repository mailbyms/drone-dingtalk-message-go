

[TOC]

### 修改说明
代码来自 [lddsb/drone-dingtalk-message](https://github.com/lddsb/drone-dingtalk-message) 


根据项目需要，修改了 markdown 消息的模板  
- 标题颜色：成功和失败分别用绿色和红色区分
- 标题中的 repo 改成 full_repo  

![image.png](https://i.loli.net/2021/02/04/5YvmTtlykrEHDQO.png)


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
其中，是 `access_token` 参数就对应 上面的 `dingtalk_token`  
![image.png](https://i.loli.net/2021/02/04/vaNUCKkqHltBVxM.png)