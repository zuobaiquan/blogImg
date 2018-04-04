# HTML�淶
## �ĵ��淶
ʹ�� HTML5 ���ĵ��������� : <!DOCTYPE html>

1. DOCTYPE��ǩ��һ�ֱ�׼ͨ�ñ�����Ե��ĵ���������������Ŀ����Ҫ���߱�׼ͨ�ñ�����Խ���������Ӧ��ʹ��ʲô�����ĵ����Ͷ��壨DTD���������ĵ���
2. ʹ���ĵ��������͵�������Ϊ�˷�ֹ����������Ĺ���ģʽ��
3. û��DOCTYPE�ĵ����������Ὺ��������Ĺ���ģʽ��������ᰴ���Լ��Ľ�����ʽ��Ⱦҳ�棬�ڲ�ͬ�������������в�ͬ����ʽ��
4. ������ҳ�������<!DOCTYP>��ô����ô�͵�ͬ�ڿ����˱�׼ģʽ��������ᰴ��W3C��׼������Ⱦҳ�档
## �ű�����
˵��js��css��λ�ã����Ӧ�ö�֪��js�������棬css�������档
���ǣ���������Ŀֻ��Ҫ����ie10+����ֻ�����ƶ��˷��ʣ���ô����ʹ��HTML5��������async�����ű��ļ�����<head>��
### �����Ͼ������(IE9-)ʱ��
�ű�����д�� body ������ǩ֮ǰ�������� async ���ԡ�����Ȼ���Ͼ�������в����첽���ؽű�������ֻ������ body ������ǩ֮ǰ�� DOM ��������ʹ�󽵵���������Ӱ�졣
### �����ִ�������У�
�ű����� DOM ���������� body β���� script ��ǩ�Ž��м��أ���ʱ���������첽���أ��������� CSSOM������ִ���Է����� CSSOM ֮�󣩡�
����������
### ������������Ƽ�

```
<html>
<head>
    <link rel="stylesheet" href="main.css">
  </head>
  <body>
      body goes here   
    <script src="main.js" async></script>
  </body>
</html>
```

### ֻ�����ִ�������Ƽ�

 ```
<html>
  <head>
    <link rel="stylesheet" href="main.css">
    <script src="main.js" async></script>
  </head>
  <body>
      body goes here  
  </body>
</html>
```

## ���廯
���廯
����һֱ����˵���廯��̣����廯��̣������ڴ����к���������ȫʹ����ȷ��Ԫ�ء�ʹ�����廯��ǩҲ��������SEO�ġ�

> ���廯��ָ������Ԫ���䱻�������ʱ�ĳ�ʼ������ʹ������
��˼��������ȷ�ı�ǩ����ȷ���£�������ֻ��div��span��

���Ƽ���
```
<b>My page title</b>
<div class="top-navigation">
  <div class="nav-item"><a href="#home">Home</a></div>
  <div class="nav-item"><a href="#news">News</a></div>
  <div class="nav-item"><a href="#about">About</a></div>
</div>
<div class="news-page">
  <div class="page-section news">
    <div class="title">All news articles</div>
    <div class="news-article">
      <h2>Bad article</h2>
      <div class="intro">Introduction sub-title</div>
      <div class="content">This is a very bad example for HTML semantics</div>
      <div class="article-side-notes">I think I'm more on the side and should not receive the main credits</div>
      <div class="article-foot-notes">
        This article was created by David <div class="time">2014-01-01 00:00</div>
      </div>
    </div>
    <div class="section-footer">
      Related sections: Events, Public holidays
    </div>
  </div>
</div>
<div class="page-footer">
  Copyright 2014
</div>
```
�Ƽ���
```
html ����:
<!-- The page header should go into a header element -->
<header>
  <!-- As this title belongs to the page structure it's a heading and h1 should be used -->
  <h1>My page title</h1>
</header>
<!-- All navigation should go into a nav element -->
<nav class="top-navigation">
  <!-- A listing of elements should always go to UL (OL for ordered listings) -->
  <ul>
    <li class="nav-item"><a href="#home">Home</a></li>
    <li class="nav-item"><a href="#news">News</a></li>
    <li class="nav-item"><a href="#about">About</a></li>
  </ul>
</nav>
<!-- The main part of the page should go into a main element (also use role="main" for accessibility) -->
<main class="news-page" role="main">
  <!-- A section of a page should go into a section element. Divide a page into sections with semantic elements. -->
  <section class="page-section news">
    <!-- A section header should go into a section element -->
    <header>
      <!-- As a page section belongs to the page structure heading elements should be used (in this case h2) -->
      <h2 class="title">All news articles</h2>
    </header>
    <!-- If a section / module can be seen as an article (news article, blog entry, products teaser, any other
     re-usable module / section that can occur multiple times on a page) a article element should be used -->
    <article class="news-article">
      <!-- An article can contain a header that contains the summary / introduction information of the article -->
      <header>
        <!-- As a article title does not belong to the overall page structure there should not be any heading tag! -->
        <div class="article-title">Good article</div>
        <!-- Small can optionally be used to reduce importance -->
        <small class="intro">Introduction sub-title</small>
      </header>
 
      <!-- For the main content in a section or article there is no semantic element -->
      <div class="content">
        <p>This is a good example for HTML semantics</p>
      </div>
      <!-- For content that is represented as side note or less important information in a given context use aside -->
      <aside class="article-side-notes">
        <p>I think I'm more on the side and should not receive the main credits</p>
      </aside>
      <!-- Articles can also contain footers. If you have footnotes for an article place them into a footer element -->
      <footer class="article-foot-notes">
        <!-- The time element can be used to annotate a timestamp. Use the datetime attribute to specify ISO time
         while the actual text in the time element can also be more human readable / relative -->
        <p>This article was created by David <time datetime="2014-01-01 00:00" class="time">1 month ago</time></p>
      </footer>
    </article>
 
    <!-- In a section, footnotes or similar information can also go into a footer element -->
    <footer class="section-footer">
      <p>Related sections: Events, Public holidays</p>
    </footer>
  </section>
</main>
 
<!-- Your page footer should go into a global footer element -->
<footer class="page-footer">
  Copyright 2014
</footer>
```

## alt��ǩ��Ϊ��
<img>��ǩ�� alt ����ָ��������ı���������ͼ���޷���ʾ�����û�����ͼ����ʾʱ������ͼ����ʾ��������е����ݡ�
������������ԭ���û��޷��鿴ͼ��alt ���Կ���Ϊͼ���ṩ�������Ϣ��
1. ����̫��
2. src �����еĴ���
3. ���������ͼ��
4. �û�ʹ�õ�����Ļ�Ķ���
��SEO�Ƕȿ��ǣ������������������ͼƬ�����ݣ���������Ҫ�����ָ�������ͼƬ������

## �ṹ�����֡���Ϊ���߷���
�������ĵ���ģ����ֻ�����ṹ�Ե� HTML���������б��ִ��룬������ʽ���У������ж�����Ϊ������ű�֮�С�
�ڴ�֮�⣬Ϊʹ������֮�����ϵ�����ܵ�С�����ĵ���ģ����Ҳ�����ٵ�������ʽ�ͽű��ļ���
���飺

1. ��ʹ�ó���һ��������ʽ��
2. ��ʹ�ó���һ�������ű���ѧ���úϲ��ű���
3. ��ʹ��������ʽ��`<style>.no-good {}</style>`��
4. ����Ԫ����ʹ�� style ���ԣ�`<hr style="border-top: 5px solid black">`��
5. ��ʹ�����ڽű���`<script>alert('no good')</script>`��
6. ��ʹ�ñ���Ԫ�أ�`i.e. <b>, <u>, <center>, <font>, <b>`��
7. ��ʹ�ñ��� class ����`i.e. red, left, center`��
## HTMLֻ��ע����
 1. HTMLֻ��ʾչʾ������Ϣ
 2. ��Ҫ����һЩ�ض��� HTML �ṹ�����һЩ�Ӿ��������
 3. ��Ҫ��imgԪ�ص���ר���������Ӿ���Ƶ�Ԫ��
 4. ��ʽ�ϵ�����Ӧ��ʹ��css���

���Ƽ���
```
<!-- We should not introduce an additional element just to solve a design problem  -->
<span class="text-box">
  <span class="square"></span>
  See the square next to me?
</span>
css ����:
.text-box > .square {
  display: inline-block;
  width: 1rem;
  height: 1rem;
  background-color: red;
}
```
�Ƽ���
```
html ����:
<!-- That's clean markup! -->
<span class="text-box">
  See the square next to me?
</span>
css ����:
/* We use a :before pseudo element to solve the design problem of placing a colored square in front of the text content */
.text-box:before {
  content: "";
  display: inline-block;
  width: 1rem;
  height: 1rem;
  background-color: red;
}
```
### ͼƬ�� SVG ͼ���ܱ����뵽 HTML �е�Ψһ���������ǳ��ֳ�����������ص�һЩ��Ϣ��
���Ƽ�:
```
html ����:
<!-- Content images should never be used for design elements!  -->
<span class="text-box">
  <img src="square.svg" alt="Square" />
  See the square next to me?
</span>
```
�Ƽ���
```
html ����:
<!-- That's clean markup! -->
<span class="text-box">
  See the square next to me?
</span>
css ����:
/* We use a :before pseudo element with a background image to solve the problem */
.text-box:before {
  content: "";
  display: inline-block;
  width: 1rem;
  height: 1rem;
  background: url(square.svg) no-repeat;
  background-size: 100%;
}
```

[��Դ](http://cherryblog.site/developing-guideline.html)