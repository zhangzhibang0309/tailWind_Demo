# tailWind_Demo
## 0_介绍一下这个框架

tailwindcss官网

tailwindui官网

他是一个css框架，跟传统的UI框架不太一样，精髓在于CSS对于css的各种封装，tailwind css的源码有18万行左右，这句话是作者说的，彻底的体现了他的框架设计哲学，语义类名是愚蠢的。

### “Best practices” don’t actually work.

> I’ve written a few thousand words on why traditional “semantic class names” are the reason CSS is hard to maintain, but the truth is you’re never going to believe me until you actually try it. If you can suppress the urge to retch long enough to give it a chance, I really think you'll wonder how you ever worked with CSS any other way.

所以说，他的基本使用方法就是给你的html代码加一堆class类名，他的类名都是与底层的css功能看起来相似的，所以自定义程度特别高。

当然他也是有封装好的UI组件的，不过比较少（其实也够用了），大部分都需要花钱。

## 1_安装

安装方式众多，因为你的项目可能采用不同的架构，这里只介绍vue+vite的构建形式。

首先是官方资料，关于安装的教程-安装。

按照这个教程基本没有问题，但是有些细节得说一下。

1. 不能用webpack搭建，我觉得应该是支持的，但是官方没有相关的文档，选择vite更加方便一些。所以第一步先用vite搭建一个vuejs项目。

2. 然后安装tailwindcss

   ```
   npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
   ```

   ﻿

3. 创建配置文件，这时候你会发现项目里面多了两个配置文件，  tailwind.config.js & postcss.config.js，这两个文件可根据tailwind官网做一些自定义配置

   ```
   npx tailwindcss init -p
   ```

4. 这里要对配置文件tailwind.config.js做一些配置，作用是为了优化打包文件，删除生产文件中未使用的样式。  主要是对purge进行配置。

   

   ```
   module.exports = {
   ```

   ```
     purge: [
   ```

   ```
       './index.html',
   ```

   ```
       './src/**/*.{vue,js,ts,jsx,tsx}'
   ```

   ```
     ],
   ```

   ```
     darkMode: false, // or 'media' or 'class'
   ```

   ```
     theme: {
   ```

   ```
       extend: {},
   ```

   ```
     },
   ```

   ```
     variants: {
   ```

   ```
       extend: {},
   ```

   ```
     },
   ```

   ```
     plugins: [],
   ```

   ```
   }
   ```

   ﻿

   

5. 然后你要在项目目录src下面新建一个css的算是入口文件，命名为index.css，里面写上下面几句话

   ```
   @tailwind base;
   ```

   ```
   @tailwind components;
   ```

   ```
   @tailwind utilities;
   ```

6. 最后在你的main.js文件，也就是整个项目的入口文件，导入一下index.css 

   ```
   import './index.css'
   ```

   ﻿

到此位置，根据官方的文档就已经安装完成了，然后就去写一下试试。

## 2_测试 

```
<h1 class="text-8xl">Hello World</h1>
```

记得重启一下项目，然后你发现，css已经生效了，然后马上拿过来一个组件，就是在tailwindui里面的免费组件，发现报错。大体的就是 @headlessui/vue @heroicons/vue/outline 这俩模块找不到，这时候就要去官网看了，在官网这个地方有个资源，打开资源之后能看到有三个库，一个是ui，一个是icon，还有一个是svg。

﻿



![image.png](https://atlas.pingcode.com/files/public/616e9bdff39d56582df63fed)

﻿

﻿



![image.png](https://atlas.pingcode.com/files/public/616e9c1cb1e304f662d59a74)

﻿

这个headless和heroicions就是上面找不到的俩模块，下面安装一下，重启项目，你的组件就可以顺利使用了。

```
npm install @headlessui/vue
npm install @heroicons/vue
```

## 3_Tailwind CSS IntelliSense插件

这个插件，安装之后tailwind的用户体验直接起飞，直接从vsc插件商店安装即可。

主要作用就是会对封装的css类名进行代码提示，而且当你鼠标放在某个class名上面还会展示一下这个类名底层的css具体是什么，✈✈✈✈✈。

不过这个插件只有你跑起来项目之后才能，一开始我还以为需要配置什么，搞了很久，结果跑起来之后就可以用了。

## 4_基本开发使用学习流程

我觉得大概这个框架小项目的话只会用到css类名以及免费的ui库。

ui库就不说了，cv cv。

对于class的各种类名的作用，还是需要查询一下文档的，位置就在tailwindcss官方文档，左边的目录，就是对各种class用法的详细介绍，而且你的css基础还可以的化，你是可以猜到很多用法的，比如我在定义字体的大小，上手写class-xxx，他就会提示然后看到什么3xl，当你的focus移动到上面的时候，就会跳出来内部的css代码，如图

﻿



![image.png](https://atlas.pingcode.com/files/public/616e9e9f7c4ff343d69f0930)

﻿

总之就一个字 爽！