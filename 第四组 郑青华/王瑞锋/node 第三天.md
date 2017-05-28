##node 第三天
####buffer
- 一个字节在十进制中最大255
- 16进制全部以0xk开头，8进制以0开头

###buffer创建
- 通过长度创建
```
var buffer=new Buffer(6);
buffer.fill(1); //手动填充buffer
```
- 通过数组创建buffer
```
var buffer=new Buffer（[-2,5,3,54]）
//如果数组中的某一个不能正确转换则转换为0，如果大于255则对256取模，如果写负数则加上256
```
- 通过字符串创建buffer
```
var buffer=new Buffer('王瑞锋')；
console.log(buffer[0]);// 通过汉字创建的buffer内容和汉字是对应的，将buffer转换成字符  方法是头string（），如果buffer中的某一个，则是16进制代表的10进制
```

1.buffer.toString ()  ,buffer.length
2.slice()截取，包前不包后  .buffer中存的是内存地址 可以将buffer看成一个二维数组
```
var buffer = new Buffer([1, 2, 3]);
var newBuffer = buffer.slice(0, 1);
newBuffer[0] = 100;
console.log(buffer);
```

3.copy 可以将小的buffer拷贝到大的buffer上
```
var buf1 = new Buffer('珠峰');
 var buf2 = new Buffer('培训');
 buf2.copy(buffer,0,0,buf2.length);
 buf1.copy(buffer,buf2.length,0,buf1.length);
console.log(buffer.toString());//培训珠峰

第二种
buf1.copy(buffer, 0);
buf2.copy(buffer, buf1.length);
console.log(buffer.toString());//培训珠峰
```

4.Buffer.concat([buf1,buf2]);返回的还是buffer
```
var buf1 = new Buffer('珠峰培');
var buf2 = new Buffer('训');
Buffer.Concat([buf1,nuf2]).toString()；
```

5.如何拷贝一个对象  递归循环
```
方法一
var obj = {
    name: 1, age: 2, a: function () {
    }
};
 var obj2 = JSON.parse(JSON.stringify(obj)); //stringify不识别函数，所以不能带函数的，如以上
 
方法二
var obj1 = {};
Object.assign(obj1, obj, {age: 3}); //拷贝对象 es6的语法
```

###reduce 返回数组叠加后的结果
```
var total = [1,2,3,4].reduce((prev,next)=>{
    console.log(prev,next);
    return prev+next;//返回值会作为下一次循环的上一次
},0);//0是指定第一次的上一次
console.log(total);
```

###进制转换
- 将任意进制转换成10进制 parserInt
```
console.log(parseInt("00111111",2));
```
- 16进制转换成2进制 0xff
```
console.log(0xff.toString(10));
```
- base64 将汉字转换成base64,没有加密功能
- d5加密 1.不可逆 2.加密的结果的长度都是一样的 3.不同的内容 加密后的结果不一致
- 一个汉字 3*8 => 6*4 ,每一个字节不能超过63这么大

##fs
####fs是一个核心模块,操作文件 目录 文件夹
 > fs里面的方法都是同步和异步同时出现，能用异步不用同步

读取的特点
1) 读取的文件必须存在
2) 读出的类型默认是buffer
3)  /代表的是根目录 当前文件所在的磁盘的根目录
4) 同步的结果永远都在返回值上，异步结果在callback参数中
5) 异步代码 没有返回值

同步错误可以try catch捕获

- 很多时候处理异步可以进行嵌套，可能会导致回调地狱
- Object.keys将对象转换成数组 {name:1,age:2} => [name,age]

写入是的特点
1) 写入的内容会自动转换成utf8格式
2) flag:'w' 清空 创建 仅写
3) 如果写入的是对象 要JSON.stringify
```
fs.writeFileSync('./age.txt',JSON.stringify({name:1}));
fs.writeFile('./age.txt',JSON.stringify({name:1}),function (err) {
    if(err)console.log(err);
});
```

####copy 有同步和异步  copySync copy
读取源文件 ，将内容读取到内存中，将内存中的数据写入到文件中
```
function copySync(source,target) {
 let file = fs.readFileSync(source);
 fs.writeFileSync(target,file);
 }
```
```
function copy(source, target, cb) {
    fs.readFile(source, function (err, data) {
        fs.writeFile(target, data, cb);
    });
}
```
readFile不能读取比内存大的文件（不大于64k），太大会导致淹没可用内存，流（边读边写）


#### mkdir必须在父级有的情况下创建子级
- fs.exists(path, callback) 测试某个路径下的文件是否存在。回调函数包含一个参数exists，true则文件存在，，否则是false。
```
fs.exists('/etc/passwd', function (exists) {
  util.debug(exists ? "it's there" : "no passwd!");
})
```

- fs.mkdir(path, [mode], [callback(err)])
以异步的方式创建文件目录。如果目录已存在，将抛出异常。
> path            将创建的目录路径
mode          目录权限（读写权限），默认0777
callback      回调，传递异常参数er
```
var fs = require('fs');
fs.mkdir('creatdir', 0777, function(err){
 if(err){
  console.log(err);
 }else{
  console.log("creat done!");
 }
})
```

####path 
let path = require('path');
path.resolve 解析（将相对路径 解析成绝对路径）   path.join 连接
```
这两种方法的结果一样，但一般选用第一种
console.log(path.resolve('dist','a','b'));
console.log(path.join(__dirname,'dist','a','b'));
```

####可读流
1）highWaterMark 64k每次读取的大小
2) 没有编码默认是buffer
```
let rs = fs.createReadStream('./1.txt',{highWaterMark:1});
```

```
rs.on('data',function (data) { //监听每次读到内容
    rs.pause();//暂停读取，暂停触发data事件
    console.log('读取一次');
    str.push(data);
    rs.resume();//恢复触发data事件
});
rs.on('end',function () { //文件读取完成后执行end方法
    console.log(Buffer.concat(str).toString());
});
rs.on('error',function (err) { //监听读流中的错误
    console.log(err);
});
```


写的特点
1) 如果文件不存在，则创建
2) 写入时默认编码是utf8格式
3) 通过流写入文件也是异步
4) 默认写的时候创建的空间大小是16k

```
let ws = fs.createWriteStream('./2.txt',{highWaterMark:1});
```

let flag = ws.write(1+"");//返回值表示是否能写入，不管true还是false 都能写进去

ws.end('撑死我了');//end方法会调用write方法，无论是否写完，都会强制被写入，关闭掉文件
//write after end  已经结束了 不能再写入了

fs.createWriteStream(path, [options])
该方法属于fs模块，使用前需要引入fs模块（var fs= require(“fs”) ）
path    文件路径
option (object) 参数包含以下属性：
{ flags: 'w',
  encoding: null，
  mode: 0666 }
  flags 默认值为w，如果你想修改一个文件，而不是取代它需要把flags改成R +。


```
ws.on('drain',function () { // drain方法执行表示预计的内存，和可用空间的内容全部消化后执行的方法
    console.log('干了');
    eat();//利用预估的空间写入内容
});
```
node.js  关于读写流Stream
http://www.tuicool.com/articles/jEVNRbY   
