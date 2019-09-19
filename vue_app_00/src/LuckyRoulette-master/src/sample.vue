<template>
	<div class="wrapper">
		<mt-header title="抽奖" class="head">
        	<router-link to="" slot="left">
            	<mt-button icon="back" @click="$router.back(-1)">返回</mt-button>
        	</router-link>
    	</mt-header>
		<Roulette :r="roulette.radius" :coverurl="roulette.coverurl" :datas="roulette.datas" :test="roulette.test"
		 :pointerurl="roulette.pointerurl" ref="luckyRoulette" :during="duringHandle" @click="clickFun"></Roulette>

		<div class="sample">
			<p>抽奖次数：{{a}}</p>
			<p>
				<mt-button @click="clickFun" class="no_1">开始抽奖</mt-button>
			</p>
			<div class="sample1"></div>
		</div>
	</div>
</template>
<script>
import Roulette from './roulette'
	export default {
		components: {
			Roulette
		},
		data() {
			return {
				s:"",
				a:3,
				sample: {
					state: 3
				},
				roulette: {
					coverurl: '../assets/r.png',
					pointerurl: '../assets/p.png',
					radius: 150,
					test: true,
					datas: [{
						name: '1',
						degs: [27, 87],
						desc: '谢谢参与',
						integral:0
					}, {
						name: '2',
						degs: [333, 387],
						desc: '特等奖',
						integral:40
					}, {
						name: '3',
						degs: [87, 147],
						desc: '二等奖',
						integral:30
					}, {
						name: '4',
						degs: [147, 207],
						desc: '欢迎再来',
						integral:0
					}, {
						name: '5',
						degs: [207, 274],
						desc: '一等奖',
						integral:20
					}, {
						name: '6',
						degs: [274, 333],
						desc: '三等奖',
						integral:10
					}]
				}
			}
		},
		methods: {
			duringHandle(state) {
				this.sample.state = state;
			},
			setRadius(radius) {
				this.roulette.radius = radius;
			},
			clickFun(){
				if(this.a>0){
					this.a--;
					this.$refs.luckyRoulette.play()
					var vm = this;
					var s=Math.ceil(Math.random()*6);
					this.s=s;
					var integral=vm.$refs.luckyRoulette.datas[s-1].integral;
					setTimeout(function() {
						vm.$refs.luckyRoulette.brake(s);
					}, 3000);
					this.axios.get("sample",{params:{integral:integral}}).then(res=>{
						setTimeout(function() {
							alert("积分"+integral);
						}, 9000);
					})
				}else{
					this.$toast("抽奖次数不足");
				}
			}
		},
		created() {

		}
	}
</script>
<style>
	.wrapper {
		text-align: center;
		background:url(../assets/timg.jpg);
		background-size:100% 100%; 
	}

	input {
		font-size: inherit;
		width: 40px;
	}

	.no_1 {
		font-size: inherit;
		background: #efefef;
		position: absolute;
		z-index: 100;
		margin: 0 auto;
		
	}
		/* p{
			margin: 0px;
			margin-top: 10px;
		} */
	.roulette_roundel--cover{
		background: url(../assets/r.png)no-repeat;
		background-size:100% 100%; 
		position: relative;
	}
	.head{
        height: 48px;
		font-size: 18px; 
		margin-bottom: 50px;
    }
	.sample1{
		background: url(../assets/turbanner.png);
		background-size:100% 100%;
		height: 280px;
		position: relative;
		top: -7px;
	}
	Roulette{
		margin-top: 10px;
	}
</style>
