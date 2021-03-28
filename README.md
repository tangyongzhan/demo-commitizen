# demo-commitizen



### commitlint
> commitlint 是代码提交检查，检查提交的 注释信息是否规范

1. 安装commitlint检查的 cli 和 conventional 配置
```
npm install --save-dev @commitlint/{config-conventional,cli}
```

2. 生成默认配置
```
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

### husky 
> 代码提交钩子：Git hooks 提交的钩子函数

1. 安装husky
```
npm install husky --save-dev
```

npx husky install


2. 添加钩子
```
# Add hook
npx husky add .husky/commit-msg "npx --no-install commitlint --edit $1"
# or
yarn husky add .husky/commit-msg "yarn commitlint --edit $1"
```

 


commitizen： git提交的约束规范工具

```
npm install husky --save-dev
```

commitizen
