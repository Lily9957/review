```
SSH利用SSH Key来进行前面提到的基于密钥的安全验证。
```

#### SSH-Key是什么？

```
1》SSH-Key 就是一对密钥对。【一个是公钥，一个是私钥】
2》公钥是给别人用的。私钥是给自己用的。
3》别人是谁？可以是GitLab服务器。
   自己是谁？可以是本地。
    
4》举个例子
     4.1》本地想要使用git从gitHub/gitlab上拉取代码。
     4.2》给GitHub/GitLab配置公钥，公钥就可以作为一个加密的箱子，将代码放在箱子里。
     4.3》被本地拉取到后，使用私钥将加密的箱子打开。就能拿到代码了。
     4.4》整个过程中，都没有用户名/密码在网络中传输，所以不会给他人拦截到，破解你的数据
  
5》所以，SSH-Key的直观作用，就是【让你方便的登录到 SSH 服务器，而无需输入密码】
```



**首先要保证自己在根目录下,不清楚自己的路径在哪的话，可以执行``pwd``来看看自己在哪里**

#### 1、查看是否有密钥

```
ls -al ~/.ssh
```

<img src="/Users/xyz10/Library/Application Support/typora-user-images/image-20210728142154980.png" alt="image-20210728142154980" style="zoom: 67%;" />

如果没有就新建，如果有，建议先删除以前的，再新建一个

上图所示，先前是有密钥的

#### 2、删除密钥

```
删除命令【其实就是删除.ssh这个隐藏目录目录】

rm -rf .ssh
```

<img src="/Users/xyz10/Library/Application Support/typora-user-images/image-20210728143436736.png" alt="image-20210728143436736" style="zoom:67%;" />



#### 3、新生成密钥

```
3》新生成SSH-key

ssh-keygen -t rsa
```



#### 4、查看公钥

```
cat .ssh/id_rsa.pub
```

<img src="/Users/xyz10/Library/Application Support/typora-user-images/image-20210728145058783.png" alt="image-20210728145058783" style="zoom:67%;" />

