<template>
  <div>
	<!--  <h2>主页</h2> -->
	<!-- 搜索框 -->
	<div class="search">
		<div class="place">厦门</div>
		<input class="searchBox" placeholder="输入搜索关键字"/>
	</div>
	
	  <!-- 轮播图 -->
	   <div class="swiper-container">
	          <div class="swiper-wrapper">
	              <div class="swiper-slide" v-for="(item,index) in swiperArr" :key="index">
					  <img :src="item.adlist_img" :alt="item.adtitle">
				  </div>
	          </div>
	          <!-- Add Pagination -->
	          <div class="swiper-pagination swiper-pagination-white"></div>
	          <!-- Add Arrows -->
	          <!-- <div class="swiper-button-next swiper-button-white"></div>
	          <div class="swiper-button-prev swiper-button-white"></div> -->
	      </div>
		  
		 <!-- 小图标 -->
		  <div class="iconCon">
			  <ul>
			  	<li v-for="(item,index) in iconArr">
					<router-link to="mytubiao">
					<img :src="require('../assets/icon/'+(index+1)+'.png')" alt="">
					<span>{{item.CategoryName}}</span>	
					</router-link>
				</li>
			  </ul>
		  </div>
		  
		  <!-- 为您精选 -->
		  <h2>为您精选</h2>
		  <div class="selectedl">
		  	<div class="exhibitionl" v-for="(item,index) in jingxuanArr">
				<router-link :to="'/myitemxtb/'+item.pro_id">
		  		<img class="imgarrl" :src="item.pro_img[0].url" alt="item.pro_name">
		  		<span>{{item.pro_name}}</span>
				<span>{{item.pro_Joiner}}人已参加</span>
				</router-link>
		  	</div>
		  	
		  </div>
		  
	  <div class="top5Con">
	  	<h2>本周最受欢迎TOP5</h2>
	  	<ul class="top5list">
	  		<li v-for="(item,index) in top5Arr">
	  			<router-link :to="'/myitem/'+item.pro_id">
	  				<div class="top5_img"><img :src="item.pro_img[0].url" /></div>
	  				<div class="top5_text">
	  					<div>{{item.pro_name}}</div>
	  					<div>{{item.pro_Joiner}}人已参加</div>
	  				</div>
	  			</router-link>
	  		</li>
	  	</ul>
	  </div>
  </div>
</template>

<script>
	//引入 axios
	import axios from 'axios';
	import Swiper from 'swiper';
	import 'swiper/dist/css/swiper.min.css';
	export default{
		name:'Mymain',
		data:function(){
			return{
				top5Arr:[],
				swiperArr:[],
				jingxuanArr:[],//精选
				iconArr:[]//10个小图标
			}
		},
		//挂载的函数
		mounted:function(){
			axios.post("https://www.jvhv.com/siteindex.php/Index/Index.html").then((res)=>{
				console.log(res);
				this.top5Arr = res.data.data.CourseTop5;
				console.log(this.top5Arr);
				//轮播图数据
				this.swiperArr = res.data.data.top_ad.list;
				//精选
				this.jingxuanArr = res.data.data.CourseforYou;
				//10个小图标
				this.iconArr = res.data.data.iconList;
				console.log(this.iconArr);
				
			})
			
			//轮播图的初始化操作
			 var swiper = new Swiper('.swiper-container', {
				loop: true,
				autoplay: 2000,
				speed: 1000,
				observer: true,
				observeParents: true,
				pagination: '.swiper-pagination',
				paginationClickable: '.swiper-pagination',
				nextButton: '.swiper-button-next',
				prevButton: '.swiper-button-prev',
				spaceBetween: 30,
				effect: 'fade'
			})
		}
	}
</script>


<!--lang="scss" 以下使用的是 scss语法
scoped="scoped" 该样式只在本页面起作用
-->
<style scoped="scoped" lang="scss">
	html, body {
	        position: relative;
	        height: 100%;
	    }
		ul,li{
			list-style: none;
		}
	    body {
	        background: #eee;
	        font-family: Helvetica Neue, Helvetica, Arial, sans-serif;
	        font-size: 14px;
	        color:#000;
	        margin: 0;
	        padding: 0;
	    }
	    .swiper-container {
	        width: 100%;
	        height: 100%;
	    }
	    .swiper-slide {
	        background-position: center;
	        background-size: cover;
	    }
	.top5Con{
		width: 90%; height:380px; background: #004b9e; border-radius: 10px; margin: auto;
		margin-top:20px;
		margin-bottom: 65px;
	}
	.top5Con h2{color:#fff; padding:20px; height: 20px;}
	.top5list{background: #fff; margin:10px; height:280px;border-radius: 10px;}
	.top5list li a{display: flex; flex-direction: row; flex-wrap: nowrap; height:60px;
	 padding:6px ; border-bottom:1px solid #ddd; }
	.top5list li a .top5_img{width:30%;}
	.top5list li a .top5_img img{width: 80%; height: 50px;}			
	.top5list li a .top5_text{width: 70%;}
	/*轮播图样式*/
	.swiper-container {
		width: 100%;
		height: 170px;
	}
	
	.swiper-container img {
		height: 200px;
		width: 100%;
	}
	
	
	// 搜索框
	.search{
		width: 100%;
		height: 30px;
		background-color: rgb(0, 75, 158);
		margin-bottom: 5px;
		display: flex;
	}
	
	.place{
		color: white;
		margin: 5px;
	}
	
	.searchBox{
		margin: 3px 50px;
		width: 200px;
		height: 20px;
		border-radius: 5px;
		text-indent: 10px;
	}
	
	.selectedl{
		display: flex;
		flex-wrap: wrap;
		margin: 19px;
		border-bottom:#f5f5f5 solid 10px;
	}
	.exhibitionl a{
		display: flex;
		flex-direction: column;
		margin: 5px;
	}
	
	.imgarrl{
		width: 150px;
		height: 120px;
		border-radius: 10px;
	}
		
		//icon样式
		.iconCon{
			border-bottom:#f5f5f5 solid 10px;
			
			ul{
				display: flex; flex-wrap: wrap; flex-direction: row; justify-content: space-around;
				margin-bottom:20px; margin-left: -38px;
				li{
					width: 40px; height:40px; margin:15px; text-align:center;
					img{width: 100%; height:100%}
					span{font-size:12px;}
				}
			}
		}
</style>
