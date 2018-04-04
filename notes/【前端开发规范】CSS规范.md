# css�淶
## id��class������
ID��class����������ʹ�ÿ��Է�ӦԪ��Ŀ�ĺ���;�����ƣ�������ͨ�õ����ƣ��������ͻ�ɬ�Ѷ�������
���Ƽ� :
```
.fw-800 {
  font-weight: 800;
}
.red {
  color: red;
}
```
�Ƽ� :
```
.heavy {
  font-weight: 800;
}
 
.important {
  color: red;
}
```
## �����ʹ��ID
һ�������ID��Ӧ�ñ�������ʽ������ID��Ȩ�غܸߣ����Բ�ʹ��ID�����ʽ�����⣬����ʹ��class

���Ƽ���
```
#content .title {
  font-size: 2em;
}
```
�Ƽ���
```
.content .title {
  font-size: 2em;
}
```
>����֮���Բ���������ʹ�ã�����ΪID�����ȼ��Ƚϸߣ�
����ʽ�����ϻᵼ�º����������ʽ����������ʽ�ļ���ʹ��ʧЧ��

## cssѡ�����б���ʹ�ñ�ǩ��
�ӽṹ�����֡���Ϊ�����ԭ��������Ӧ�þ�������css�г���HTML��ǩ��������cssѡ�����г��ֱ�ǩ�������Ǳ�ڵ����⡣

## ʹ����ѡ����
�ܶ�ǰ�˿�����Աдѡ��������ʱ��ʹ�� ֱ����ѡ������ע��ֱ����ѡ�����ͺ��ѡ���������𣩡�
��ʱ������ܻᵼ����ʹ��������Ⲣ����ʱ����ܻ�ܺ����ܡ�
Ȼ�������κ�����£�����һ���ǳ����õ�������
����㲻д��ͨ�õģ���Ҫƥ�䵽DOMĩ�˵�ѡ������ ��Ӧ�����ǿ���ֱ����ѡ������

���Ƽ�:
```
.content .title {
  font-size: 2rem;
}
```
�Ƽ���
```
.content > .title {
  font-size: 2rem;
}
```
## ����ʹ����д����
����ʹ����д���Զ��ڴ���Ч�ʺͿɶ����Ǻ����õģ�����font���ԡ�

���Ƽ���
```
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;
```
�Ƽ���
```
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
```
>ע�⣺0���治����λ

## ���Ը�ʽ
1. Ϊ�˱�֤һ���ԺͿ���չ�ԣ�ÿ������Ӧ���÷ֺŽ�����ÿ���������С�
2. ��������ð�ź�ʹ��һ���ո񡣳���һ���Ե�ԭ��
3. ���Ժ�ֵ�������Ժ�ð��֮��û�пո񣩵�֮��ʼ��ʹ��һ���ո�
4. ÿ��ѡ������������������ʹ���µ�һ�С�
5. ����ѡ����������ֵ��˫���ţ��������������ǵ����ţ�������������
6. URIֵ��url()����Ҫʹ�����š�

��Ϊ���ʵ��������Ӧ����ѭ����˳��Ӧ�ð����±��˳�򣩣�

�ṹ�����ԣ�
 1. display
 2. position, left, top, right etc.
 3. overflow, float, clear etc.
 4. margin, padding

���������ԣ�
  1. background, border etc.
  2. font, text

���Ƽ���
```
.box {
  font-family: 'Arial', sans-serif;
  border: 3px solid #ddd;
  left: 30%;
  position: absolute;
  text-transform: uppercase;
  background-color: #eee;
  right: 30%;
  isplay: block;
  font-size: 1.5rem;
  overflow: hidden;
  padding: 1em;
  margin: 1em;
}
```
�Ƽ���
```
.box {
  display: block;
  position: absolute;
  left: 30%;
  right: 30%;
  overflow: hidden;
  margin: 1em;
  padding: 1em;
  background-color: #eee;
  border: 3px solid #ddd;
  font-family: 'Arial', sans-serif;
  font-size: 1.5rem;
  text-transform: uppercase;
}
```

������£�

[ǰ�˱���淶](http://www.css88.com/archives/5505)
[JavsScript�����淶](http://www.cnblogs.com/polk6/p/4660195.html) 
[�����淶���ģ�JS�淶](https://segmentfault.com/a/1190000006131512)


[��Դ](http://cherryblog.site/developing-guideline.html)