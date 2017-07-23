<template>
	<!-- 时间分成三部分框的 -->
	<div v-if="blockType()" class="box">
		<div class="time">
			<span class="minute"> {{ minute }} </span>
		</div>
		:
		<div class="time">
			<span class="second">{{ second }}</span>
		</div>
		:
		<div class="time">
			<span class="millisecond">{{ millisecond }}</span>
		</div>
	</div>
	<!-- 时间放在一个框的 -->
	<div v-else class="box2">
		<span class="minute">{{ minute }}</span>
		:
		<span class="second">{{ second }}</span>
		:
		<span class="millisecond">{{ millisecond }}</span>
	</div>
</template>

<script type="text/javascript">

	export default {
		name:'killtime',
		props: {
			lefttime :{ //开奖的时间戳
				type: String
			},
			handleEnd:{
				type: Function
			},
			type: {  //样式的类型
				type: String,
				default:''
			}
		},
		data () {
			return {
				minute :'00',
				second : '00',
				millisecond : '00',
				interval:null
			}
		},
		mounted () {
			this.countDown()
		},
		watch: {

		},
		methods : {
			//倒计时秒杀函数
			countDown () {
				let _this_ =  this;
				this.interval = setInterval(function(){
					let now=new Date().getTime()/1000;     //现在的时间 转换为秒
					let left = parseInt(_this_.lefttime) - now;   //时间差
					// console.log("left:"+left+" lefttime:"+_this_.lefttime+" now:"+now);
					let m = Math.floor(left / 60 % 60);
					let s = Math.floor(left %60);
					let ms = Math.floor((left*1000 - m*60*1000 - s*1000)/10);


					m=m<10?'0'+m:m;
					s=s<10?'0'+s:s;
					ms=ms<10?'0'+ms:ms;

					_this_.minute = m;
					_this_.second = s;
					_this_.millisecond = ms;


					//如果秒杀时间结束，则清除定时器 然后触发函数
					if (new Date().getTime()/1000 > parseInt(_this_.lefttime)) { 
						clearInterval(_this_.interval);
						_this_.$emit('handleEnd'); 
					}
				},100)
			},
			blockType () {
				let _this_ = this;
				let bol = false;
				bol = (_this_.type=='one');
				return bol;
			}
		}

	}
	</script>

<style type="text/css">

		.box {
			position: relative;
		}
		.box .time {
			width: 20px;
			height: 20px;
			border: 1px solid red;
			border-radius: 5px;
			position: relative;
			display: inline-block;
		}
		.box .time span {
			text-align: center;
		    display: block;
		    font-size: 12px;
		    margin: 20% auto;
		}
		.box2{
			border: 1px solid #ccc;
			border-radius: 15px;
			width: 70px;
			height: 15px;
			text-align: center;
			color: orange;
			font-size: 12px;
		}
</style>

