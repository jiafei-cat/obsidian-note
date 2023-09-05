> 官方文档: https://docs.npmjs.com/cli/v9/configuring-npm/package-json

## main
> 指定当前包入口，如果没有指定则取当前包的index.js

```json
{
 "main": "./dist/index.esm.js"
}
```

## types
> 声明当前包类型入口文件

```json
{
	"types": "index.d.ts",
}
```

## exports
> node 12+版本
> 以前导出当前这个包需要声明main字段来指定入口

```json
"exports": {
	".": {
		"types": {
			"default": "./sdk.d.ts"
		},
		"default": {
			"default": "./dist/sdk/index.js"
		}
	},
	"./package.json": "./package.json"

},
```

指定不同的引入
`require`为 commonJS 导入时指定文件
`defalut`为 ESM 导入时指定文件
```json
{
	"exports": {
		".": {
			"types": {
				"require": "./index.d.cts",
				"default": "./index.d.ts"
			},
			"browser": {
				"require": "./dist/browser/axios.cjs",
				"default": "./index.js"
			},
		
			"default": {
				"require": "./dist/node/axios.cjs",
				"default": "./index.js"
			}
	},
	"./package.json": "./package.json"
	},
}
```

## bin
> 该配置在安装该包或者npm link时，会将指定的文件作为可执行加入到配置的系统环境变量中(所以该文件要声明#!/usr/bin/env node 来指定用node运行)

```json
{
	"bin": "bind/index.js",
}

// 多个
{
	"bin": {
		"test": "dist/cli/index.js",
		"test2": "dist/cli/index2.js",
	},
}
```

## files
> 当npm public时指定哪些文件public

```json
{
	"files": [
		"package.json",
		"dist",
		"*.d.ts"
	],
}
```