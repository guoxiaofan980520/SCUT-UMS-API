##拾卡寻人APP入口示例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>拾卡寻人</title>
    <meta name="viewport" content="width=device-width,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no"/>

    <script src="https://cdn.bootcss.com/zepto/1.1.6/zepto.js"></script>
    <script src="js/touch.js"></script>
    <script src="js/animation.js"></script>
</head>
<style>
    @-webkit-keyframes imgAnim {
        0%   { left:20%; -webkit-transform: scale(0.3,0.3)}
        50%  { left:10%;-webkit-transform: scale(0.6,0.6)}
        100% { left:30%;-webkit-transform:scale(0.9,0.9)}

    }
    @-webkit-keyframes bntFadeIn {
        from{opacity: 0.2; -webkit-transform: scale(0.2,0.2)}
        50%{opacity: 0.6;-webkit-transform: scale(0.5,0.5)}
        to{opacity: 0.8;-webkit-transform: scale(0.8,0.8)}
    }
    @-moz-keyframes imgAnim {
        0%   { left:20%; -moz-transform: scale(0.2,0.2)}

        25%  { left:15%;-moz-transform: scale(0.3,0.3)}

        50%  { left:10%;-moz-transform: scale(0.4,0.4)}
        60%  { left:15%;-moz-transform: scale(0.5,0.5)}
        70%  { left:20%;-moz-transform: scale(0.6,0.6)}
        90% { left:25%;-moz-transform:scale(0.8,0.8)}
        100% { left:30%;-moz-transform:scale(0.9,0.9)}

    }
    @-moz-keyframes bntFadeIn {
        from{opacity: 0.2; -moz-transform: scale(0.2,0.2)}
        50%{opacity: 0.6;-moz-transform: scale(0.5,0.5)}
        to{opacity: 0.8;-moz-transform: scale(0.8,0.8)}
    }
    /* @keyframes imgAnim1 {
         from{transform:scale(1,1) }
         to{transform: scale(0.3,0.3)}
     }*/

    div[name='container']{
        /* visibility: hidden;*/
        width:100%;
        height: 100%;
        background:#fff;
    }
    input[type='text']
    {
        margin: 40% 15% 0 15%;
        width: 70%;
        height: 20%;
        border: none;
        border-bottom: 1px solid #6cbfe1;
        padding-bottom:4px;
    }
    input[type='button'] {
        -webkit-animation: bntFadeIn 1s linear 1 0.2s;
        -moz-animation: bntFadeIn 1s linear 1 0.2s;
        width: 70%;
        color: #fff;
        font-size: 14px;
        letter-spacing: 6px;
        height: 32px;
        border-radius: 4px;
        margin: 0 15% 5% 15%;
        background-color: rgb(53, 163, 203);
        border-style: hidden;
    }
    div[name='imageBox']
    {

        position: absolute;
        -moz-animation: imgAnim 1s linear 1 0s;
        -webkit-animation: imgAnim 1s linear 1 0s;
        width:40%;;
        height: auto;
        left: 30%;
        top: 10%;
    }
    div[name='finish']
    {
        visibility: hidden;
        padding-top: 30%;
        position: relative;
        height: auto;
        left: 30%;
        top: 30%;
    }
    div[name='finish'] img
    {
        width:40%;
    }
    img{

        width: 100%;
        height: auto;
    }
    p{
        color: #666;
        margin: 5% 15% 15% 15%;
        font-size: 13px;
    }
    #loading ul{
        list-style: none;
    }
    @-webkit-keyframes loading {
        from{transform: scaleY(0.7);background: skyblue}
        33%{transform: scaleY(0.4)}
        66%{transform: scaleY(0.6)}
        to{transform: scaleY(0.7) ;background: #35A3CB}
    }
    #loading ul li{
        float:left;
        height:100px;
        width:5px;
        margin-left:5px;
    }
    #loading ul li:nth-child(1){ -webkit-animation: loading 1.4s  linear 0.1s infinite;-moz-animation: loading 1.4s  linear 0.1s infinite}
    #loading ul li:nth-child(2){ -webkit-animation: loading 1.4s  linear 0.2s infinite ;-moz-animation: loading 1.4s  linear 0.2s infinite}
    #loading ul  li:nth-child(3){ -webkit-animation: loading 1.4s  linear 0.3s infinite;-moz-animation: loading 1.4s  linear 0.3s infinite}
    #loading ul  li:nth-child(4){ -webkit-animation: loading 1.4s  linear 0.4s infinite;-moz-animation: loading 1.4s  linear 0.4s infinite;}
    #loading ul  li:nth-child(5){ -webkit-animation: loading 1.4s  linear 0.5s infinite;-moz-animation: loading 1.4s  linear 0.5s infinite;}
    #loading ul li:nth-child(6){ -webkit-animation: loading 1.4s  linear 0.6s infinite;-moz-animation: loading 1.4s  linear 0.6s infinite;}
    *{margin:0px;padding: 0px;}
    #img{
        position: fixed;
        width: 100%;height: 100%;
    }
</style>
<body>

<div name="container" id="mainCon">
    <div name="imageBox" id="logoCon"><img  src="css/images/logo.png"></div>
    <div style="margin-top: 40%" id="textCon">
        <input style="font-size:1.5em" type="text" placeholder="请输入失卡人的学号" id="stuId">
        <p>点击确定后，将发送你的手机号码至卡人的客户端，便于失卡人与您联系</p>
        <input type="button" value="确定" id="sure">
        <input type="button" value="取消" id="cancel">
    </div>
    <div name="finish" id="finishCon">
        <img  src="css/images/finish.png">
    </div>
    <p style="position:fixed;left:0;top:500px;font-size: 12px;" id="content"></p>
</div>

<div  id="loading" style="">
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
</div>
<script>
    var swidth=screen.width;  //频幕宽度
    var lwidth=$("#loading ul li").width()*12; //进度条的宽度
    var left=(swidth-lwidth)/2;
    $("#loading").css("margin-left",left);  //进度条居中
    $("#loading").css("margin-top",left);
    //获取url的参数
    function GetUrl() {
        var url = location.search; //获取url中"?"符后的字串
        var theUrl = new Object();
        if (url.indexOf("?") != -1) {
            var str = url.substr(1);
            substr = str.split("&");
            for(var i = 0; i < substr.length; i ++)
            {
                theUrl[substr[i].split("=")[0]]=unescape(substr[i].split("=")[1]);
            }
        }
        return theUrl;
    }
    
    //实现功能的方法
    $(function () {
        //   cancel tap event
        $("#cancel").tap(function () {
            $("input[type='text']").val("");
        })
        //   sure tap event
        $("#sure").tap(function () {
            $("#loading").show();
            var args = GetUrl();
            var sendData={
                "account":args['account'],
                "code":args['code'],
                "desAccount":$("#stuId").val()
            };
            $.ajax({
                url:"/Wisdom/message/findPerson",
                type:"post",
                dataType:"json",
                contentType:"application/json",
                data:JSON.stringify(sendData),
                async:false,
                success:function (json) {
                    if(json.result == "checked"){
                        //   alert(111);
                        $("#loading").hide();//隐藏加载动画
                        $("#logoCon").remove();
                        $("#textCon").remove();
                        $("#finishCon").remove();
                        //    alert(222);
                        $("#mainCon").append($(" <img id='img' style='position:fixed; width:80%;height: 50%;top:10%;left:10%;right: 10%;' src='css/images/check-circle.png'>"));
                        console.log(screen.height);

                        var img = document.getElementById("img");
                        img.style.width = (screen.width);
                        img.style.height= (screen.height);
//                     var jsonData = $({content:"失卡的同学已经收到该信息，请静待其与你联系！"});
                        //     alert(json.content);
                        $("#content").html(json.content);
                        //   alert(333);
                    }
                    else if(json.result == "failsave"){
                        $("body").children().remove();
                        $("body").append($(" <img id='img'  src='css/images/netWorkError.png'>"));
                        console.log(screen.height);

                        var img=document.getElementById("img");
                        img.style.width=(screen.width);
                        img.style.height=(screen.height);
                    }
                    else if(json.result == "no such service"){
                        $("body").children().remove();
                        $("body").append($(" <img id='img'  src='css/images/netWorkError.png'>"));
                        console.log(screen.height);

                        var img=document.getElementById("img");
                        img.style.width=(screen.width);
                        img.style.height=(screen.height);
                    }
                },
                error:function() { //处理出错信息
                    // window.location.href="networkError.html";
                    //$("#loading").hide();
                    $("body").children().remove();
                    $("body").append($(" <img id='img'  src='css/images/netWorkError.png'>"));
                    console.log(screen.height);

                    var img=document.getElementById("img");
                    img.style.width=(screen.width);
                    img.style.height=(screen.height);

                }
            });
        });
    });

</script>
</body>
</html>

```
