- id:: 61ff3126-2ab9-4c1e-824c-7df74411e42b
-
-
- 主要的几种方法
	- 1、（不推荐，很丑，没有暗黑主题）官方，当前需要手动到logseq软件，导出JSON文件，然后用部署，但是以后可能会有一键部署，但是优先级不高。
		- 源代码库： https://github.com/logseq/publish
		  id:: 61f94c39-e68d-41ae-b2ff-959522bfef73
		- 示例站点： https://eloquent-keller-6512b6.netlify.app/
	- 2、这个是将logseq的库文件直接内嵌到静态文件编辑器（ eleventy，……）中，在部署时通过nodejs 处理成静态文件，（可能对一些自己魔改的文件不支持，需要源代码适配）
		- 源代码库：https://github.com/believer/devlog
		- 示例站点：https://devlog.willcodefor.beer/
	- 3、（优先推荐）通过github action 将github库中的logseq库文件，通过action的docker编译成静态文件，到gh-pages分支（可自己修改构建文件的去处，如用action的ftp-action，直接推送）
		- action市场主页：https://github.com/marketplace/actions/logseq-publish
		- 源代码库：https://github.com/pengx17/logseq-publish
		- 示例站点：
			- 1、https://docs.logseq.com/
			  2、https://note.xuanwo.io/
			  3、https://pengx17.github.io/knowledge-garden/
	-
- 优先推荐的部署方法：
  id:: 61f94db6-d369-4ee3-9226-baf4b45741b7
	- 1、在github下载logseq-publish action作者 [pengx17](https://github.com/pengx17) 的自己部署的库：https://github.com/pengx17/knowledge-garden （点击链接，点击绿色图标code，选择最后下载zip）
	- 2、在自己的github，建一个空私有库，同步到本地，把knowledge-garden.zip的文件，解压缩到本地同步下来的github库文件夹，同步到github，检测action是否自动运行（main.yml），并产生了新的分枝：gh-pages，
	- 3、然后在vercel中部署，默认是main分支，部署完，打开网页是不行的，需要在vercel项目的设置中，设置生产分支为：gh-pages，在github中提交或者直接在action中点击重新部署，激活cli action的运行，产生新的gh-pages文件，然后刷新vercel部署的网页，等待Vercel 的CDN，加载你的页面（网页代码的性能可能不足，要等待一会）。
	- 4、没有问题后，用本地logseq软件，打开这个库，然后修改
	- 5、在logseq设置中的[[Custom configuration]]，可以设置哪些页面能够展示，以及主页是哪个页面
- 注意事项：
- 1、github action中logseq-publish的是如何区分私有页面与公开页面的？
	- github库是私有的，但是logseq-publish 的action是不是只会将页面属性中标注了 publish的页面，处理成网页，公开展示？
	-
- 2、如何加额外的JavaScript和html代码到部署网页？
	- 在github库的workflow文件夹的main.yaml，编写action代码，将添加的JavaScript和HTML代码写入到index.html.