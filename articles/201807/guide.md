<h1 id="-">文档编写流程与规范</h1>
<h2 id="-">编写流程</h2>
<p>第一步：建立产品目录</p>
<p>根据产品名字 修改模板中相应内容，按规则给出书写方法。</p>
<p>第二步：创建 github仓库   (<a href="https://github.com/iuap3/">https://github.com/iuap3/</a>)</p>
<p>把已经建立好的产品规范目前，上传到github仓库。</p>
<p>第三步：通知各角色编写文档</p>
<p>在github上编写文档。</p>
<p>第四步：收到提交后，合并，定时推送到网站。</p>
<h2 id="-">编写方式</h2>
<p>在线仓库地址--- <a href="https://github.com/iuap3/">https://github.com/iuap3/</a></p>
<p>当你想更新文档仓库里内容时，要走一个流程：</p>
<p>1、先 fork 别人的仓库，相当于拷贝一份，相信我，不会有人直接让你改修原仓库的；</p>
<p>2、clone 到本地编写MD文件，push到fork 的仓库；</p>
<p>3、fork 的仓库发起 pull request 给原仓库，让他看到你修改合并。</p>
<p>至此，整个 pull request 的过程就结束了。</p>
<p>编写就是MD标准格式，请参考线上其他文档。</p>
<h2 id="-">编写规范</h2>
<h3 id="-">文案风格</h3>
<p>1、一定多检查，确保没有错别字。</p>
<p>2、即使是流行语中的谐音错别字也不要使用，比如「墙裂」、「童鞋」等。</p>
<p>3、我们崇尚精练的文风。请在检查中把对表达意思没有明显作用的字、词、句删除，在不影响表达效果的前提下把文案长度减到最短。</p>
<p>4、记住，如果你写了一条文案觉得非常聪明非常好笑，很可能需要停下来想一下用户是否能理解。</p>
<h3 id="-">目录要求</h3>
<p>1、  文件命名规则：</p>
<pre><code>* [目录名称](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/产品英文名XXX/章节编号X-/目录英文名.md)
</code></pre><p>例如：</p>
<pre><code>* [产品概述](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/1-/prod_intro.md)
</code></pre><p>articles文件夹，articles的下级产品英文名“esb”文件夹，产品英文名esb的下级“1-”文件夹，“1-”的下级prod_intro.md内容文件。</p>
<p>英文名必须全部小写。</p>
<p>其他章节依此方法设置即可。</p>
<p>2、  图片的存放位置：</p>
<pre><code>* [目录名称](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/产品英文名XXX/章节编号X-/图片images/图片英文名.jpg) 
</code></pre><p>例如：</p>
<pre><code>* [产品概述](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/1-/images/tupian.jpg)
</code></pre><p>比如产品概述中的图片，本章中包含的所有图片请放置于articles/产品英文名esb /1-/images文件夹下，无此文件夹请依次建立。</p>
<p>3、  此目录必须在SUMMARY.md文件中。所有MD文件是UTF-8编码。</p>
<p>SUMMARY格式：</p>
<pre><code># 集成总线

* [集成总线](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/1-/)
   * [产品概述](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/1-/introduction.md)
   * [产品优势](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/1-/advantage.md)
   * [应用场景](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/1-/scenarios.md)
   * [基础架构](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/1-/infrastructure.md)
   * [产品历程](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/1-/course.md)
* [快速入门](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/2-/)
   * [场景一：如何快速更换导航栏](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/2-/scene1.md)
   * [场景二：如何开发widget](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/2-/scene2.md)
* [用户手册](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/3-/)
* [常见问题](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/4-/)
   * [如何开发widget](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/4-/question1.md)
</code></pre><p>4、  在上例中，[集成总线] 、[快速入门] 、[用户手册]和[常见问题]是一级目录，其余为二级目录。要求一级目录无内容，仅做目录。</p>
<p>例如：</p>
<pre><code>* [集成总线](//iuap.yonyoucloud.com/doc/exclusive_cloud_instantmessaging.html#/md-build/exclusive_cloud_instantmessaging/articles/esb/1-/)
</code></pre><p>比如一级目录“集成总线”后面不需要加MD文件（如introduction.md内容文件）。</p>
<p>二级目录必须缩进。</p>
<p>5、  必须严格按此格式写目录。</p>
<h2 id="markdown-">Markdown简明语法</h2>
<p>1、标题</p>
<p>类 Atx 形式是在行首插入 1 到 6 个 # ，对应到标题 1 到 6 阶，例如：</p>
<pre><code># 这是 H1

## 这是 H2

###### 这是 H6
</code></pre><p>转换后：</p>
<h1 id="-h1">这是 H1</h1>
<h2 id="-h2">这是 H2</h2>
<h6 id="-h6">这是 H6</h6>
<hr>
<p>2、列表</p>
<p>1）无序列表可以用* ， + ， — 来创建，例如：</p>
<pre><code>* 1
* 2
* 3
</code></pre><p>转换后：</p>
<ul>
<li>1</li>
<li>2</li>
<li>3</li>
</ul>
<p>2）有序列表只有如下这一种方式，注意，数字后面的点只能是英文的点，例如：</p>
<pre><code>
1. 列表1
2. 列表2
3. 列表3

</code></pre><p>转换后：</p>
<ol>
<li>列表1</li>
<li>列表2</li>
<li>列表3</li>
</ol>
<hr>
<p>3、代码框</p>
<p>可以使用右上角的“&lt;&gt;” Code功能，将代码内容包含在“&lt;&gt;”中。</p>
<hr>
<p>4、表格</p>
<p>可以访问：<a href="http://pressbin.com/tools/excel_to_html_table/index.html">http://pressbin.com/tools/excel_to_html_table/index.html</a></p>
<p>进行表格转换。</p>
<p>将表格内容复制到第一个框中，然后点击“Convert”，在Results框中显示转换的结果，直接复制到编辑器即可。</p>
<hr>
<p>5、图片</p>
<p>可以使用右上角“Insert Image”功能。</p>
<hr>
<p>6、题注居中</p>
<p>对于题注需要居中的情况，可以使用如下命令：</p>
<pre><code>&lt;p align=&quot;center&quot;&gt;图1&lt;/p&gt;
</code></pre><p>转换后：</p>
<p align="center">图1</p>























