# demo-commitizen


## 说明
1. Conventional Commits 是提交注释的规范
2. commitlint 是检查注释是否规范的工具
3. husky 是Git的钩子，可以在执行Git命令前执行一些操作函数，如：格式化代码，检查commit是否规范。

## Conventional Commits(约定式提交规范)

#### 代码提交注释模版：
```
<type>[optional scope]: <subject>
//空一行
[optional body]
//空一行
[optional footer(s)]
```
#### 详细说明：
* type 的类别
```
feat：增加一个新功能
fix：修复bug
docs：只修改了文档
style：做了不影响代码含义的修改，空格、格式化、缺少分号等等
refactor：代码重构，既不是修复bug，也不是新功能的修改
perf：改进性能的代码
test：增加测试或更新已有的测试
chore：构建或辅助工具或依赖库的更新
```
* scope 可选，表示影响的范围、功能、模块
* subject 必填，简单说明，不超过50个字
* body 选填，用于填写更详细的描述
* footer 选填，用于填关联issus,或BREAK CHANGE
* BREAKING CHANGE 不向下兼容的修该

#### 符合规范的提交
```
git commit -m "fix: 修复了某个bug"
git commit -m "feat(common): common文件 添加了XXX方法"
```


## commitlint （检查commit提交的注释规范）
> commitlint 是一个检查代码是否符合  conventional commit format. 规范的工具

1. 安装commitlint检查的 cli 和 conventional 配置
```
npm install --save-dev @commitlint/{config-conventional,cli}
```

2. 生成默认配置
```
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```


## husky ( Git 的钩子)
> 代码提交钩子：Git hooks 提交的钩子函数, 可以在执行Git命令前执行一些操作函数，如：格式化代码，检查commit是否规范。

1. 安装husky(v5版本)
```
# Install Husky v5
npm install husky --save-dev
# or
yarn add husky --dev
```

2. husky 
```
# Active hooks
npx husky install
# or
yarn husky install
```

2. 添加husky钩子函数，在提交时候使用commitlint检查注释是否规范
```
# Add hook
npx husky add .husky/commit-msg "npx --no-install commitlint --edit $1"
# or
yarn husky add .husky/commit-msg "yarn commitlint --edit $1"
```

 
 ## commitizen 生成标注的提交规范
 ```
 npm install commitizen -g
 ```



2. 在package.json添加commitizen配置

使用下方命令，会生成Conventional Changelog 的日志信息
```
commitizen init cz-conventional-changelog --save-dev --save-exact
```
package.json 会自动添加上方生成的配置。

```
"config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    }
},
```

 3. husky的hooks配置，后续使用 git cz 来触发commitizen生成提交规范信息。
 ```
 "husky": {
    "hooks": {
      "prepare-commit-msg": "exec < /dev/tty && git cz --hook || true"
    }
  }
 ```

