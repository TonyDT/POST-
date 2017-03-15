# POST-

# node.js   
#1.文章来自慕课网但是请大家保持学习的心态不要去搞破坏。
#2.下文是慕课网教程的一个post注入代码
var http = require('http')
var querystring = require('querystring')

var postData = querystring.stringify({

#要评论的内容，如果，你自己喜欢可以写一个html页面。。把这个写成功能哈哈哈

'content':'我勒个去啊',

#文章的一个评论id 对该视频进行评论
'cid':348

})
#注入体post形式反注入来源于

var options = {
hostname: 'www.imooc.com',
path:'/course/docomment',
method:'POST',
headers:{

#注入headers 请求头信息，抓取到post内容以后手动加逗号 和分号改成key value形式


'Accept':'application/json, text/javascript, */*; q=0.01',
'Accept-Encoding':'gzip, deflate',
'Accept-Language':'zh-CN,zh;q=0.8',
'Connection':'keep-alive',
'Content-Length':postData.length,
'Content-Type':'application/x-www-form-urlencoded; charset=UTF-8',
'Cookie':'PHPSESSID=mkoioll7evs82jiub5j05pjkf7; imooc_uuid=9bcc8326-80ee-46da-b1d2-ee7681f0a2bd; imooc_isnew=1; imooc_isnew_ct=148955285,2; loginstate=1; apsid=ZlM2ZkN2M5NGI5NmNlYWEwNjU5NDBmYzZjNjZmOTAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMjEyNDQ5NgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABkb25ndGFvY29tQDEyNi5jb20AAAAAAAAAAAAAAAAAADE4ZTU0ODBiODM4ODNhNTdiMjQyYjYyOWQ4YzI0M2Zi7MXIWOzFyFg%3DOW; last_login_username=dongtaocom%40126.com; Hm_lvt_f0cfcccd7b1393990c78efdeebff3968=1489552853; Hm_lpvt_f0cfcccd7b1393990c78efdeebff3968=1489552895; cvde=58c8c5d47b403-24',
'Host':'www.imooc.com',
'Origin':'http://www.imooc.com',
'Referer':'http://www.imooc.com/comment/348',
'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36',
'X-Requested-With':'XMLHttpRequest'
    }
}

#请求完成返回状态
var  req = http.request(options,function(res){
console.log('status:' + res.statusCode);
console.log('headers:' + JSON.stringify(res.headers));

        res.on('data',function(chunk){
        console.log(Buffer.isBuffer(chunk))
        console.log(typeof chunk);	
        })

        res.on('end',function(){
        console.log('评论完毕');
        })
})

req.on('error',function(e){
console.log('Error:' + e.message);
})
#写入
req.write(postData)

req.end()


执行结果
status:200
headers:{"server":"nginx","date":"Wed, 15 Mar 2017 05:29:40 GMT","content-type":"text/html; charset=utf-8","transfer-encoding":"chunked","connection":"keep-alive","vary":"Accept-Encoding, Accept-Encoding","expires":"Thu, 19 Nov 1981 08:52:00 GMT","cache-control":"no-store, no-cache, must-revalidate, post-check=0, pre-check=0","pragma":"no-cache","content-encoding":"gzip"}
true
object
评论完毕
bogon:http dt$ node comment.js
status:200
headers:{"server":"nginx","date":"Wed, 15 Mar 2017 05:31:58 GMT","content-type":"text/html; charset=utf-8","transfer-encoding":"chunked","connection":"keep-alive","vary":"Accept-Encoding, Accept-Encoding","expires":"Thu, 19 Nov 1981 08:52:00 GMT","cache-control":"no-store, no-cache, must-revalidate, post-check=0, pre-check=0","pragma":"no-cache","content-encoding":"gzip"}
true
object
评论完毕
