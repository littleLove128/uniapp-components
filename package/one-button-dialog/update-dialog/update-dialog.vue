<template>
	<transition name="dialog-pop">
		<view class="update-dialog" v-show="visible" @click.self="handCloses">
			<view class="update-dialog-content">
				<view class="new-version">{{version}}</view>
				<view class="fixed-word"> {{title}} </view>
				<view class="center-mark">
					<div class="lineLeft"></div>
					<view class="update-now-text"> {{updateNow}}</view>
					<div class="lineRight"></div>
				</view>
				<view class="update-content-text">
					{{updateContent}}
				</view>
		<!-- 		<progress 
				percent="3" 
				activeColor="#2EBEF3" 
				backgroundColor="#E7EBEE" 
				border-radius='10px'
				:active='true'
				/> -->
				<view class="my-progress">
					<view class="percent" v-if="active"></view>
				</view>
				<text class="percent-text">{{percent}}%</text>
				<view class="buttonPosition">
					<functional-button
					:title="buttonText"
					circle
					type="surface"
					highlight
					size="large"
					@click='download'
					>
					</functional-button>
				</view>
			</view>
		</view>
	</transition> 
</template>

<script>
	/**
	 * visible 显示与否
	 * version 传入版本号
	 * updateContent 传入更新内容
	*/
	export default{
		name:'update-dialog',
		componentName:'updateDialog',
		data(){
			return {
				title:"发现新版本",//默认显示，写项目的时候需要换成多语言的
				updateNow:'立即更新，体验更佳',
				active:false, 
				percent:0, //进度条
				buttonText:'立即下载' //按钮文字
			}
		},
		props:{
			visible: {
			   type: [Boolean,String],
			   default: false
			},
			version:{
				type:String,
				default:''
			},
			updateContent:{
				type:String,
				default:''
			}
		},
		methods:{
			handCloses() {
				this.$emit('close',false);
				// this.visible = false
			},
			download(){
				if(this.percent>=100){
					this.buttonText = '安装';
					this.active = true;
					this.percent = 100;
				} else {
					this.buttonText = '下载中';
					this.active = true;
					this.percent = 100;
				}
				
			}
		}
	}
</script>

<style lang="scss" scoped>
.update-dialog{
	position: fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	overflow: auto;
	margin: 0;
	z-index: 2001;
	// background-color: rgba($color: #000000, $alpha: 0.09);
	.update-dialog-content{
		position: relative;
		margin: 15vh auto 50px;
		box-sizing: border-box;
		width: 90%;
		border-radius: 10px;
		height: 804rpx;
		padding: 36rpx;
		// background: url('/static/picture/updatebg/blue-update-bg.png') #FFFFFF no-repeat;
		// background-size: 100% 100%;
		.new-version{
			font-size: 28rpx;
			margin-top: 36rpx;
			padding-bottom: 10rpx;
			width: 100rpx;
			font-weight: 600;
			// color: #111E3E;
			// border-bottom: 4rpx solid #012639;
		}
		.fixed-word{
			margin-top: 20rpx;
			font-size: 46rpx;
			font-weight: 500;
		}
		.center-mark{
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			margin-top: 84rpx;
			.update-now-text{
				font-size: 22rpx;
				// color: #787C84;
			}
			.lineLeft{
				// background: linear-gradient(to right,#EBFFFD,#787C84);
				width: 130rpx;
				height: 2rpx;
			}
			.lineRight{
				// background: linear-gradient(to left,#EBFFFD,#787C84);
				width: 130rpx;
				height: 2rpx;
			}
		}
		.update-content-text{
			margin-top: 86rpx;
			font-size: 28rpx;
			// color: #111E3E;
			height: 160rpx;
		}
		.my-progress{
			margin-top: 32rpx;
			height: 6rpx;
			width: 560rpx;
			border-radius: 6rpx;
			// background-color: #E7EBEE;
			.percent{
				height: 100%;
				// background-color: #2EBEF3;
			}
		}
		.percent-text{
			font-size: 24rpx;
			margin-top: 16rpx;
			text-align: center;
			// color: #111E3E;
		}
		.buttonPosition{
			margin: 24rpx auto;
		}
	}
}	
	
	
.dialog-pop-enter-active {
  animation: dialog-fade-in .4s;
}
.dialog-pop-leave-active {
  animation: dialog-fade-out .4s;
}
@keyframes dialog-fade-in {
  0% {
    transform: translate3d(0, -20px, 0);
    opacity: 0;
  }
  100% {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
}
@keyframes dialog-fade-out {
  0% {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
  100% {
    transform: translate3d(0, -20px, 0);
    opacity: 0;
  }
}
	
</style>
