# 十七、Node.js

### Windows下安装node.js <a id="windows&#x4E0B;&#x5B89;&#x88C5;nodejs"></a>

[https://nodejs.org/en/download/](https://nodejs.org/en/download/) 下载 Windows Installer \(.msi\) 的 64位版本，一般用LTS版本即可。

{% hint style="danger" %}
 坑：安装目录千万不要有空格——哭到无力 ┭┮﹏┭┮
{% endhint %}

### Linux下安装node.js <a id="linux&#x4E0B;&#x5B89;&#x88C5;nodejs"></a>

下载地址: [https://nodejs.org/en/](https://nodejs.org/en/)

下载安装，将下载下来的 node-v12.16.1.tar.gz 文件解压缩，然后将文件复制到 /opt 目录下：

```bash
# 1.下载安装包
wget https://nodejs.org/dist/v12.17.0/node-v12.16.1-linux-x64.tar.xz
# 2.解压
tar zxvf node-v12.16.1.tar.gz
# 3.移动到指定安装目录，并重命名为nodejs（好记）
sudo mv node-v8.9.1-linux-x64 /opt/nodejs
```

 配置环境变量，打开 /etc/profile, 添加下来内容,将 `/opt/nodejs/bin` 加入PATH 路径：

```
vi /etc/profile

export NODE_HOME=/opt/nodejs
export PATH=$NODE_HOME/bin:$PATH

source /etc/profile  # 使配置生效
```

建立软连接：

```bash
ln -s /opt/nodejs/bin/npm /usr/local/bin/
ln -s /opt/nodejs/bin/node /usr/local/bin/
```

检查安装是否成功：

```bash
node -v
npm --version
```

### 配置淘宝源

默 认安装之后，nodejs使用的时官方的默认仓库 `https://registry.npmjs.org/`，这样不仅仅下载速度慢，而且有时会出现校验和报错。

指定国内仓库:

1. 通过config命令

   ```text
   npm config set registry https://registry.npm.taobao.org
   npm info underscore （如果上面配置正确这个命令会有字符串response）
   # 查看配置：
   npm config get registry 
   ```

2. 在npm命令行指定

   ```text
    npm --registry https://registry.npm.taobao.org info underscore
   ```

3. 修改 ~/.npmrc

   编辑这个文件，如果没有则添加，加入内容：

   ```text
    registry = https://registry.npm.taobao.org
   ```

{% hint style="info" %}
 建议第三种，不用每次都设置。
{% endhint %}

### 配置全局包存放路径

在安装目录下新建两个文件夹，用于存放全局包和缓存：

node\_global  
node\_cache

配置方式（Linux 和Window通用）：

```bash
# 可以通过CMD指令npm root -g查看：
C:\Users\XXX>npm root -g
C:\Users\XXX\AppData\Roaming\npm\node_modules
# 或者通过如下命令查询：
npm config get prefix
npm config get cache
 
# 修改路径：
npm config set prefix "E:\Programs\nodejs\node_global"
npm config set cache "E:\Programs\nodejs\node_cache"
# 或者在nodejs的安装目录中找到node_modules\npm\.npmrc文件，修改如下：
prefix =E:\Programs\nodejs\node_global
cache = E:\node\E:\Programs\nodejs\node_cache
```

{% hint style="info" %}
 **环境变量：**

* 添加变量NODE\_PATH： E:\Programs\nodejs
* 编辑变量Path，增加路径： %NODE\_PATH%\node\_modules %NODE\_PATH%\node\_global
{% endhint %}

## nodejs模块命令 <a id="nodejs%E6%A8%A1%E5%9D%97%E5%91%BD%E4%BB%A4%3A"></a>

```bash
npm install <input_name>       # 本地安装 模块安装到当前命令行所在目录
npm install <input_name> -g    # 全局安装 模块安装到全局目录
xnpm uninstall -g <input_name> # 卸载模块
npm config set prefix "全局目录路径"  # 设置全局目录路径
npm config get prefix "全局目录"     # 获取当前设置全局目录
npm config set cache "缓存目录路径"   # 设置缓存目录路径
npm config get cache "缓存目录路径"   # 获取当前设置缓存目录
npm cache clean -f  # 清理npm缓存
npm install -g n    # 安装最新版本的Node helper
```



