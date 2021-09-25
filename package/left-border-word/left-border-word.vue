<template>
	<view class="left-border-word">
		<view class="left">
			<view class="line"></view>
			<text>{{title}}</text>
		</view>
		<view v-if="showArrow">
			<text class="iconfont iconerjitiaozhuan" style="font-size: 6px;" @click="handleClick()"></text>
		</view>
	</view>
</template>

<script>
	/**
	 * title 是这个部分的标题，
	 * showArrow 默认为不显示右边箭头，传值表示显示，
	 * handleClick()可以点击右箭头
	 */
	export default{
		name:'left-border-word',
		componentName:'leftBorderWord',
		props:{
			title:{
				type:String,
				default:''
			},
			showArrow:{
				type:Boolean,
				default:false
			}
		},
		methods:{
			handleClick(){
				this.$emit('click');
			}
		}
	}
</script>

<style lang='scss' scoped>
	@import '../../common/icons/iconfont.css';
	.left-border-word {
		padding-left: 15px;
		padding-right: 15px;
		padding-top: 10px;
		padding-bottom: 10px;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		font-size: 30rpx;
		.left {
			display: flex;
			align-items: center;
			flex-direction: row;
			justify-content: flex-start;
		}
		.line {
			width: 4rpx;
			height: 20rpx;
			margin-right: 10rpx;
		}
	}
	
</style>
