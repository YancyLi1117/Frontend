# JavaScript Tutorial

## 1.1 Something special

### JavaScript Where to

`<script>...</script> or <script src=....js"></script>`
**不能使用自闭合模式!**

### Output

Writing into an HTML element, using innerHTML.
Writing into the HTML output using document.write().
Writing into an alert box, using window.alert().
Writing into the browser console, using console.log().

### Equal to

==: equal, if not the same type but the same value, still true
===: absolute equal

## 1.2 Data types

numbers: can be float (compare by abs(a1-a2)<0.000001)or integer
bool: true, false
special: NaN===NaN :false, so use isNaN to
null and undefined

### String

over the line:use "" ,'',``(over line)
**can't change the value!** only use the function
some functions: str.length(),
str.substring(start,end) [start,end),
str.replace(a,b):does not change the string, returns a new string.
str.touppercase()/tolowercase()
str.trim() :removes whitespace
str.concat(b) : same as +
str.indexof(b) : return the loc tempelete:

```javascript
let firstName = "John";
let lastName = "Doe";
let text = Welcome `${firstName}, ${lastName}`!;
```

### array

arr=[1,2,3,4] arr[5]:undefined
arr.tostring()/join("-")
arr.pop(),arr.push()
arr.shift() arr.unshift(): delete the first element and move forward
arr.delete() will left a undefined hole
arr.sort()
arr.reverse()

### object

`person={name:"hello", age:19, gender:male}` person.name> hello
xxx in xxx

### Date

```javascript
var now = new Date();
now.getFullYear()/getMonth()...
now.getTime(); //time stamp

time = new Date(352748254858);
console.log(time); //timestamp to time
time.toLocalString() //a method, to time
time.toGMTString() //to GMT time
```

### map and set

map: number can be the key (object can't), like python dict
set: key is disorder, but unrepeatable, don't store value

```javaScript
//map
var map =new Map([['tom',100],['jack',90],['haha',80]]);
var name =map.get('tom'); //get value from key
map.set('admin',1234); //modify or add
map.delete('tom');  //delete
//traverse
for (let x of map){
    console.log(x)
}

//set
var set = new Set([1, 2, 3, '3']);
set.add(4); //add an element
set.delete(2); //delete an element
console.log(set.has(3)); //if has element 3
//traverse
for (let x of set){
    console.log(x)
}
```

### traverse the element

the diff between for in and for of:
https://zhuanlan.zhihu.com/p/142323221

```javascript
var age= [12,3,21,34,5,6,23];

//forEach function
age.forEach(function (value)){
    console.log(value)
})

//for ..in method
for (var index in age){
    if (age.hasOwnProperty(index)){
        console.log("exist")
        console.log(age[index])
    }
}

//for... of method
for(var index of age){
    console.log(index)
}
```

traverse the map and set: use for...of

### Json

a text format for storing and transporting data, value cannot be **function, date, undefined**, string with ""
diff with js object

```javascript
var jsobj = { a: "hello", b: "hellob" }; //can unflod in the console
var json = '{a:"hello",b:"hellob"}';
// can convert object to json
var obj2str = JSON.stringify(jsobj);
// convert json string to object
var str2obj = JSON.parse(json);
```

## 1.3 Declaring a variable

if just declare but don't give a value, is undefined

### var

don't begin with number, the scope is just like java int/char...

### let

Variables defined with let cannot be Redeclared, must be Declared before use, have Block Scope.
You can use the variable before it is declared,but using a **let** variable before will result in a ReferenceError.

### const

Variables defined with const cannot be Redeclared/Reassigned, and have Block Scope.
must be **assigned a value** when they are declared

### strict mode

begin with "use strict"; in the function or script, but **don't merge the code with sloop mode and strict mode**

## 1.4 Function

### Define a function

```javascript
// if don't implete return, also return, but undefined
function abs(x) {
  if (x >= 0) {
    return x;
  } else {
    return -x;
  }
}
// the same as above, annonymose function
var abs = function (x) {
  if (x >= 0) {
    return x;
  } else {
    return -x;
  }
};
```

but the function parameters don't declare the type, and won't report error
use typeof to throw a exception
`if (typeof x !=='number'{throw 'not a number';}`
and the function don't declare the number of parameters, for the more parameters, use **arguments** to find them

```javascript
var abs = function (x) {
  for (var index = 0; i < arguments.length; i++) {
    console.log(argument[i]);
  }
  if (x >= 0) {
    return x;
  } else {
    return -x;
  }
};
```

but still not so convenient, use **...rest**

```javascript
function aaa(a, b, ...rest) {
  console.log(a);
  console.log(b);
  console.log(rest);
}
```

## 2.1 Object oriented, prototype inheritance

### Method

for a object, there are **property** and **method** in it. Method is only function in the object, and recalling the method should use()

```javascript
var student = {
  name: "student",
  birth: 2000,
  age: function () {
    var now = new Date().getFullYear();
    return now - this.birth;
  },
};
student.name; //recall the property
student.age(); //recall the method
getAge(); //NaN, beceuse this point to window, and window have no getAge method
```

### This

like the pointer in C++, in js we can use **apply** to control where it points

```javascript
function getAge(){
    var now = new Date().getFullYear();
    return now - this.birth;
}

var student={
    name: "student",
    birth: 2000,
    age: getAge
};
getAge.apply(student.[]); //this point to student, with no parameter
```

### Arrow function

```javascript
//before
hello = function () {
  return "Hello World!";
};
//use arrow function
hello = () => {
  return "Hello World!";
};
//or
hello = () => "Hello World!";
```

### Prototype

```javascript
//Student is the prtotype object
var Student={
    name:"name",
    age:18,
    run:function(){
        console.log(this.name+"is running");
    }
var xiaoming = {
    name="xiaoming"
};
//do the inheritage
xiaoming.__proto__ =Student; //age, run is the same with proto


}
```

## 2.2 Object oriented, class inheritance

before ES6:

```javascript
fuction student(name){
    this.name =name;
}
// add a method to student
student.prototype.hello = function(){
    alert('hello')
};
```

That is not so good. so in ES6 we always use class

```javascript
class student {
  constructor(name) {
    this.name = name;
  }
  hello() {
    alert("hello");
  }
}
// college inheritage student
class college extends student {
  constructor(name, grade) {
    super(name);
    this.grade = grade;
  }
  myGrade() {
    alert("a college student");
  }
}
var xiaoming = new student("xiaoming");
var xiaohong = new college("xiaohong", 89);
```

## 3.1 DOM element

window: website window

```javascript
window.innerHeight;
window.innerWidth;
window.outerHeigh;
window.outerWidth;
```

navigator:maybe modify by some one, don't use it

```javascript
navigator.appName;
navigator.appVersion;
navigator.userAgent;
navigator.platform;
```

location: the url present, has the property: host, href, protocol, reload
`location.assign('www.baidu.com')`
document:the present page, will mention after
`document.cookie`
history: the browser history
`history.back()/forward()`

## 3.2 DOM HTML

the website is a tree

### Get a DOM node

```javascript
// with css
var h1 = document.getElementsByTagName("h1");
var p1 = document.getElementsById("p1");
var cn = document.getElementsByClassName("cn");
var father = document.getElementsById("father");

var children = father.children; //get all the children of father
father.firstChild / lastChild;
```

### update the DOM node

```javascript
var id1 = document.getElementsById("id1");
id1.innerText = "12345"; //modify the text
id1.innerHTML = "<strong>123</strong>"; // pharse the HTML

id1.style.color = "yellow"; //modify the css
```

### Add a DOM node

add an element

```HTML
<p id ="js"> JavaScript</p>
<div id="list">
    <p id ="se"> JavaSE</p>
    <p id="ee"> JavaEE </p>
    <p id="me"> JavaME</p>
</div>
<script>
    var js=document.getElementsById('js');
    var list= document.getElementById('list');
    list.appendChild(js);
</script>
```

insert a new lable

```HTML
<script>
    var js=document.getElementsById('js');
    var list= document.getElementById('list');

    //add a new <p>
    var newP =document.createElement('p');
    newP.id='newP';
    newP.innerText='Hello';
</script>
```

### Delete DOM node

get the father node and then delete the child from father

```HTML
<div id ="father">
    <h1>head1</h1>
    <p id="p1">p1</p>
    <p class"p2"> p2</p>
</div>
<script>
    var self=document.getElementsById('p1');
    var father =p1.parentElement;
    father.removeChild(self);
    //mention: the index of children changes
    father.removeChild(father.children[0]);
</script>
```

## 3.3 DOM Event

onchange An HTML element has been changed
onclick The user clicks an HTML element
onmouseover The user moves the mouse over an HTML element
onmouseout The user moves the mouse away from an HTML element
onkeydown The user pushes a keyboard key
onload The browser has finished loading the page

## 3.4 DOM Form

use the form post to pass the value

```HTML
<form action="post">
    <p>
        <span> user name:</span><input type="text" id="username">
    </p>

    <p>
        <span>gender</span>
        <input type="radio" name="gender" value="male" id="man"> male
        <input type="radio" name="gender" value="female" id="woman"> female
    </p>
</form>
<script>
    var name=document.getElementsById('username');
    var man=document.getElementsById('man');
    var women=document.getElementsById('woman');

    name.value; //get the username
    name.value="hello"; //modify the value of username

    man.checked; //the radio is checked, true or false
</script>
```

use the button on click to pass value, and use md5 to encrypt

```HTML
<form action="http://www.baidu.com" method="post">
    <p>
        <span> user name:</span><input type="text" id="username">
    </p>

    <p>
        <span>password</span>
        <input type= "password" id ="pwd">
    </p>
    <button type="submit" onclick="aaa()"> submit</button>
</form>
<script>
    fuction aaa(){
        var name=document.getElementsById('username');
        var pwd=document.getElementsById('pwd');

        //use md5 to encrypt
        pwd.value=md5(pwd.value);
    }
</script>
```

check the pwd, and encrypt

```HTML
<form action="http://www.baidu.com" method="post" onsubmit="return aaa()">
    <p>
        <span> user name:</span><input type="text" id="username">
    </p>

    <p>
        <span>password</span>
        <input type= "password" id ="pwd">
    </p>
    <!--use a hidden element to increase the safty -->
    <input type="hidden" id="md5pwd" name="pwd">
    <button type="submit"> submit</button>
</form>
<script>
    fuction aaa(){
        var name=document.getElementsById('username');
        var pwd=document.getElementsById('pwd');
        var md5pwd=document.getElementsById('md5pwd');

        //use md5 to encrypt
        md5pwd.value=md5(pwd.value);
        return true;
    }
</script>
```

test

