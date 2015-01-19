# Gulp-Toor

[![npm](http://img.shields.io/npm/v/gulp-toor.svg)](https://www.npmjs.com/package/gulp-toor)
[![npm](http://img.shields.io/npm/l/gulp-toor.svg)](https://www.npmjs.com/package/gulp-toor)

## 用途

Gulp插件，使用r.js（require.js）打包目录下所有require.js文件。

## 使用方法

```javascript
gulp.task('test',function(){
	gulp.src(['myapp/**/*.js'],{
		base:'myapp' //设定相对目录，在输出时myapp之后的路径会保留
	}).pipe(toor({
		baseUrl:'myapp',	//require.js模块根目录

		//一些require.js配置，比如packages/paths/shim等
		packages:[{
			name: 'echarts',
			location: 'lib/echarts',      
			main: 'echarts'
		},{
			name: 'zrender',
			location: 'lib/zrender', // zrender与echarts在同一级目录
			main: 'zrender'
		}],
		paths:{
			jquery:'lib/jquery'
		},
		shim: {
			'lib/modernizr': {
				exports: 'Modernizr'
			},
			'lib/jquery':{
				exports: 'jQuery'
			}
		},
		exclude:['jquery']
	})).pipe(gulp.dest('myapp-build'))	//输出目录，后面会接上源文件myapp之后的路径
		.on('error',function(err){
		console.log(err);	//输出错误（gulp插件会触发错误事件，但不会输出，需要手工处理）
	})
});
```
