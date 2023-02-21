# centOs安装docker

### 直接上才艺，注意登录用户哈

#### 更新数据源

```
`yum update`
```

![](C:\Users\davea\AppData\Roaming\marktext\images\2023-02-21-13-56-36-image.png)

#### 安装docker

```
yum install docker
```

![](C:\Users\davea\AppData\Roaming\marktext\images\2023-02-21-13-56-46-image.png)

#### 测试docker

    systemctl status docker // 查看docker有没有启动  
    systemctl start docker // 启动 
    systemctl enable docker // 可选 增加开机启动
     docker pull hello-world // 拉取镜像
     docker run hello-world // 启动镜像  生成某个容器

![](C:\Users\davea\AppData\Roaming\marktext\images\2023-02-21-13-57-46-image.png)

只要收到docker说的hello就可以了，

这是最简单的docker安装步骤