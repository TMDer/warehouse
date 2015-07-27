## Engineer questionare

### what is this

```
Version Control System
It can let you modify your code with your team more easier than before.
Example:
When you change your workspace you can use "clone" to copy all data about your project to the workspace you are using from cloud database.
When you add a new team you can use "fork" the project for other cloud database to copy it to your personal cloud database.
After you edit some thing,you can use "push" to upload code to cloud database,you also can use "pull" to copy new version code to your workspace.The different function in "pull & clone" is "pull" don't download all version code,it only download the latest version.
If you are a third party programer,you can use "pull request" to requset the project owner to integrate your code to his/her cloud database.

My github:https://github.com/stevekevin1005
It has some project for Android.

```

### what difference are apply, call, bind?

```
"apply","call" and "bind" do same thing,they can change the target's inter pointer("this").
example1:

<script type="text/javascript" language="JavaScript">
var x = 1;
var y = { x: 2 };
 
function f(){
    alert(this.x);
}
f.call();//1
f.call(y);//2
</script>

Their different thhig is at the second parameters.
"call" input the parameters one by one.
"apply" input the parameters array;
example2(modify from example1):

<script type="text/javascript" language="JavaScript">
var x = 1;
var y = { x: 2 };
 
function f(a,b){
    alert(this.x+a+b);
}
f.call(y,1,2);//5
f.apply(y,[1,2]);//5
</script>

"call" and "apply call the correspondence function immediately but "bind" not,It produce a new fuction.
example3(modify from example2):

<script type="text/javascript" language="JavaScript">
var x = 1;
var y = { x: 2 };
 
function f(a,b){
    alert(this.x+a+b);
}

var useBind = f.bind(y,1,2); //the parameters is like "call"
useBind();//5
</script>

```

### please write a function can execute like

```js
console.log(add(2,3)); // logs 5
console.log(add(2)(3)); // logs 5
```
```
function add(a,b){
    
	if(b==null){
		return function(b){
			return a+b;
		};
	}
	return a+b;
}
```



### please explain css style priority

```
in elemeny > in style > link > import
example:
<div style="color:White"><div> 
VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV

<style type="text/css">
    div { color: White; }
</style>                       

VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV

<link href="myStyle.css" rel="stylesheet" type="text/css" />

VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV

<style type="text/css">
    @import url("myStyle.css");
</style>

```

### please explain inline mode, block mode of css

```
inline:
All elements in a line,height,margin can't change. The width is the width of image or text;
blocK:
Always begin on a new line,height,margin can change. The width initial set is width of the container,it can change.

```

### please introduce ORM, what is different between SQL select?

```
I don't learn it before,so I google it.
It seems as a tool let us can us database easier.
It hide the detail of data access and let us not to consider SQL code to develop.
If we need to shift database we only need to modify relation mapping.
But some efficacy will be discarded and It not easy to do Complex queries
```

### please explain right join, left join and inner join.

```
inner join: choose data by set condition  in between two data sheet
left join: choose data include all data from lefr data sheet by set condition  in between two data sheet (if not confirm confition than return null)
right join: choose data include all data from right data sheet by set condition  in between two data sheet(if not confirm confition than return null)

examle:
data sheet:ex1
id name phone
1 Tony  12345678
3 Kevin 1234567
data sheer:ex2
id  home
1   tw
2   hk

(inner join)
SELECT a.name, b.home * FROM `ex1` as a INNER JOIN `ex2` as b where a.id = b.id

result:
name home
Tony tw

(left join)
SELECT a.name, b.home * FROM `ex1` as a LEFT JOIN `ex2` as b where a.id = b.id
name home
Tony tw
Kevin

(right join)
SELECT a.name, b.home * FROM `ex1` as a Right JOIN `ex2` as b where a.id = b.id
name hone
Tony tw
     hk
```

### what is your favorite SQL and why?

```
mySQL
If i want to copy it,it's easy.
I learn it the longest.
It provide flexible interface.
It take network load lower.
```

### how will you implement a API server? and if it should be connect via facebook, twitter data, how will you do?

```
1.go to facebook and twitter to find their API and learn how to use.
2.decide the Information format which I want to transmission and reception.
3.do it
```

### do you code for test? how do you feel test?

```
yes
I think it's a the hard time in programing,sometimes I have to cost more than double time of coding to test where are bugs.
But when I finish it,I have a sense of achievement.
```

### a layout like that below, how will you implement it and tag naming, please explain 

![](http://i.stack.imgur.com/GXLMT.png)

```
The lowest level I will mean "Contain" and "Footer".
Next, I add "LeftSideBar","MiddleContain" and "RightSideBar".
Next, I add "Banner" and "MainContain"  in "MiddleContain".
Finally, I add "Header" and a framework "MainDisplay".

```

## Person: KevinSteve  張仰鈞

## Date: 2015/7/27
