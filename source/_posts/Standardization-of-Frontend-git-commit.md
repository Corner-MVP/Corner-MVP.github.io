---
title: Standardization of Frontend git commit
date: 2022-02-11 16:38:35
tags:
  - git
categories:
  - Frontend
---

## 1. Background

Since git allows multiple developer to maintain one public repository, however different developers have different code style and commit style. Therefore, a standardize process is required.

## 2. Tools

- `@commitlint/cli` : the cli of `commitlint`
- `@commitlint/config-conventional` : the rule of `commitlint`
- `husky` : prevent git commit that do not meet git commit rules

## 3. installation steps

- install dependencies

```bash
npm i husky@4.3.8 - D
npm install @commitlint/config-conventional --save-dev
npm install @commitlint/cli --save-dev
npm install @commitlint/parse --save-dev
```

- update `package.json`

```json
// package.json
"husky": {
	"hooks": {
		"commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
	}
},
```

- add configuration file `commitlint.config.js`

```jsx
module.exports = {
  extends: [
    "@commitlint/config-conventional"
  ],
  rules: {
    'type-enum': [
      2,
      'always',
      [
        'feat',      // feature 新功能，新需求 feature
        'fix',       // 修复 bug fix bug
        'docs',      // 仅仅修改了文档，比如README, CHANGELOG, CONTRIBUTE等等 edit docs for example README, CHANGELOG, CONTRIBUTE etc.
        'style',     // 仅仅修改了空格、格式缩进、逗号等等，不改变代码逻辑
        'refactor',  // 代码重构，没有加新功能或者修复bug
        'test',      // 测试用例，包括单元测试、集成测试等
        'revert',    // 回滚到上一个版本
        'perf',      // 性能优化
        'chore',     // 改变构建流程、或者增加依赖库、工具等，包括打包和发布版本
        'conflict'   // 解决合并过程中的冲突
      ]
    ],
    'type-case': [0],
    'type-empty': [0],
    'scope-empty': [0],
    'scope-case': [0],
    'subject-full-stop': [0, 'never'],
    'subject-case': [0, 'never'],
    'header-max-length': [0, 'always', 72]
  }
};
```

- error example

![faild](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/0fe78710-087d-46be-b1f0-f7ede2faf82a/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220211T084733Z&X-Amz-Expires=86400&X-Amz-Signature=aa97e379e29e14812635037e85fe90d6455c28eb0ac7895b5505b2db6e715889&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

- correct example

![correct](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/8fa3d98d-2268-40fb-b7c4-ac1366f9a078/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220211%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220211T084751Z&X-Amz-Expires=86400&X-Amz-Signature=30cc7330e7c008587b8ec15654d1ad74fcbc762bcee306d6228a6c0baae39f83&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

## 4. Tips

Since the latest version of `husky` has bug,  `husky hooks` is not working.  Therefore, it needs to install lower version of `husky` . Firstly, run `git config core.hookspath` in command to check whether the return value is blank or not. If the return value is `.husky` , run `git config --unset core.hookspath` to delete it. And then uninstall `husky` and install lower version of `husky`.