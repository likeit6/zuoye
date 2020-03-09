<template>
	<div>
		<!--轮播内容页-->
		<div class="swiper-container">
			<div class="swiper-wrapper">
				<div class="swiper-slide" v-for="(item,index) in swiperArr" :key="index">
					<img :src="item.url" :alt="item.adtitle" />
				</div>
			</div>
			<div class="swiper-pagination"></div>
			<!-- <div class="swiper-button-prev"></div>
			<div class="swiper-button-next"></div> -->
		</div>
		
		<br>
		<div class="changdi">
			<h3>{{itemObj.pro_name}}</h3>
			<h4>{{itemObj.pro_timestr}}</h4>
			<span>有效期：{{itemObj.pro_active_date_text}} | 场地：{{itemObj.pro_placestr}}</span>
			<br>
			<div class="jiage">价格：{{itemObj.pro_price}}.0元</div>
			<button class="btn" @click="goBack">返回</button>
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
		name: "myitem",
		data: function() {
			return {
				//接收内容页的对象
				itemObj: {},
				//轮播数据
				swiperArr: [],
				//场地
				changdi: []
			}
		},
		//顺序问题，放后面不行
		methods: {
			//返回上一页
			goBack: function() {
				this.$router.go(-1);
			}
		},
		mounted: function() {
			//通过 itemid获取 内容页数据
			//7.获取数据，将数据保存到变量中
			//创建新的查询传参对象
			let params = new URLSearchParams();
			//接口定义了一些实用的方法来处理 URL 的查询字符串
			params.append('pro_id', this.$route.params.itemid);
			console.log(this.$route.params);
			params.append('fid', '');
			axios.post("https://www.jvhv.com/siteindex.php/Lesson/Detail.html", params).then((res) => {
				this.itemObj = res.data.data;
				console.log(this.itemObj);
				// 轮播图
				this.swiperArr = res.data.data.pro_imglist;
				// console.log(this.swiperArr);
			})


			//轮播图配置
			var mySwiper = new Swiper('.swiper-container', {
				loop: true,
				autoplay: 2000,
				speed: 1000,
				observer: true, //处理异步数据
				observeParents: true,
				// 如果需要分页器
				pagination: '.swiper-pagination',
				// 如果需要前进后退按钮
				nextButton: '.swiper-button-next',
				prevButton: '.swiper-button-prev',
			})
		}

	}
</script>

<style lang="scss">
	//轮播图样式
	.swiper-container {
		border-bottom: #f5f5f5 solid 10px;
		height: 170px;

		.swiper-wrapper {
			.swiper-slide {
				img {
					width: 100%;
					height: 170px;
				}
			}
		}
	}

	h3 {
		font-size: 26px;
		font-weight: normal;
		margin-top: 10px;
		padding-left: 10px;
	}

	.jiage {
		color: red;
		font-size: 25px;
	}

	h4 {
		margin-left: 7px;
	}

	.btn {
		margin-top: 10px;
		width: 82px;
		height: 31px;
	}
	.changdi{
		text-align: center;
	}
</style>
