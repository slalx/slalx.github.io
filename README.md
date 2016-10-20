# 技术产品管理沉思录



## 技术

#### 图片优化技术 

- [Medium 是如何优化图片加载的](http://www.jackpu.com/medium-shi-ru-he-zuo-tu-pian-jia-zai-de/)

	> 这篇文章重点讲了medium,google,facebook是如何实现图片等预览技术的


#### API设计

- api设计模式
	- [一个API，多个门面？](http://www.infoq.com/cn/articles/api-facades)
- 接口描述语言
	
	1. [swagger](http://swagger.io/)
	2. [RAML](http://raml.org/)
	3. [API blueprint](https://apiblueprint.org/)
	
		> 尽管公司是以团队的形式来组织的，但是我看到在越来越多的场景下，开发人员会被分为前端开发人员（Web或移动）以及后端开发人员，其中后端开发者会负责实现Web或移动设备所需的API。Web API成为了项目交付的中心点：API是一种契约，将不同的团队关联了起来，能够让他们高效协作。
	如果我们开发的API要给别人使用的话，很重要的一点就是不要破坏这种契约。通常，有些框架和工具能够让我们根据代码库生成API定义——例如，通过注解驱动的方式，在端点、查询参数等内容上添加注解。
	但有时候，即便你自己的测试用例依然能够通过，很小的代码重构也可能会破坏契约。你的代码库没有问题，但重构可能会破坏API消费者的代码。为了更加高效的协作，可以考虑采用API契约优先的方式，确保你的实现依然能够遵循共享的协议：API定义。
	目前，有不少可用和流行的API定义语言，如Swagger（Open API specification）、RAML或API Blueprint。你可以选择一个最适合你的。
	采用API定义的方式有多项优势。首先，因为我们的实现需要遵循API定义，所以兼容性就更不容易遭到破坏了。其次，API定义对工具化非常有利。通过API定义，我们可以生成客户端SDK，这样的话API的消费者就可以将其集成到他们的项目中，实现对API的调用，甚至可以作为skeleton，用来生成服务的初始实现。
	我们还可以创建API的mock，这样在底层API构建的时候，开发可以调用这些mock，从而避免协调API生产者和消费者之间不同的开发周期。每个团队都可以按照自己的节奏开展工作！但是，它的好处并不局限于代码和兼容性，还涉及到文档。
	API定义语言还会帮助我们对API实现文档化，它们会生成很漂亮的文档，展现了各种端点、查询参数等等，并且（有时）还会提供可交互的控制台，通过它，我们可以很容易地发起对API的调用。

#### 应用架构模式


- <http://www.ebpml.org/blog15/2016/01/sam-a-functional-approach-to-ui-construction/>

	> SAM

#### 依赖管理

- [持续集成之“依赖管理”](http://www.infoq.com/cn/news/2011/05/ci-dependency-management/)

#### HTTP

- [HTTP2 特性和抓包分析](http://mp.weixin.qq.com/s?__biz=MzAxODE2MjM1MA==&mid=2651551351&idx=2&sn=a56ff090060f97e11e856aef2622a717&chksm=8025a1b6b75228a0080fa971222b3cb7c3179ba5474028b8fa4656619073c4c14d76cf83cd86&scene=0#wechat_redirect)



