<template>
	 <view class="icon-content" >
		<view :class="['icon-content-'+size]">
			<image v-if="icon" class="imageIcon" :src="icon" ></image>
			<text>{{title}}</text>
		</view>
	 </view>
</template>

<script>
	/**
	 * title是传入过来的文本
	 * icon 是传入过来的图片
	 * size 是图片与文字的大小， large 大， medium 中等（默认为中等），small 小
	*/
	export default{
		name:'icon-content',
		componentName:'iconContent',
		props:{
			icon:{
				type:String,
				default:''
			},
			title:{
				type:String,
				default:''
			},
			size:{
				type:String,
				default:'medium'
			}
		}
	}
</script>

<style lang="scss" scoped>
.icon-content{
	display: flex;
	flex-direction: row;
	align-items: center;
	justify-content: flex-start;
	image {
		margin-right: 3px;
	}
	//large 大， medium 中等（默认为中等），small 小
	.icon-content-large {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: flex-start;
		text {
			font-weight: bold;
			font-size: 36rpx;
		}
	}
	.icon-content-medium {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: flex-start;
		.imageIcon {
			width: 36rpx;
			height: 36rpx;
		}
		text {
			font-weight: 500;
			font-size: 32rpx;
		}
	}
	.icon-content-small {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: flex-start;
		.imageIcon {
			width: 32rpx;
			height: 32rpx;
		}
		text {
			font-weight: 400;
			font-size: 28rpx;
		}
	}
	
}
	

</style>
