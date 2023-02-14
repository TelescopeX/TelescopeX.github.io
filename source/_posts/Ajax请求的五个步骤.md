---

title: Ajax请求的五个步骤
---
  * ——Ajax简介——：ajax即异步 JavaScript 和XML。Ajax是一种用于创建快速动态网页的技术。通过在后台与服务器进行少量数据交换，Ajax可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。而传统的网页(不使用 Ajax)如果需要更新内容，必需重载整个网页面。
  
  * ajax的工作原理：客户端发送请求，请求交给xhr，xhr把请求提交给服务，服务器进行业务处理，服务器响应数据交给xhr对象，xhr对象接收数据，由javascript把数据写到页面上
### 实现AJAX的基本步骤：

* 要完整实现一个AJAX异步调用和局部刷新,通常需要以下几个步骤:

1. 创建XMLHttpRequest对象,即创建一个异步调用对象。
2. 创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息。
3. 设置响应HTTP请求状态变化的函数。
4. 发送HTTP请求。
5. 获取异步调用返回的数据。
6. 使用JavaScript和DOM实现局部刷新。

### 一.创建XMLHttpRequest对象

1. 不同浏览器使用的异步调用对象有所不同，在IE浏览器中异步调用使用的是XMLHTTP组件中的XMLHttpRequest对象，而在Netscape、Firefox浏览器中则直接使用XMLHttpRequest组件。因此，在不同浏览器中创建XMLHttpRequest对象的方式都有所不同。

* 在IE浏览器中创建XMLHttpRequest对象的方式为:
 var xmlHttpRequest = new ActiveXObject("Microsoft.XMLHTTP");

* 在Netscape浏览器中创建XMLHttpRequest对象的方式为:

var xmlHttpRequest = new XMLHttpRequest();

**由于无法确定用户使用的是什么浏览器,所以在创建XMLHttpRequest对象时,最好将以上两种方法都加上.如以下代码所示:**

 ```ruby
 var xmlHttpRequest;  //定义一个变量,用于存放XMLHttpRequest对象
    createXMLHttpRequst();   //调用创建对象的方法
    //创建XMLHttpRequest对象的方法 
    function createXMLHttpRequest(){                                                 
        if(window.ActiveXObject) {//判断是否是IE浏览器
            xmlHttpRequest = new ActiveXObject("Microsoft.XMLHTTP");//创建IE的XMLHttpRequest对象
        }else if(window.XMLHttpRequest){//判断是否是Netscape等其他支持XMLHttpRequest组件的浏览器
            xmlHttpRequest = new XMLHttpRequest();//创建其他浏览器上的XMLHttpRequest对象
        }
    } 
 ```
  

1. "if(window.ActiveXObject)"用来判断是否使用IE浏览器.其中ActiveXOject并不是Windows对象的标准属性,而是IE浏览器中专有的属性,可以用于判断浏览器是否支持ActiveX控件.通常只有IE浏览器或以IE浏览器为核心的浏览器才能支持Active控件.

2. "else if(window.XMLHttpRequest)"是为了防止一些浏览器既不支持ActiveX控件,也不支持XMLHttpRequest组件而进行的判断.其中XMLHttpRequest也不是window对象的标准属性,但可以用来判断浏览器是否支持XMLHttpRequest组件.

3. 如果浏览器既不支持ActiveX控件,也不支持XMLHttpRequest组件,那么就不会对xmlHttpRequest变量赋值.
### 二.创建HTTP请求

1. 创建了XMLHttpRequest对象之后，必须为XMLHttpRequest对象创建HTTP请求，用于说明XMLHttpRequest对象要从哪里获取数据。通常可以是网站中的数据,也可以是本地中其他文件中的数据。
__创建HTTP请求可以使用XMLHttpRequest对象的open()方法,其语法代码如下所示:__

* method：该参数用于指定HTTP的请求方法，一共有get、post、head、put、delete五种方法，常用的方法为get和post。

* URL：该参数用于指定HTTP请求的URL地址，可以是绝对URL，也可以是相对URL。

* flag：该参数为可选，参数值为布尔型。该参数用于指定是否使用异步方式。true表示异步、false表示同步，默认为true。

* name：该参数为可选参数，用于输入用户名。如果服务器需要验证，则必须使用该参数。

* password：该参数为可选，用于输入密码。若服务器需要验证，则必须使用该参数。

1. 通常可以使用以下代码来访问一个网站文件的内容。      

xmlHttpRequest.open("get","http://www.aspxfans.com/BookSupport/JavaScript/ajax.htm",true);

3. 或者使用以下代码来访问一个本地文件内容：

xmlHttpRequest.open("get","ajax.htm",true);

* 注意：如果HTML文件放在Web服务器上，在Netscape浏览器中的JavaScript安全机制不允许与本机之外的主机进行通信。也就是说，使用open()方法只能打开与HTML文件在同一个服务器上的文件。而在IE浏览器中则无此限制（虽然可以打开其他服务器上的文件，但也会有警告提示）。

### 三.设置响应HTTP请求状态变化的函数

1. 创建完HTTP请求之后，应该就可以将HTTP请求发送给Web服务器了。然而，发送HTTP请求的目的是为了接收从服务器中返回的数据。从创建XMLHttpRequest对象开始，到发送数据、接收数据、XMLHttpRequest对象一共会经历以下5中状态。
2. 
* 未初始化状态。在创建完XMLHttpRequest对象时，该对象处于未初始化状态，此时XMLHttpRequest对象的readyState属性值为0。
* 初始化状态。在创建完XMLHttpRequest对象后使用open()方法创建了HTTP请求时，该对象处于初始化状态。此时XMLHttpRequest对象的readyState属性值为1。
* 发送数据状态。在初始化XMLHttpRequest对象后，使用send()方法发送数据时，该对象处于发送数据状态，此时XMLHttpRequest对象的readyState属性值为2。
* 接收数据状态。Web服务器接收完数据并进行处理完毕之后，向客户端传送返回的结果。此时，XMLHttpRequest对象处于接收数据状态，XMLHttpRequest对象的readyState属性值为3。
* 完成状态。XMLHttpRequest对象接收数据完毕后，进入完成状态，此时XMLHttpRequest对象的readyState属性值为4。此时接收完毕后的数据存入在客户端计算机的内存中，可以使用responseText属性或responseXml属性来获取数据。

3. 只有在XMLHttpRequest对象完成了以上5个步骤之后，才可以获取从服务器端返回的数据。因此，如果要获得从服务器端返回的数据，就必须要先判断XMLHttpRequest对象的状态。

4. XMLHttpRequest对象可以响应readystatechange事件，该事件在XMLHttpRequest对象状态改变时（也就是readyState属性值改变时）激发。因此，可以通过该事件调用一个函数，并在该函数中判断XMLHttpRequest对象的readyState属性值。如果readyState属性值为4则使用responseText属性或responseXml属性来获取数据。具体代码如下所示：

    //设置当XMLHttpRequest对象状态改变时调用的函数，注意函数名后面不要添加小括号
    xmlHttpRequest.onreadystatechange = getData;
     
    //定义函数
    function getData(){
        //判断XMLHttpRequest对象的readyState属性值是否为4，如果为4表示异步调用完成
        if(xmlHttpRequest.readyState == 4) {
            //设置获取数据的语句
        }
    }

### 四.设置获取服务器返回数据的语句

1. 如果XMLHttpRequest对象的readyState属性值等于4，表示异步调用过程完毕，就可以通过XMLHttpRequest对象的responseText属性或responseXml属性来获取数据。

2. 但是，异步调用过程完毕，并不代表异步调用成功了，如果要判断异步调用是否成功，还要判断XMLHttpRequest对象的status属性值，只有该属性值为200，才表示异步调用成功，因此，要获取服务器返回数据的语句，还必须要先判断XMLHttpRequest对象的status属性值是否等于200，
  __如以下代码所示：__
```ruby
     if(xmlHttpRequst.status == 200) {
        document.write(xmlHttpRequest.responseText);//将返回结果以字符串形式输出
        //document.write(xmlHttpRequest.responseXML);//或者将返回结果以XML形式输出
     }
```
3. 注意：如果HTML文件不是在Web服务器上运行，而是在本地运行，则xmlHttpRequest.status的返回值为0。因此，如果该文件在本地运行，则应该加上xmlHttpRequest.status == 0的判断。

__通常将以上代码放在响应HTTP请求状态变化的函数体内，如以下代码所示__       
```ruby
    //设置当XMLHttpRequest对象状态改变时调用的函数，注意函数名后面不要添加小括号
    xmlHttpRequest.onreadystatechange = getData;
     
    //定义函数
    function getData(){
        //判断XMLHttpRequest对象的readyState属性值是否为4，如果为4表示异步调用完成
        if(xmlHttpRequest.readyState==4){
            if(xmlHttpRequest.status == 200 || xmlHttpRequest.status == 0){//设置获取数据的语句
                document.write(xmlHttpRequest.responseText);//将返回结果以字符串形式输出
                //docunment.write(xmlHttpRequest.responseXML);//或者将返回结果以XML形式输出
            }
        }
    }
```
### 五.发送HTTP请求

1. 在经过以上几个步骤的设置之后，就可以将HTTP请求发送到Web服务器上去了。发送HTTP请求可以使用XMLHttpRequest对象的send()方法。
 
___ 其语法代码如下所示：__

XMLHttpRequest.send(data);

2. 其中data是个可选参数，如果请求的数据不需要参数，即可以使用null来替代。data参数的格式与在URL中传递参数的格式类似，以下代码为一个send()方法中的data参数的示例：

name=myName&value=myValue

3. 只有在使用send()方法之后，XMLHttpRequest对象的readyState属性值才会开始改变，也才会激发readystatechange事件，并调用函数。
### 六.局部更新
1. 在通过Ajax的异步调用获得服务器端数据之后，可以使用JavaScript或DOM来将网页中的数据进行局部更新。
  


