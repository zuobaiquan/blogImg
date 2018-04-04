# js�淶
## ����ȫ�������ռ���Ⱦ
��ֹȫ�������ռ䱻��Ⱦ������ͨ���������ǽ����������һ�� IIFE(Immediately-Invoked Function Expression)���������������Ķ�����Ҳʹ���ڴ���ִ����������ͷš�

IIFE ����ȷ����Ĵ��벻�����ױ�����ȫ�������ռ���Ĵ������޸ģ�i.e. �������⣬window ���ã������ǵ�δ����Ĺؼ��ֵȵȣ���
���Ƽ�:
```
var x = 10, y = 100;
// Declaring variables in the global scope is resulting in global scope pollution. All variables declared like this
// will be stored in the window object. This is very unclean and needs to be avoided.
console.log(window.x + ' ' + window.y);
```
�Ƽ�:
```
// We declare a IIFE and pass parameters into the function that we will use from the global space
(function(log, w, undefined){
  'use strict';
 
  var x = 10,
      y = 100;
 
  // Will output 'true true'
  log((w.x === undefined) + ' ' + (w.y === undefined));
 
}(window.console.log, window));
```
�Ƽ���IIFEд��:
```
(function(){
  'use strict';
 
  // Code goes here
 
}());
```
�����������ȫ�ֱ������������ IIFE �ı���������ͨ�����з�ʽ���Σ�
```
(function($, w, d){
  'use strict';
 
  $(function() {
    w.alert(d.querySelectorAll('div').length);
  });
}(jQuery, window, document));
```
> **IIFEд�������ÿ����������**
`{// Code goes here}`

## �ϸ�ģʽ
ECMAScript 5 �ϸ�ģʽ���������ű�����������ڱ��������Ӧ��ͬ�� javascript �ﾳ���������ϸ�Ĵ����顣�ϸ�ģʽҲȷ���� javascript ������ӵĽ�׳�����е�Ҳ���ӿ��١�
�ϸ�ģʽ����ֹʹ����δ���ܿ��ܱ������Ԥ���ؼ��֡�
��Ӧ������Ľű��������ϸ�ģʽ��������ڶ����� IIFE ��Ӧ��������������Ľű���һ��ʹ����������������нű����������ϸ�ģʽ�����п��ܻ�����һЩ�������������⡣
## ��������
����ʹ�� var �������������粻ָ�� var������������ʽ������Ϊȫ�ֱ���������:
`var a = b = 0; //b�ᱻ��ʽ�Ĵ���Ϊȫ�ֱ���`
���ԣ�������ʹ�� var ����������������ʹ�õ�varģʽ�������еı����ں�����ǰ��ֻʹ��һ��var���壩�����磺
```
(function (){
  'use strict'
  var a = 0,
      b = 0,
      c = 0,
      i,
      j,
      myObject();
}())
```
## js������ǰ
javascript���Զ��������������ڵı����ͷ����Ķ�����ǰ��ֻ����ǰ��������ֵ������ԭ����
���磺
```
(function(log){
  'use strict';
 
  var a = 10;
 
  for(var i = 0; i < a; i++) {
    var b = i * i;
    log(b);
  }
 
  if(a === 10) {
    var f = function() {
      log(a);
    };
    f();
  }
 
  function x() {
    log('Mr. X!');
  }
  x();
 
}(window.console.log));
```
�������js
```
(function(log){
  'use strict';
  // All variables used in the closure will be hoisted to the top of the function
  var a,
      i,
      b,
      f;
  // All functions in the closure will be hoisted to the top
  function x() {
    log('Mr. X!');
  }
 
  a = 10;
 
  for(i = 0; i < a; i++) {
    b = i * i;
    log(b);
  }
 
  if(a === 10) {
    // Function assignments will only result in hoisted variables but the function body will not be hoisted
    // Only by using a real function declaration the whole function will be hoisted with its body
    f = function() {
      log(a);
    };
    f();
  }
 
  x();
 
}(window.console.log));
```
>**ES6�﷨����let��������������**
ʹ���ϸ��
����ʹ�� === ��ȷ�ıȽϲ��������������жϵĹ����У��� JavaScript ��ǿ������ת������ɵ����š����磺
```
(function(log){
  'use strict';
 
  log('0' == 0); // true
  log('' == false); // true
  log('1' == true); // true
  log(null == undefined); // true
 
  var x = {
    valueOf: function() {
      return 'X';
    }
  };
 
  log(x == 'X');
 
}(window.console.log));
```
## ��ͬ== ���ϸ��===������
1. ==�� ����ֵ���Ͳ�ͬ��ʱ��Ҫ�Ƚ�������ת�����ٱȽϡ�
2. ===����������ת�������Ͳ�ͬ��һ�����ȡ�

==��ͬ������
1. �������ֵ������ͬ���ͣ������===�Ƚϣ�����===�ıȽ�ֵ
2. �������ֵ��������ͬ���ͣ�Ҳ�п��ܷ���true
3. ���һ��ֵ��null��һ��ֵ��undefined������true
4. ���һ��ֵ��string�����number�����stringת����number�ٽ��бȽ�
5. ���һ��ֵ��true�������ת��1�ٱȽϣ�false��ת��0
```
console.log( false == null )      // false
console.log( false == undefined ) // false
console.log( false == 0 )         // true
console.log( false == '' )        // true
console.log( false == NaN )       // false
 
console.log( null == undefined ) // true
console.log( null == 0 )         // false
console.log( null == '' )        // false
console.log( null == NaN )       // false
 
console.log( undefined == 0)   // false
console.log( undefined == '')  // false
console.log( undefined == NaN) // false
 
console.log( 0 == '' )  // true
console.log( 0 == NaN ) // false
```
�ܽ�һ��==

1. false ���˺�����Ƚ�Ϊ true �⣬�� 0������ �Ƚ�ҲΪ true
2. null ֻ�� undefined �Ƚ�ʱΪ true�� ������ undefined Ҳ���� null �Ƚ�Ϊ true��û�еڶ���
3. 0 ���˺� false �Ƚ�Ϊ true�����п��ַ��� ������ �Ϳ����� []
4. ���ַ��� ���� ���˺� false �Ƚ�Ϊ true������һ������ 0
>==, >, <, +, -, �� ��Щ����������ɵ���ʽ����ת�������޸����õģ�������ı�����������ֵ�������ǣ�����㸲дĳ������� valueOf/toString�Ļ���==�ͻ����������.
���磺
```
Array.prototype.valueOf = function() {
  this[0]++;
  return this;
}
var x = [1, 2, 3];
x == 0;
console.log(x);   // [2, 2, 3]
```
===��������

1. Ҫ������ֵ���Ͳ�ͬ������false
2. Ҫ������ֵ����number���ͣ�������ֵ��ͬ������true
3. Ҫ������ֵ����stirng����������ֵ��String������ͬ������true
4. Ҫ������ֵ����true���߶���false������true
5. Ҫ������ֵ����ָ����ͬ��Object��Arraya����function������true
6. Ҫ������ֵ����null���߶���undefined������true
## ����ж�
js����������Ϊ�٣�
false
null
undefined
0
���� (���ַ���)
NaN

## ����Ĭ�ϲ���
�������� || �� && Ҳ�ɱ��������ز���ֵ�������������Ϊ�ǲ���������ÿ�����ʽ���ᱻ�������ҵ�������жϡ����ڴ˲�������������һ�����ʽ�����ػ��������ڱ�����ֵʱ���ǿ�����������Ĵ���ġ�����:���x��������y�����ڣ�x=1�����x����y���ڣ�x = y
```
if(!x) {
  if(!y) {
    x = 1;
  } else {
    x = y;
  }
}
```
��ͬ��
`x = x || y || 1;`
��һС���ɾ��������������趨Ĭ�ϵĲ�����
```
(function(log){
  'use strict';
 
  function multiply(a, b) {
    a = a || 1;
    b = b || 1;
 
    log('Result ' + a * b);
  }
 
  multiply(); // Result 1
  multiply(10); // Result 10
  multiply(3, NaN); // Result 3
  multiply(9, 5); // Result 45
 
}(window.console.log));
```
## ��ʹ��eval()����
����eval��������˼��˵����ħ��ʹ��eval()�����������ȫ������
eval()�����������Ƿ��������ַ���������js����������

## this�ؼ���
ֻ�ڶ������������������趨�ıհ���ʹ�� this �ؼ��֡�this �������ڴ���Щ�󵼡���ʱ��ָ��ȫ�ֶ��󣨴����ʱ����ʱ��ָ������ߵĶ������� eval �У���ʱ��ָ�� DOM ���е�ĳһ�ڵ㣨�����¼�����󶨵� HTML ������ʱ����ʱ��ָ��һ���´����Ķ����ڹ������У�����ʱ��ָ��������һЩ������������� call() �� apply() ִ�к͵���ʱ����

����Ϊ����������׵ر��������������ʹ�ó�����
>�ڹ��캯����
�ڶ���ķ����У������ɴ˴������ıհ��ڣ�

## ��ѡ����ʽ���
����ʽ���������Լ򻯴��벢����ά���ɱ�����Ϊ�����׸��ã����ʵ��ؽ���͸��ٵ�������
�������������У���һ��������͵�ͬһ�����ϣ��Ƚ������ֽ����������һ�������Ǿ���ĳ��������ڶ����������ǲ����˺���ʽ��̺� ECMA Script 5.1 �����鷽����
���Ƽ�
```
(function(log){
  'use strict';
  var arr = [10, 3, 7, 9, 100, 20],
        sum = 0,
         i; 
  for(i = 0; i < arr.length; i++) {
    sum += arr[i];
  } 
  log('The sum of array ' + arr + ' is: ' + sum) 
}(window.console.log));
```
�Ƽ�(����ʽ���)��
```
(function(log){
  'use strict';
  var arr = [10, 3, 7, 9, 100, 20];
  var sum = arr.reduce(function(prevValue, currentValue) {
    return prevValue + currentValue;
  }, 0);
  log('The sum of array ' + arr + ' is: ' + sum);
}(window.console.log));
```
## �޸��ڽ������ԭ����
�޸��ڽ������� Object.prototype �� Array.prototype �Ǳ�������ֹ�ġ��޸��������ڽ�������� Function.prototype����Σ��û��ô�󣬵�ʼ�ջ��ǻᵼ���ڿ������������� debug �����⣬Ӧ��ҲҪ���⡣

## ��Ԫ�����жϣ�if �Ŀ�ݷ�����
����Ԫ����������򷵻���䡣�ڱȽϼ򵥵������ʹ�ã������ڸ��ӵ������ʹ�á�û��Ը���� 10 ����Ԫ���������Լ����������Ρ�
���Ƽ���
```
if(x === 10) {
  return 'valid';
} else {
  return 'invalid';
}
```
�Ƽ���
`return x === 10 ? 'valid' : 'invalid'`

# JSHint
��js�淶�У��кܶ�淶������ʽ�ϵĹ淶�������߼��ϵĹ淶�����羡��ʹ��===������==�����ǿ���ʹ��JSHint����JSLint��Javascript������֤���ߣ����ֹ��߿��Լ����Ĵ��벢�ṩ��صĴ���Ľ�������Ҹ���ʹ�õ���JSHint�����Ծ������Ϊ��:
ESLint ��vscode�༭���� �
1. ����vscode�а�װESlint ,����չ������eslint���Ұ�װ
![image](https://user-images.githubusercontent.com/9931345/35262799-1bff78c2-0051-11e8-8fa4-753a547721a9.png)

2. ��װ��ɺ���ն˿���̨����һ������
>npm i eslint -g          //��ȫ�ְ�װeslint
>cd yourDocumentPath      //��������ļ�Ŀ¼
> eslint --init        //��ʼ��eslint 
![image](https://user-images.githubusercontent.com/9931345/35262814-36e9c390-0051-11e8-9303-8826f7cf7399.png)

����ʹ�ã� ����ȥeslint�������ݾ���������ö�.eslintrc.json �������� 
![image](https://user-images.githubusercontent.com/9931345/35262780-0c64df10-0051-11e8-8457-c50649435ebc.png)

��Щ�淶����ʲô��˼�أ������г�һЩ���õģ�ʣ�µĴ�ҿ��Բο�[�ٷ��ĵ�](http://jshint.com/docs/)


|����    | ����    |
|------|--------|
|curly | ѭ����������������ʹ�û����Ű�ס  |
|eqeqeq | ʹ��ǿ�Ƶ�===  |
|newcap | ��������ĸ��д�ĺ������������ࣩ��ǿ��ʹ��new  |
|noarg | ����arguments.caller��arguments.callee  |
|sub | ��������ʹ��aaa.bbb������aaa[��bbb��]  |
|undef | ��������δ����ı���  |
|boss | ����������if(a = 0)�����Ĵ���  |
|node | ָ�����л���Ϊnode  |
|strict | ����ʹ���ϸ�ģʽ  |
|asi | ����ʡ�Էֺ�  |
|bitwise | ��ֹʹ��λ����������羭����&&д��& ��ܴ˴���  |
|jquery | ����ȫ�ֱ�¶��jQuery��  |
|evil | ��ֹʹ��eval  |
|maxdepth | Ƕ�׵�������  |
|maxparams | ������������  |



[��Դ](http://cherryblog.site/developing-guideline.html)