<template>
	<section class="body" style="padding-top: 20px;">
		<div class="box">
			<div class="wechat">
				<!--聊天列表-->
				<div class="middle on">
					<div class="wx_search">
						<input type="text" placeholder="搜索" />
						<button>+</button>
					</div>
					<div class="office_text">
						<ul class="user_list">
							<li class="user_active">
								<div class="user_head"><img src="../../img/images/head/15.jpg" /></div>
								<div class="user_text">
									<p class="user_name">宋静</p>
									<p class="user_message">我是宋静！</p>
								</div>
								<div class="user_time">下午 2：54</div>
							</li>
							<li>
								<div class="user_head"><img src="../../img/images/head/2.jpg" /></div>
								<div class="user_text">
									<p class="user_name">夏继涛</p>
									<p class="user_message">[小程序]</p>
								</div>
								<div class="user_time">上午 11：03</div>
							</li>
							<li>
								<div class="user_head"><img src="../../img/images/head/3.jpg" /></div>
								<div class="user_text">
									<p class="user_name">十里老街秋名山车神车队</p>
									<p class="user_message">乞讨两块交个话费</p>
								</div>
								<div class="user_time">昨天</div>
							</li>
							<li>
								<div class="user_head"><img src="../../img/images/head/4.jpg" /></div>
								<div class="user_text">
									<p class="user_name">阿杰</p>
									<p class="user_message">[动画表情]</p>
								</div>
								<div class="user_time">昨天</div>
							</li>
							<li>
								<div class="user_head"><img src="../../img/images/head/5.jpg" /></div>
								<div class="user_text">
									<p class="user_name">订阅号</p>
									<p class="user_message">庐山国际水彩艺术节：</p>
								</div>
								<div class="user_time">星期三</div>
							</li>
							<li>
								<div class="user_head"><img src="../../img/images/head/6.jpg" /></div>
								<div class="user_text">
									<p class="user_name">小龙网食品</p>
									<p class="user_message">槟榔的100种吃法</p>
								</div>
								<div class="user_time">星期二</div>
							</li>
							<li>
								<div class="user_head"><img src="../../img/images/head/7.jpg" /></div>
								<div class="user_text">
									<p class="user_name">文件传输助手</p>
									<p class="user_message"></p>
								</div>
								<div class="user_time">星期二</div>
							</li>
							<li>
								<div class="user_head"><img src="../../img/images/head/8.jpg" /></div>
								<div class="user_text">
									<p class="user_name">陈明杰</p>
									<p class="user_message">妈的，你在聊我</p>
								</div>
								<div class="user_time">星期四</div>
							</li>
						</ul>
					</div>
				</div>

				<!--聊天窗口-->
				<div class="talk_window">
					<div class="windows_top">
						<div class="windows_top_box">
							<span>早安无恙</span>

						</div>
					</div>
					<!--聊天内容-->
					<div class="windows_body">
						<div class="office_text" v-for="result in resultList">
							<ul class="content" id="chatbox">
								<li class="other"><img src="../../img/images/head/15.jpg" title="张文超"><span>{{result.ai_Content}}</span></li>
							</ul>
							<ul class="content" id="chatbox">
								<li class="me"><img src="../../assets/user.png" title="金少凯"><span>{{result.userSpeakText}}</span></li>
								<li class="mes"><span>{{result.evaluation}}</span></li>
							</ul>
						</div>
					</div>
				</div>
				<div class="sidestrip">
					<!--头像插件-->
					<div class="am-dropdown-content">
						<div class="own_head am-dropdown-toggle"> </div>
						<p class="own_name">宋静</p>

						<p class="own_numb">工号：A100011</p>
					</div>

				</div>

			</div>
		</div>

	</section>

</template>

<script>
import MarkdownEditor from '@/components/MarkdownEditor'

import axios from 'axios';
	export default {
		data() {
			return {
				resultList: []
			}
		},
		methods: {
			//获取对话内容
			getDialogue() {
				
		var vm = this;
		// 取到路由带过来的参数 
        var routerParams = this.$route.query.id;
        // 将数据放在当前组件的数据内
        var id = routerParams;
        
				axios.get("/api/call/getcallrecords?callId="+id)
					.then(response => {
						vm.resultList = response.data
					})
			}
		},
		mounted() {
			this.getDialogue();
		}
	}
</script>

<style scoped>

body{
	background-size: 100% 100%; 
	height: 100vh;
	-webkit-user-select:none;
    -moz-user-select:none;
    -ms-user-select:none;
    user-select:none;
}


::-webkit-scrollbar {
	width:5px;
} /* 这是针对缺省样式 (必须的) */


::-webkit-scrollbar-track {
	background-color:rgba(0,0,0,0);
	border-radius:10px;
} /* 滚动条的滑轨背景颜色 */


::-webkit-scrollbar-thumb {
	background-color: rgba(0, 0, 0, 0.1); 
	border-radius:10px;
} /* 滑块颜色 */


::-webkit-scrollbar-button {
	background-color:rgba(0,0,0,0);
	height: 0;
} /* 滑轨两头的监听按钮颜色 */


::-webkit-scrollbar-corner {
	background-color: black;
} /* 横向滚动条和纵向滚动条相交处尖角的颜色 */



p{
	margin: 0;
}

ul{
	margin: 0;
	padding: 0;
}

ul li{
	list-style-type: none;
}

.box{
    background-repeat: no-repeat;
    width: 100%;
    height: 100%;
    background-position: center center;
    background-size: cover;
    display: flex;
    justify-content: left;
    align-items: center;
}
.wechat{
    width:1070px;
    height:680px;
    background: #fff;
    box-shadow: 0 0 8px rgba(0,0,0,.1);
    border-radius:4px;
    overflow: hidden;
}

.sidestrip{
	width: 260px;
	background:#2a2e32;
	float: left;
	height: 100%;
	border-radius: 4px 0 0 4px;
	padding-top:20px;
	position: relative;
	
}


.am-dropdown-content{
	padding: 30px;
	text-align: center;
}


.own_head{
	width: 80px;
	height: 80px;
	margin-left: 60px;
	border-radius: 40px;
	background: url(../../assets/user.png);
	background-size:80px;
	
}
.own_head_top{
	width: 100%;
	display: inline-block;
	padding-bottom: 25px;
}

.own_name{
	font-size: 18px;
	color: #999;
	text-align: center;
	padding-top: 10px;
	margin-bottom:6px;
}

.own_name > img{
	width: 14px;
	margin-left: 8px;
	margin-top:3px;
}

.own_numb{
	font-size:14px;
	color: #999;
}

.own_head_top > img{
	width: 60px;
	float: right;
}

.own_head_top_text{
	float: left;
}

.own_head_bottom{
	padding-top: 20px;
}

.own_head_bottom p{
	color: #FFFFFF;
}

.own_head_bottom p > span{
	color: #FFFFFF;
	margin-right: 10px;
}

.own_head_bottom_img{
	display: inline-block;
	float: right;
	margin-top: 10px;
}

.own_head_bottom_img a img{
	margin-left:20px;
}


/*#si_1{
	background: url(../../img/images/icon/head_2.png) no-repeat;
}

#si_2{
	background: url(../../img/images/icon/head_3.png) no-repeat;
}

#si_3{
	background: url(../../img/images/icon/head_4.png) no-repeat;
}*/

.sidestrip_icon{
	margin-top: 30px;
	padding: 0 18px;
	width:60px;
}

.sidestrip_icon a{
	width: 100%;
	height:24px;
	display: block;
	margin-bottom: 30px;
}

/*.active{
	background: url(../../img/images/icon/head_2_1.png) no-repeat !important;
}

.sidestrip_bc{
	background:url(../../img/images/icon/head_5.png) no-repeat;
	position: absolute;
	bottom: 20px;
	width: 16px;
	height: 13px;
	left: 22px;
}
*/


.am-dimmer{
	z-index: 0;
	background-color:rgba(0,0,0,0);
}

.middle{
	width:260px;
	height: 100%;
	float: left;
	background: #e6e5e5;
	overflow: hidden;
	display: none;
}

.on{
	display:block;
}

.user_list, .friends_list, .icon_list{
	width: 100%;
}

.wx_search{
	padding:25px 12px 12px 12px;
	display: inline-block;
	width: 100%;
	float:inherit;
}

.wx_search input{
	width: 190px;
	height: 25px;
	background:#e5e2e2;
	border: 1px solid #d9d7d6;
	padding-left: 5px;
	outline: 0;
	float: left;
}

.wx_search button{
	font-size:20px;
	font: initial;
	background:#e5e2e2;
	border: 1px solid #d9d7d6;
	float: right;
	color: #585858;
	outline: 0;
	height: 25px;
	width: 25px;
	margin-right: 20px;
}

.wx_search button:hover{
	background:#d0d0d0;
	border: 1px solid #b9b6b5;
}

.user_list li{
	width: 100%;
	height: 64px;
	padding: 12px;
}

.friends_list li{
	width: 100%;
	padding-top: 12px;
	border-bottom:1px solid #dddbdb;
}

.user_list li:hover, .icon_list li:hover{
	background:#dedbdb;
}

.friends_box:hover{
	background:#dedbdb;
}

.user_head{
	background: #999;
	height: 40px;
	width: 40px;
	border-radius:2px;
	float:left;
	overflow: hidden;
}

.user_head img{
	width: 40px;
}

.user_text{
	float: left;
	height: 40px;
	width: 120px;
	padding-left: 8px;
}

.friends_text{
	float: left;
	line-height: 40px;
	width: 180px;
	padding-left: 8px;
}

.friends_text p{
	overflow: hidden;
	text-overflow:ellipsis;
	white-space: nowrap;
}

.user_text p{
	line-height: 20px;
	overflow: hidden;
	text-overflow:ellipsis;
	white-space: nowrap;
}

.user_name{
	color: #333;
	font-size: 14px;
}

.user_message{
	color: #999;
	font-size: 12px;
}

.user_time{
	float: right;
	margin-right: 40px;
	color: #999;
	font-size: 12px;
}

.zUIpanelScrollBox,.zUIpanelScrollBar{
	width:7px;
	top:4px;
	right:0px;
	border-radius:5px;
}

.zUIpanelScrollBox{
	background:black;
	opacity:0;
	filter:alpha(opacity=5);
}

.zUIpanelScrollBar{
	background:rgba(0,0,0,.1);
	filter:alpha(opacity=80);
}

.office_text{
    width: 100%;
	height:calc(100% - 62px);
    position: relative;
    display: inline-block;	
}

.friends_list li > p{
	font-size: 12px;
	color: #999;
	line-height: 26px;
	padding-left: 12px;
}

.friends_box{
	padding: 12px 0;
	width: 100%;
	padding-left: 12px;
	display:flex;
}

.icon_list li{
	width: 100%;
	height: 40px;
}

.icon{
	float: left;
	height:100%;
	width:50px;
	position: relative;
}

.icon_list li span{
	display: inline-block;
	line-height: 40px;
}

.icon img{
	position: absolute;
	left: 50%;
 	top: 50%;
 	transform:translate(-50%,-50%);
}

.icon_active, .user_active{
	background:#dedbdb;
}

/*******聊天窗口******/

.talk_window{
	width:550px;
	height: 100%;
	float: left;
	background: #f5f5f5;
}

.windows_top{
	padding-top:10px;
	height: 62px;
	border-bottom: 1px solid #e7e7e7;
}

.windows_top_box > span{
	font-size: 18px;
	color: #333;
	line-height: 52px;
	padding-left: 30px;
	display: inline-block;
}

.windows_top_box{
	width: 100%;
	height: 100%;
	position: relative;
}

.window_icon{
	position:absolute;
	top:-10px;
	right: 0;
}

.window_icon li{
	float: left;
	width:34px;
	height: 26px;
	position: relative;
}

.window_icon li:hover{
	background: #e3e3e3;
}


.window_icon li a img{
	position: absolute;
	left: 50%;
 	top: 50%;
 	transform:translate(-50%,-50%);
}

.windows_input{
	border-top: 1px solid #ececec;
	height: 145px;
	width: 100%;
}

.windows_body{
	height: 100%;
	width: 100%;
	height: 200px;
    box-sizing: border-box;
}

.input_icon{
	height: 42px;
	padding:0 28px;
}

.input_icon a{
	position: relative;
	display: inline-block;
	height: 20px;
	width: 24px;
	margin-top:11px;
	margin-right:8px;
}

.input_icon a img{
	position: absolute;
	left: 50%;
 	top: 50%;
 	transform:translate(-50%,-50%);
}

.input_box textarea{
	width:calc(100% - 56px);
	height:calc(100% - 42px);
	border: none;
	outline: 0;
	background:#f5f5f5;
	resize:none;
	margin-left: 28px;
	font-size: 14px;
	line-height: 20px;
}

.input_box{
	height: calc(100% - 42px);
}

.office_text1{
    width: 100%;
    height:100%;
    position: relative;
    display: inline-block;
}

#send{
	border:1px solid #e5e5e5;
	background:#f5f5f5;
	color: #666;
	padding:0 8px;
	outline: 0;
	height: 26px;
	float: right;
	margin-top: 8px;
	margin-right:28px;
}

#send:hover{
	background:#09bb07;
	color: #fff;
	border:1px solid #09bb07;
}

.optionLeft{
	background: rgb(158,243,106);
	float: right;
}

.windows_body p{
    padding: 5px 10px;
    margin-top: 10px;
    border-radius:4px;
}


/*区分聊天*/

.content{
	width: 100%;
	padding:10px 20px;
}

.me img{
	float: right;
    width: 34px;
    height: 34px;
    border-radius: 2px; 
}

.me span { 
    float: right;
    background: #FFDEAD;
}

.me{
    margin-top: 10px;
    padding-left: 10px;
    display: block;
    clear: both;
    overflow: hidden;
    float:right;
    margin-bottom:5px;
    margin-right: 50px;
}

.me span{
    background: #7BC4EF;
    padding:7px;
    border-radius:4px;
    margin:0 10px;
    max-width:60%;
    border: 1px solid #7BC4EE;
    position: relative;
    color: white;
    opacity: 0.9;
    font-size: 13px;
    
}
.mes{
   padding-right:87px;
    display: block;
    clear: both;
    overflow: hidden;
    float:right;
    margin-bottom:5px;   
}

.mes span{
    background: #f2dede;
    padding:7px;
    border-radius:4px;
    float: right;
    margin:0 10px;
    max-width:60%;
    border: 1px solid #f2dede;
    position: relative;
    color: #a94442;
    opacity: 0.8;
    font-size: 13px;
    
}

.me span:before{
    content: " ";
    position: absolute;
    top: 9px;
    right: 100%;
    border: 6px solid transparent;
    border-left-color: #7BC4EF;
    right: inherit;
    left: 100%;
}

/*other*/
.other img{
	float: right;
    width: 34px;
    height: 34px;
    border-radius: 2px; 
}

.other span { 
    float: right;
    background: #7BC4EF;
}
.others{
    padding-left: 50px;
    width:60%;
    display: block;
    clear: both;
    overflow: hidden;
    float:left;
    margin-bottom:5px;
}
.others span{
    background: #fff;
    padding:7px;
    border-radius:4px;
    float: left;
    margin:0 2px;
    max-width:60%;
    border: 1px solid #fff;
    position: relative;
    color: red;
    
}
.other{
    margin-top: 10px;
    padding-left: 10px;
    width:60%;
    display: block;  
    clear: both;
    overflow: hidden;
    float:left;
    margin-bottom:5px;
}
.other img {
    float: left;
}
.other span{
    background: #62BF6E;
    padding:7px;
    border-radius:4px;
    float: left;
    margin:0 10px;
    max-width:60%;
    border: 1px solid #62BF6E;
    position: relative;
    color: white;
    opacity: 0.9;
    font-size: 13px;
    
}

.other span:before{
    content:"";
    position: absolute;
    top: 9px;
    right: 100%;
    border: 6px solid transparent;
    border-right-color: #62BF6E;
    right: inherit;
    right: 100%;
}

</style>
