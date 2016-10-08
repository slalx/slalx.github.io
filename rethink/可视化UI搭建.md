# 可视化UI搭建


最近研究了下有关可视化搭建页面的，发现一个牛逼的可视化搭建系统，需要有以下几个特点



1. 框架无感知

	> 不管你是用react,bootstrap,angular等流行面的那种框架，搭建系统都应该能够适配,这就要求有一个通用的页面模型，来描述整个页面

2. 数据处理框架可接入

	> 搭建系统要能够支持数据处理框架的接入，来完成页面组件之间的交互
	
3. 组件属性可配置

	> 组件属性应该可以增加和减少，并且所有的属性直都应该可以配置

4. 应该具有可扩展的布局系统
> 5. 
5. 可以和gitlab或者github集成

	> 可以和源代码管理系统打通 
	 
6. 含有构建打包系统
	> 页面设计完成，应该可以自动打包
7. 可以和cdn发布系统集成
	> 可以一键发布到cdn

## 相关项目

1. [structor](https://github.com/ipselon/structor)
	
	- What Structor is
		- 	Structor is a visual editor (WYSIWYG editor) - you may construct a React component of any complexity combining components and styling them right on the page.
		- [ ]Structor is a scaffolding tool  you may generate scaffolds of different types of React components (dumbs, containers) with different configuration.
		- [x]Structor is a library tool - you may find many full-fledged components which can be installed into your project from Structor Market.
		- Structor is a playground tool - you may modify the source code and have an instant feedback immediately because of embedded Hot Reloading tools.
 

	- wiki 
		- [Structor's component model representation
](https://github.com/ipselon/structor/wiki/Structor's-component-model-representation)  
2. [react-designer](https://github.com/rsamec/react-designer) `推荐`
	- whart react designer is
		- React designer is WYSIWYG editor for easy content creation (legal contracts, business forms, marketing leaflets, inforgrafics, technical guides, visual reports, rich dashboards, tutorials and other content, etc.).

	- wiki 
			- [react-html-pages-render](https://github.com/rsamec/react-html-pages-renderer)
			- [ppt](https://github.com/rsamec/ptt)
	- Live demo  
		-  [demo](http://rsamec.github.io/react-designer/#/?_k=5vozk3)
	- module 
		- [react-property-editor](https://github.com/rsamec/react-property-editor) 
		- [react-html-pages-render](https://github.com/rsamec/react-html-pages-renderer)
		- [布局组件](https://github.com/kodyl/react-flexr)





# immutable data

- [freezer](https://github.com/arqex/freezer)


