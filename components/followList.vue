<template>
	<view class="followList">
		<scroll-view style="height:100%;" scroll-y="true" @scroll="scroll">
			<view class="item" v-for="(item,index) in list" :key="item.id">
				<view class="top">
					<view class="img-box">
						<image class="img" src="../static/img/hh.jpg"></image>
					</view>
					<view class="author-name">
						{{item.author}}
					</view>
					<view class="iconfont iconRectangleCopy share">
						
					</view>
				</view>
				<view class="title">
				 {{item.title}}
				</view>
				<view class="video-box">
					<follow-player ref="player" :index="index" :item="item"></follow-player>
					<view class="music-box">
						<view class="music">
							快乐崇拜嘿嘿嘿！！！
						</view>
					</view>
				</view>
				<view class="box">
					<view class="left">
						3-20
					</view>
					<view class="right">
						<view class="iconfont iconaixin icon">
							<text class="text">赞</text>
						</view>
						<view class="iconfont iconpinglun icon">
							<text class="text">评论</text>
						</view>
						<view class="iconfont iconfenxiang icon">
							<text class="text">分享</text>
						</view>
					</view>
				</view>
				<view class="comment">
					<view class="Number">
						4.2W评论过
					</view>
					<view class="comment-box">
						<view class="iconfont iconiconfonticonfontsousuo1 icon-pen"></view>
						<input class="input" type="text" value="" placeholder="添加评论..."/>
					</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	import followPlayer from "./followPlayer.vue"
	var timer=null;
	export default {
		props:['list'],
		name:"followList",
		data() {
			return {
				index:0,
			};
		},
		methods:{
			scroll(res){
				clearTimeout(timer);
				timer=setTimeout(()=>{
					const index=Math.floor((res.detail.scrollTop+150)/550)
					this.index=index
				},100)	
			}
		},
		components:{
			followPlayer
		},
		watch:{
			index(){	
			if(this.index>=0&&this.index<(this.list.length)){
				this.$refs.player[this.index].play()
			}
			if((this.index-1)>=0&&(this.index-1)<this.list.length){
				this.$refs.player[this.index-1].pause()
			}
			if((this.index+1)>=0&&(this.index+1)<this.list.length){
				this.$refs.player[this.index+1].pause()
			}	
			}
		}
	}
</script>

<style>
.followList{
	margin-top: 10px;
	width:100%;
	height:100%;
	background: #000000;
	padding-bottom:50px;
}
.item{
	padding: 0 15px;
	height:550px;
}
.top{
	height:35px;
	
}
.img-box{
	float: left;
	
}
.img{
	width:35px;
	height:35px;
	border-radius: 50%;
}
.author-name{
	float:left;
	font-size: 14px;
	height:35px;
	line-height: 35px;
	color:#FFFFFF;
	margin-left: 10px;
}
.share{
	float: right;
	font-size: 25px;
	margin-right: 5px;
	height:35px;
	line-height: 35px;
	color:#FFFFFF;
}
.title{
	width:100%;
	font-size: 13px;
	margin-top: 15px;
	height:25px;
	color:#FFFFFF;
	
}
.video-box{
	width:100%;
	height:350px;
	position: relative;
	
}
.music-box{
	z-index: 20;
	position: absolute;
	bottom: 10px;
	width: 100px;
	overflow: hidden;
	}
.music{
	color:#FFFFFF;
	font-size: 14px;
	width: 300px;
	animation: music 4s linear infinite;
}
.box{
	height:25px;
	margin-top: 25px;
	
}

.left{
	float: left;
	font-size: 11px;
	height:25px;
	line-height: 25px;
	color:#AAAAAA;
}
.right{
	float: right;
	color:#ffffff;
	height:25px;
	
}
.icon{
	float: right;
	font-size: 18px;
	color: #FFFFFF;
	margin-left: 10px;
}
.text{
	padding:0 5px;
	font-size: 13px;
	}
.comment{
	width:100%;
}
.Number{
	width:100%;
	height:25px;
	font-size: 15px;
	line-height: 15px;
	color:#AAAAAA;
	margin: 10px 0;
}
.comment-box{
	height:25px;
	color:#ffffff;
	position: relative;
		}
.icon-pen{
	height:30px;
	color:#FFFFFF;
	position: absolute;
	top:0;
	left:0;
		}
.input{
	font-size: 15px;
	margin-left: 28px;
	}
	@keyframes music{
		0%{
			transform: translate3d(80%,0,0);
		}
		100%{
		   transform: translate3d(-80%,0,0);
		}
	}
</style>
