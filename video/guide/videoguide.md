# 移动端html5视频开发指南

1. 在页面添加一个视频

	```
	<video src="demo.webm" type="video/webm">
	    <p>您的浏览器不支持video元素.</p>
	</video>
	
	```

2. 为video元素指定多个视频格式

	并不是所有的浏览器都支持同一种格式，source可以让开发者为video元素指定多个视频格式
	
	```
	    <video controls>
	      <source src="demo.webm" type="video/webm">
	      <source src="demo.mp4" type="video/mp4">
	      <p>您的浏览器不支持video元素.</p>
	    </video>
	
	```
	
	当浏览器解析到<source>标签，使用type属性来决定哪个文件被下载和播放。如果浏览器支持webm格式，就会播放demo.webm文件，如果不支持，浏览器就会接着检查是否支持MPEG-4。这里<https://www.xiph.org/video/vid1.shtml>可以看到音视频在web上是如何工作的。
	
	这种指定视频格式有下面的几点好处
	
	- 开发这可以根据喜爱的顺序列出多个格式
	- 浏览器客户端切换格式减少了延迟；只有一个请求去获取内容
	- 在浏览器中选择视频格式比在浏览器端更加简单，快速，可靠
	- 为每个source元素指定type属性可以提高网络性能，这样就不用让浏览器选择一个source,下载一段段视频，再判断格式是否支持。
	
	在移动环境下上面你的几点好处尤其明显，移动环境下网速和延迟，使得用户的耐心是有限的。如果不为source属性指定type,当多个source都不支持时，会严重影响性能。同时也要保证请求的response heanders是否返回了正确的mime type,否则video source type也不工作。
	
	
	
	
	
3. 为source指定一个开始和结束时间

	这样可以节省带宽。使用Media Fragments API 可以为video元素添加一个开始时间和结束时间。
	具体格式就是在url后面加入下面你的格式**#t=[start_time][,end_time]**
	假如要播放5秒到10秒的视频，向下面这样,[示例]()
	
	```
	<source src="video/chrome.webm#t=5,10" type="video/webm">
	
	```
	
	使用Media Fragments API也可以为视频指定多个画面，<https://www.youtube.com/watch?v=y3CFxQb7JZk>可以看下这里的demo
	
	** 注意 **
	
	- Media Fragments API支持大部分的android平台，但是ios不支持
	- Range Request需要服务器端支持
	
	
4. 为视频指定一个封面

	通过video元素的poster属性可以为视频指定封面，这样可以让用户在没有没有加载或者播放的情况下既可以对视频有所了解。

	```
	<video poster="poster.jpg" ...>
  		...
	</video>
	
	```	

	在src出现错误或者视频格式不支持的情况下，poster也可以作为替代。不足就是poster需要额外的请求来加载。
	
	
5. 查看支持的格式

	使用 canPlayType() 找出支持的视频格式。该方法采用与 mime-type 一致的字符串参数和可选编解码器，会返回以下某个值：
	
	
	返回值 | 描述
	------------ | -------------
	(empty string) | 容器和/或编解码器不受支持。
	maybe | 容器和编解码器可能受支持，但是浏览器 需要下载部分视频才能明确。 
	probably | 格式似乎受支持。
	
	以下是一些 canPlayType() 参数示例和在 Chrome 中运行时的返回值：
	
 	类型      | 响应
------------ | -------------
video/xyz | （空字符串）
video/xyz; codecs="avc1.42E01E, mp4a.40.2" | （空字符串）
video/xyz; codecs="nonsense, noise" | （空字符串）
video/mp4; codecs="avc1.42E01E, mp4a.40.2" | probably
video/webm | maybe
video/webm; codecs="vp8, vorbis" | probably
	

6. 制作多种格式的视频

	许多工具都可以帮助您将同一视频保存为多种格式：
	
	- 桌面工具： [FFmpeg](https://ffmpeg.org/)
	- GUI应用: [Miro](https://www.mirovideoconverter.com/) [HandBrake](https://handbrake.fr/) [VLC](https://www.videolan.org/)
	- 在线编码/转码服务：[Zencoder](https://en.wikipedia.org/wiki/Zencoder) [Amazon Elastic Encoder](https://aws.amazon.com/elastictranscoder)

7. 查看所用的格式

	想了解浏览器实际所选的视频格式吗？
	在 JavaScript 中，使用视频的 currentSrc 属性即可返回所用的来源。
	
8. 查看视频大小

	视频帧实际编码大小可能会与视频元素的尺寸有所不同（正如图片可能不会以实际尺寸显示一样）。
	要查看视频的编码大小，请使用视频元素的 videoWidth 和 videoHeight 属性。width 和 height 会返回视频元素的尺寸，而这些尺寸可能已使用 CSS 或内联宽度和高度属性进行过调整。
	
	** 注意 **
	
	- 请勿提供框架大小或质量超过平台处理范围的视频。
	- 提供适当时长的视频。
	- 视频较长可能会导致无法顺畅下载和定位：一些浏览器可能需要等待视频下载完成后才可播放。
	
	
9. 确保视频不会溢出容器

	如果视频元素过大，不适合当前视口，则可能会从容器中溢出，从而使用户无法观看内容或使用 控件。

	您可以使用 JavaScript 或 CSS 控制视频尺寸


	** 注意 **
	
	请勿强制调整元素尺寸，否则会使宽高比异于原始视频。挤压或拉伸都会造成较差的视觉效果。

10. 设备方向在不同设备中的工作原理

	设备方向对台式机显示器或笔记本电脑而言不会构成问题，但对移动设备或平板电脑网页设计却是至关重要。
	
	iPhone 版 Safari 可以在横向和纵向之间自由转换：
	
	![](http://gtms04.alicdn.com/tps/i4/TB1xg6_HpXXXXa3XVXXttgA8VXX-338-600.png) ![](http://gtms03.alicdn.com/tps/i3/TB1ofr_HpXXXXbdXVXXdrLoIVXX-600-338.png)
	
	iPad 和 Android 版 Chrome 中的设备方向问题十分棘手。 例如，在未进行自定义设置的情况下，iPad 上横向播放的视频如下所示：
	
	![](http://gtms01.alicdn.com/tps/i1/TB1hhZXHpXXXXb7XFXX8JnCIVXX-600-450.png)
	
11. 内联或全屏显示
	
	不同的平台展示视频的方式也不相同。iPhone 版 Safari 会在网页中内联显示视频元素，却会以全屏模式播放视频：
	![](http://gtms02.alicdn.com/tps/i2/TB1W1T_HpXXXXbfXVXX3sk2NVXX-400-600.png)
	
	在 Android 设备中，用户可以通过点击全屏图标来请求全屏模式。但是默认情况下，浏览器以内联模式播放视频：

	![](http://gtms01.alicdn.com/tps/i1/TB1HbP9HpXXXXXaaXXX7oBEJVXX-360-600.png)
	
	iPad 版 Safari 以内联模式播放视频：
	
	![](http://gtms01.alicdn.com/tps/i1/TB1hhZXHpXXXXb7XFXX8JnCIVXX-600-450.png)
	
	
12. 控制内容的全屏模式

	不强制视频全屏播放的平台为 Fullscreen API 提供广泛支持。使用此 API 可以控制内容或网页的全屏模式。
	
	以全屏模式显示某元素，如video:
	
	```
		elem.requestFullScreen();
	
	```
	以全屏模式显示整个文档
	
	```
		document.body.requestFullScreen();
	
	```
	您还可以监听全屏状态变化
	
	```
		video.addEventListener("fullscreenchange", handler);
	```
	或者，查看元素当前是否处于全屏模式：
	
	```
		console.log("In full screen mode: ", video.displayingFullscreen);
	
	```
	您也可以使用 CSS :fullscreen 伪类来更改以全屏模式显示的元素的显示方式。
	
	
	在支持 Fullscreen API 的设备中，考虑将缩略图用作视频占位符：
	
	** 注意 **
	
	requestFullScreen()有可能需要处理兼容性问题
	
13. 添加字幕

	要使媒体在移动设备上更易访问，请使用track元素添加字幕或说明。

	** 注意 **
	
	Android 版 Chrome、iOS Safari 以及当前的所有桌面版浏览器（Firefox 除外）均支持track元素
	
	如下面这样
	
	```
	    <video controls>
	        <source src="demo.webm" type="video/webm" />
	        <source src="demo.mp4" type="video/mp4" />
	      <track src="demo-en.vtt" label="English captions"
	             kind="captions" srclang="en" default>
	      <p>您的浏览器不支持video元素.</p>
	    </video>
	
	```
	
	track元素的 src 属性决定字幕文件的位置。
	
14. 定义字幕文件中的字幕

	字幕详解<http://www.atatech.org/articles/22025>

	
	```
		WEBVTT

		00:00.000 --> 00:04.000
		坐在树枝上使用笔记本电脑的人。
		
		00:05.000 --> 00:08.000
		树枝折断，他开始下落。
		
		...
	
	```

15. 视频元素属性参考

		
	属性 | 适用范围| 描述
	------------ | -------------
	src | 所有浏览器 |视频地址|
	poster |所有浏览器|封面图，视频元素显示后无需下载视频内容就可立即显示的图片文件地址| 
	preload | 所有移动浏览器均无法预加载|浏览器提示：播放前预加载元数据（或某个视频）十分重要。选项包括无、元数据或自动|
	autoplay|iPhone 和 Android 设备均不支持；所有桌面版浏览器、iPad 以及 Android 版 Firefox 和 Opera 均支持。|自动开始下载和播放|
	loop|所有浏览器|循环播放视频|
	controls|所有浏览器|显示默认视频控件（播放、暂停等）|

	自动播放
	
	在桌面设备中，autoplay 会指示浏览器尽快开始下载并播放视频。在 iOS 设备和 Android 版 Chrome 中，autoplay 不起作用；用户必须点按屏幕才能播放视频。
	
	即使是在可以进行自动播放的平台中，您也需要考虑将其启用是否妥当：
	- 数据流量可能会十分昂贵。
	- 使媒体不事先询问就开始下载并播放，这可能会在无意间占用带宽和 CPU，从而使页面呈现出现延迟。
	- 用户可能会处于不便播放音频或视频的环境中。
	
	开发者可通过 WebSettings API 在 Android WebView 中配置自动播放行为。 默认情况下，它处于启用状态，但是 WebViewIt 应用可选择将其停用。

	预加载
	
	preload 属性会指示浏览器应预加载的信息或内容量
	
	值 | 描述
	------------ | -------------
	none|用户甚至可能不会观看视频，那就无需预加载任何内容。|
	metadata|应预加载元数据（时长、尺寸、文字轨道），但要尽量减少视频加载量。|
	auto|用户都希望可以立即下载整个视频。|
	
	preload 属性在不同平台中的效果不同。 例如，Chrome 在桌面设备上可以缓冲 25 秒的视频，却无法在 iOS 或 Android 设备上缓冲。这意味着，移动设备上可能会出现播放启动延迟，而在桌面设备上却不会出现这种情况。请参阅 [Steve Souders 的测试网页](https://stevesouders.com/tests/mediaevents.php)，了解全部详情。
	
16. 视频元素的javascript属性

	属性 | 描述
	------------ | -------------
	currentTime| 获取或设置播放位置（以秒为单位）
	volume|获取或设置视频的当前音量
	muted|获取静音状态或将音频设为静音
	playbackRate|获取或设置播放速率；1 表示以常规速度向前播放。
	buffered|说明当前已缓冲、可以播放的视频量,[示例](http://slalx.github.io/video/samples/video-buffer.html),在chrome的缓冲量是21.44S
	currentSrc|视频的当前播放位置。
	videoWidth|以像素为单位表示的视频帧宽度(这可能会与视频元素宽度有所不同）
	videoHeight|以像素为单位表示的视频帧高度(这可能会与视频元素高度有所不同）

	** 注意 **
	
	移动设备既不支持 playbackRate，也不支持音量。

16. 视频元素的javascript属性	

		
	属性 | 描述
	------------ | -------------
	load()|在没有开始播放的情况下加载或重新加载视频来源：例如，当使用 JavaScript 更改视频 src 时
	play()|从当前位置播放视频
	pause()|在当前位置暂停播放视频
	canPlayType('format')|找出支持的格式
	
	** 注意 **
	
	除非以响应用户操作（例如点击按钮）的方式调用 play() 和 pause()， 否则这两种方法无法在移动设备（Android 版 Opera 除外）上起作用
	
17. 视频元素的事件

	事件名称 | 描述
	------------ | -------------
	canplaythrough|当所提供的数据足以使浏览器相信自己可以连贯地播放整个视频时触发的事件。
	ended|视频播放完毕后触发的事件
	error|出现错误时触发的事件
	playing|视频首次开始播放时、暂停后或重新开始播放时触发的事件。
	progress|为指明下载进度而定期触发的事件
	waiting|操作延迟，等待另一操作完成时触发的事件
	loadedmetadata|浏览器完成视频元数据（时长、尺寸、文字轨道）加载后触发的事件
	
18. 视频内容保护 html5 DRM