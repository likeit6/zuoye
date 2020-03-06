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
	              <div class="swiper-slide" style="background-image:url(https://img.jvhv.com/images/201909/5d79e7e251a52.jpg)"></div>
	              <div class="swiper-slide" style="background-image:url(https://img.jvhv.com/images/201909/5d774e055c02e.jpg)"></div>
	              <div class="swiper-slide" style="background-image:url(https://img.jvhv.com/images/201908/5d5f44fba0a1b.png)"></div>
	          </div>
	          <!-- Add Pagination -->
	          <div class="swiper-pagination swiper-pagination-white"></div>
	          <!-- Add Arrows -->
	          <div class="swiper-button-next swiper-button-white"></div>
	          <div class="swiper-button-prev swiper-button-white"></div>
	      </div>
		  
		  
		  <!-- 为您精选 -->
		  <h2>为您精选</h2>
		  <div class="selected">
		  	
		  	<div class="exhibition">
		  		<img class="imgarr" src="https://img.jvhv.com/images/201908/5d5cbfbe93e02.png" alt="">
		  		<span>健身私教课</span>
		  	</div>
		  	
		  	<div class="exhibition">
		  		<img class="imgarr" src="https://img.jvhv.com/images/201908/5d5cb669985de.png" alt="">
		  		<span>增肌六节课速成</span>
		  	</div>
		  	
		  	<div class="exhibition">
		  		<img class="imgarr" src="https://img.jvhv.com/images/201908/5d4965e65150b.jpg" alt="">
		  		<span>中考冲刺班</span>
		  	</div>
		  	
		  	<div class="exhibition">
		  		<img class="imgarr" src="https://img.jvhv.com/images/201908/5d5b9c9a45846.png" alt="">
		  		<span>成人私教课</span>
		  	</div>
		  </div>
		  
	  <div class="top5Con">
	  	<h2>本周最受欢迎TOP5</h2>
	  	<ul class="top5list">
	  		<li v-for="(item,index) in top5Arr">
	  			<router-link :to="'/item/'+item.pro_id">
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
				top5Arr:[]
			}
		},
		//挂载的函数
		mounted:function(){
			axios.post("https://www.jvhv.com/siteindex.php/Index/Index.html").then((res)=>{
				console.log(res);
				this.top5Arr = res.data.data.CourseTop5;
				console.log(this.top5Arr);
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
	
	.selected{
		display: flex;
		flex-wrap: wrap;
		margin: 19px;
	}
	.exhibition{
		display: flex;
		flex-direction: column;
		margin: 5px;
	}
	
	.imgarr{
		width: 150px;
		height: 120px;
		border-radius: 10px;
	}
		
</style>
