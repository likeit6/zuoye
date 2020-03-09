<template>
	<div>
		<!--轮播内容页-->
		<div class="swiper-container">
			<div class="swiper-wrapper">
				<div class="swiper-slide" v-for="(item,index) in swiperArr" :key="index">
					<img :src="item.url" />
				</div>
			</div>
			<div class="swiper-pagination"></div>
		</div>
		<!-- 价格，场地 -->
		<div class="jiagel">
			<h2>课程：{{content.pro_name}}</h2>
			<h3>{{content.pro_timestr}}</h3>
			<h4>有效期：{{content.pro_active_date_text}}|场地：{{content.pro_placestr}}</h4>
			<div class="jiage">价格：{{content.pro_price}}</div>
			<button class="btn" @click="huitui">回退</button>
		</div>

		<span style="margin-left: 10px;">可预约场馆</span>
		<!-- 课程 -->

		<div class="selected">
			<div class="exhibition" v-for="(item,index) in kecheng" :key="index">
				<img class="imgarr" :src="item.gym_headimg[0].url">
				<div class="xiabu">
					<span>{{item.gym_name}}</span>
					<br>
					<br>
					<span>地址：{{item.gym_address}}</span>
					<br>
					<br>
					<span>距离：{{item.gym_distance}}</span>
				</div>
			</div>
		</div>

	</div>
</template>

<script>
	//引入 axios
	import axios from 'axios';
	//引入swiper
	import Swiper from 'swiper';
	//引入swiper的css
	import 'swiper/dist/css/swiper.css';
	export default {
		name: "myitemxtb",
		data: function() {
			return {
				//接收内容页的对象
				//轮播数据
				swiperArr: [],
				content: {},
				kecheng: []
			}
		},
		methods: {
			huitui: function() {
				this.$router.go(-1);
			}
		},
		mounted: function() {
			let params = new URLSearchParams();
			//接口定义了一些实用的方法来处理 URL 的查询字符串
			params.append('pro_id', this.$route.params.itemid);
			console.log(this.$route.params);
			params.append('fid', '');
			axios.post("https://www.jvhv.com/siteindex.php/Lesson/Detail.html", params).then((res) => {
				// 轮播图
				this.swiperArr = res.data.data.pro_imglist;
				// console.log(this.swiperArr);
				//价格
				this.content = res.data.data;
				//课程信息
				this.kecheng = res.data.data.pro_gym_list;
				console.log(this.kecheng);
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

<style>
	//轮播图样式
	.swiper-container {
		width: 100%;
		height: 170px;
	}

	.swiper-container img {
		height: 200px;
		width: 100%;
	}

	.jiage {
		color: red;
	}

	.jiagel {
		text-align: center;
		/* //灰色小条 */
		border-bottom: #f5f5f5 solid 10px;
		margin: 10px 0;
	}

	.btn {
		margin-top: 10px;
		width: 82px;
		height: 31px;
	}

	/* //课程 */

	.selected {
		display: flex;
		overflow: hidden;
		/* 开启横向滚动条 */
		overflow:auto;
		/* flex-wrap: wrap; */
		text-align: center;
		margin: 19px;
		border-bottom: #f5f5f5 solid 10px;
	}
	
	.exhibition{
		margin: 0 10px;
	}

	.exhibition a {
		display: flex;
		flex-direction: column;
		margin: 5px;
	}

	.imgarr {
		width: 150px;
		height: 120px;
		border-radius: 10px;
	}
	.xiabu{
		height: 166px;
		background-color: #999999;
		border-radius: 5px;
	}
</style>
