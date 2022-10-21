[目录](README)

# Npm & Yarn

## 1. Npm 介绍

Npm 全称是 Node Package Manager , 是 Node 默认的包管理器，也是一个应用程序，用来安装和管理 Node 包.

官网 [https://npmjs.org](https://npmjs.org)

- **什么是包？**

<mark>Node.js 的包遵循 CommonJS 规范</mark>，将一组相关的模块(module) 组合在一起，形成一个完整的工具，该工具称为包.

我们电脑上的文件夹，包含了某些特定的文件，符合了某些特定的结构，就是一个包

模块：每一个 JS 文件称为模块

包：若干个 JS 文件组成包

- **一个标准的包，应该包含哪些内容？**
1. package.json ------   描述文件(包的“说明书”，必须要有！！！)

2. bin --------------------- 可执行二进制文件

3. lib ---------------------- 经过编译后的 js 代码

4. doc -------------------- 文档(说明文档、bug 修复文档，版本变更记录文档)

5. test -------------------- 单元测试，一些测试报告

**其中 package.json 必须有，其他的 bin, lib, doc, test 可以省略**

- **如何让一个普通文件夹变成一个包？**

让这个文件夹拥有一个 package.json 文件即可，且 package.json 里面的内容要合法

**执行命令：npm init**

**包的要求：不能有中文，不能有大写字母，不要以数字开头，不能与 npm 仓库上其他包同名**

- **npm 与 node 的关系？**

安装 node 后就自动安装了 npm，npm 是 node 官方出的包管理器，专门用于管理包

- **Npm 的作用**

Node 的包管理器(`npm`)，功能极其强大：通过 npm 可以对 Node 的工具包进行搜索、下载、安装、删除、上传。

借助别人写好的包，可以让我们的开发更加方便

常见的使用场景有以下 3 种：

1. 允许用户从 NPM 服务器下载别人编写的第三方包到本地使用。
2. 允许用户从 NPM 服务器下载并安装别人编写的命令行程序到本地使用。
3. 允许用户将自己编写的包上传到 NPM 服务器供别人使用。
- **Npm 的安装**

npm 不需要单独安装, 在安装 Node 的时候，会连带一起安装 npm, 可以通过以下命令在 cmd 终端检测是否成功安装：

```shell
npm -v
```

也就是 Node 安装好了，npm 自然就一起安装好了。除了默认的 npm，还有 cnpm、yarn 这些模块管理器. （npm 用的较多.）

## 2. npm 的使用

1. **使用 npm,首先执行命令 npm init 创建 package.json 文件，该文件是对当前项目的相关描述** :
   
   ```js
   {
       "name": "ryan dahl",     #包的名字
       "version": "1.0.0",        #包的版本
       "main": "index.js",        #包的入口文件
       "scripts": {               #脚本配置
           "test": "echo \"Error: no test specified\" && exit 1"
       },
       "keywords": [],            #关键字
       "author": "",              #作者
       "license": "ISC",          #版权声明，ISC相当于MIT license(版权许可证)
       "description": ""          #包的描述
   }
   ```
   
   - **注意生成的包名不能使用中文，不能有大写字母 ！！！**
   
   - 开源证书扩展阅读
     
     http://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html

2. **安装包并将该包写入到 dependencies 生产依赖中**
   
   ```shell
   npm install 包名 --save  或
   npm i 包名 -S   或
   npm i 包名
   ```
   
   备注：
   
   - 安装之前必须保证文件夹内有 package.json，且里面的内容格式合法
   
   - 局部安装完的第三方包，放在当前目录中 node_module 这个文件夹里
   
   - 安装完毕会自动产生一个 package-lock.json 里，里面缓存的是每个下载过的包的地址，目的是下次安装时速度快一些
   
   - 当安装完一个包，该包的名字会自动写入到 package.json 中的 dependencies(生产依赖)里
   
   - npm5 及之前的版本安装时要加上 -s

3. **安装包并将该包写入到 devDependencies 开发依赖中**
   
   ```shell
   npm install 包名 --save-dev  或
   npm i 包名 -D
   ```
   
   备注：**什么是生成依赖与开发依赖？**
   
   - 只在开发时才用到的库，就是开发依赖 (即程序员正在写代码的时候) ------ 例如：语法检查，压缩代码，扩展 css 前缀的包
   
   - 在生产环境中不可缺少的就是生产依赖 (即项目上线，代码写完了，部署到服务器上给客户用) ------- 例如：jQuery, bootstrap 等
   
   - 注意：某些包既属于开发依赖，又属于生产依赖 -------- 例如：jQuery

4. **全局安装**
   
   一般来说，带有指令集的包要进行全局安全，如 cnpm，yarn，webpack ，gulp 等，全局安装的包，其指令到处都能用，如果该包不带有指令，就不需要全局安装.
   
   全局命令的安装位置:
   
   ```shell
   C:\Users\用户名\AppData\Roaming\npm
   ```
   
   ```shell
   npm i 包名 -g
   ```

5. **安装依赖**
   
   根据 package.json 中的依赖声明安装工具包, 也就是安装 package.json 中声明的所有包.
   
   所有通过 npm 下载的模块(包)都会自动装到 node_modules 的目录(文件夹)里
   
   ```shell
   npm i
   npm install
   
   该命令用来安装模块到 node_modules 目录
   如果已经存在这个目录就直接用，如果目录不存在，会自动创建一个
   ```

6. **移除包**
   
   ```shell
   npm uninstall packageName
   ```

7. **更新包**
   
   ```shell
   npm update packageName
   ```

8. **用@下载指定版本：如果不指定版本，默认安装最新的**
   
   ```js
   npm install jquery@3.3.1      # 当前目录下安装jquery版本3.3.1
   npm install nodemon@2.0.7 -g  # 全局安装nodemon的版本2.0.7
   ```

9. **查看安装包信息（了解）**
   
   ```shell
   npm list         #查看本地安装包信息
   npm list -g      #查看全局安装包信息
   npm list express #查看某个安装包信息
   
   npm ls            #npm list简写
   npm ls nodemon -g #查看全局安装包nodemon的信息
   
   npm view 包名 versions  #查看远程npm仓库中某个包的所有版本信息
   npm view 包名 version   #查看npm仓库中某包的最新版本
   
   npm audit fix  #检测项目中依赖中的一些问题，并尝试修复
   ```

10. **清除缓存**
    
    有时因为停电等意外原因导致下载中断，再次安装会安装不了，这时清除一下缓存就可以解决问题
    
    ```shell
    npm cache clean --force
    ```

11. **团队开发时 Npm 使用流程**
    
    1. 从仓库中拉取仓库代码
       
       也就是远程仓库中没有 node_modules，但有 package.json，别人从远程仓库拉取到代码后可以进行下面的第 2 步
    
    2. 运行 npm install 安装所有相关依赖
       
       也就是说 node_modules 不会传给别人，所有人都可以通过 npm install 或 npm i 命令自己安装 node_modules
    
    3. 运行项目，继续开发

12. **安装模块时，选择全局安装还是局部安装？**
    
    一般都是当前项目下安装
    
    全局安装的多是 cli 工具

13. **另外备注：关于package.json里的依赖包**
    
    可以在package.json里手写添加依赖包(模块)，但手写后不会自动安装包(模块），还需要执行命令 npm install 安装模块, 但模块涉及到名称，版本号这些容易写错的细节，所以通常不建议手写，还是通过命令去安装更好.

## 3. Cnpm

cnpm 是淘宝对国外 npm 服务器的一个完整镜像版本，也就是淘宝 npm 镜像，网站地址[http://npm.taobao.org/](http://npm.taobao.org/)

<mark>cnpm 跟 npm 用法完全一致，只是在执行命令时将 npm 改为 cnpm</mark>

1. **安装命令**
   
   ```shell
   npm install -g cnpm --registry=https://registry.npmmirror.com
   ```

2. **查看版本**
   
   ```js
   cnpm - v;
   ```

3. **cpnm 和 npm 的差异**
   
   ```shell
   # 使用npm
   npm init -y  # 生成package.json
   npm instal jquery  # 会放置在json文件的依赖项中。
   
   # 使用cnpm时，-S不可以省略
   # -S 是 --save的缩写    -D 是--save-dev 的缩写
   cnpm install jquery -S  # 如果没有package.json文件，会自动创建。
   cnpm install ejs md5 -S  # 如果不声明-S那么不会放置在json文件的依赖项。
   cnpm install jwt-simple -D
   ```

4. **npm 配置镜像地址**
   
   ```shell
   //淘宝镜像
   npm config set registry https://registry.npm.taobao.org
   //官方镜像
   npm config set registry https://registry.npmjs.org
   
   查看当前镜像地址
   npm config get registry
   ```

## 4. Yarn

yarn 是 Facebook 开源的新的包管理器，可以用来代替 npm.

介绍参看 [Getting Started | Yarn](https://classic.yarnpkg.com/en/docs/getting-started)

<mark>使用 Yarn 或 Npm 没什么区别，都一样</mark>.

1. **安装 yarn**
   
   [Installation | Yarn](https://classic.yarnpkg.com/en/docs/install#windows-stable)
   
   ```shell
   npm install --global yarn
   ```

2. **相关命令**
   
   [Usage | Yarn](https://classic.yarnpkg.com/en/docs/usage)
   
   以vue为例子的各种安装命令
   
   ```js
   yarn add vue // 当前项目下安装包
   yarn global add vue // 全局安装包，注意global要在add前面，否则不是全局
   yarn remove vue //移除包
   yarn global remove vue //移除全局包
   yarn upgrade vue // 升级包
   yarn global upgrade vue //升级全局包 
   ```

3. **yarn 和 npm 命令对照**
   
   ```shell
     Yarn                            Npm            
    yarn init                        npm init
    yarn                           npm install
    yarn gloabl add xxx@x.x.x      npm install xxx@x.x.x -g
    yarn add xxx@x.x.x             npm install xxx@x.x.x --save
    yarn add xxx@x.x.x --dev       npm install xxx@x.x.x --save-dev
    yarn remove xxx                npm uninstall xxx --save(-dev)
    yarn run xxx                   npm run xxx
   ```
   
   
   
   ## 5. Pnpm
   
   1. **安装**
      
      ```shell
      npm install -g pnpm
      ```
   
   2. **命令**
      
      ```shell
      pnpm init // 初始化项目，添加package.json）
      
      pnpm add xxx // 添加依赖
      
      pnpm add -D xxx // 添加开发依赖
      
      pnpm add -G xxx //添加全局包
      
      pnpm install // 安装依赖
      
      pnpm remove xxx // 移除包
      ```
   
   [目录](README)
