### yarn的基本操作

yarn安装更新
-

npm安装更新yarn：

	npm install --global yarn

npm与yarn的指令对比
-

初始化包：

	npm init	或	yarn init

根据package.json安装依赖：

	npm install		或	yarn

安装依赖并写入到package.json里的dependencies：

	npm install [包名] --save	或	yarn add [包名]

全局安装依赖并写入到package.json里的dependencies：

	npm install [包名] -g --save		或	yarn global add [包名]

安装依赖并写入devDependencies：

	npm install [包名] --save-dev	或	yarn add [包名] --dev/-D

升级包版本：

	npm update [包名] --save		或	yarn upgrade [包名]

卸载包：

	npm uninstall [包名] --save	或	yarn remove [包名]

有时候文件夹中或生成一个跟package.json同级名字叫yarn.lock的文件，这文件的功能是每次添加依赖或者更新包版本，yarn都会把相关信息写入这个文件中。这样可以解决同一个项目在不同机器上环境不一致的问题，虽然npm也有类似的，但是没有yarn 使用方便，这体现了yarn安全依赖管理的特点。

【有待补充】