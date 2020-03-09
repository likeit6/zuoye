<template>
	<div>
		<div class="onw">
			<div class="tow" v-for="(item,index) in tuijian" :key="index">
				<!-- <img  :src="item.tre_img[0].url" /> -->
				
				<!-- 判断 tre_img 是否有值不然会报url未定义-->
				<img class="arr" v-if="item.tre_img != false" :src="item.tre_img[0].url" alt="">
				<div>{{item.tre_descr}}</div>
			</div>
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
					tuijian:[],
					imgArr:[],
				}
			},
			//挂载的函数
			mounted:function(){
				axios.post("https://www.jvhv.com/siteindex.php/Trends/Index.html").then((res)=>{
					this.tuijian = res.data.data.list;
					// for(var i = 0; i<this.tuijian.length;i++){
					// 	this.imgArr.splice(0,0,this.tuijian[i++].tre_img[0].url);
					// }
					// console.log(this.tuijian[0].tre_img[0].url);
					// console.log(this.imgArr);
					// // let c = a.concat(b);
				})
				
			}
		}
</script>

<style>
	
	
	.arr{
		width: 100%;
		height: 229px;
	}
</style>
