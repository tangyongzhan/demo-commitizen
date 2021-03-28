

# 如何生成规范的Git提交信息。
> 本案例学习如何，规范代码提交
知识：husky + commitizen + commitlint + Conventional Commits 

## 说明
1. 代码提交规范：Conventional Commits 是提交注释的规范
2. 检查规范工具：commitlint 是检查注释是否规范的工具
3. 检查提交钩子：husky 是Git的钩子，可以在执行Git命令前执行一些操作函数，如：格式化代码，检查commit是否规范。
4. 生成规范提交：commitizen 是生成标注的提交规范的工具，因为"Conventional Commits"提交的规范较为复查，使用工具会减少出错，确保每次提交符合规范。

## 一、规范： Conventional Commits(约定式提交规范)

1. 代码提交注释模版：
    ```shell
    <type>[optional scope]: <subject>
    //空一行
    [optional body]
    //空一行
    [optional footer(s)]
    ```
2. 详细说明：
* type 的类别
    ```shell
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

3. 符合规范的提交
```shell
git commit -m "fix: 修复了某个bug"
git commit -m "feat(common): common文件 添加了XXX方法"
```


## 二、规范的检查工具 commitlint

> commitlint 是一个检查代码是否符合  conventional commit format. 规范的工具

```shell
# 1. commitlint的cli和config-conventiona配置
npm install --save-dev @commitlint/{config-conventional,cli}

# 2. 生成默认配置
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```


## 三、Git提交钩子函数工具 husky ( Git hooks)

> husky是（Git hooks）代码提交的钩子函数工具, 可以在执行Git命令前执行一些操作函数，如：格式化代码，检查commit是否规范。

```shell
# 1. 安装husky(Install Husky v5)
npm install husky --save-dev
# or
yarn add husky --dev

# 2. husky 安装激活 （ Active hooks ）
npx husky install
# or
yarn husky install

# 3. 添加husky钩子函数，在提交时候使用commitlint检查注释是否规范（ Add hook ）
npx husky add .husky/commit-msg "npx --no-install commitlint --edit $1"
# or
yarn husky add .husky/commit-msg "yarn commitlint --edit $1"
```
 
 ## 四、commitizen 生成提交规范工具
 1. 安装 commitizen 工具

 ```shell
 npm install commitizen -g
 ```

2. 生成commitizen配置

```shell
# 生成配置命令
commitizen init cz-conventional-changelog --save-dev --save-exact
```
```js
// 执行命令后：package.json 会自动添加上方生成的配置。
"config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    }
},
```

3. 配置`husky`的`hooks`使用`git cz`来触发`commitizen`生成提交规范信息

```json
 "husky": {
    "hooks": {
      "prepare-commit-msg": "exec < /dev/tty && git cz --hook || true"
    }
  }
```

4. 后续使用 git cz 生成合规的提交信息，如此和确保每次提交都遵循了“约定式提交规范”
```
git add .
git cz 按步骤生成规范的提交
```





