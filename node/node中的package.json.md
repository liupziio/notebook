1.  	name - 包名.

2. version - 包的版本号。
3. description - 包的描述。
4. scripts - 指定了运行脚本命令的npm命令行缩写，
5.  dependencies- 运行时依赖
6.  devDependencies 开发时依赖
7. homepage - 包的官网URL。

8.   author - 包的作者，它的值是你在https://npmjs.org网站的有效账户名，遵循“账户名<邮件>”的规则，例如：zhangsan <zhangsan@163.com>。

9.  contributors - 包的其他贡献者。

10. repository - 包代码的Repo信息，包括type和URL，type可以是git或svn，URL则是包的Repo地址。

11.    main - main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 index.js。

12.    keywords - 关键字