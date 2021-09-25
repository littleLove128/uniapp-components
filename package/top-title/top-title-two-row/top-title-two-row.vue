<template>
	<view class="top-title-two-row" title subTitle :class="[{'isFixed':isFixed}]">
		<view class="showCol">
			<view class="showRow">
				<image v-if="icon" :src="icon" mode=""></image>
				<text>{{title}}</text>
			</view>
			<text class="subtitle">{{subTitle}}</text>
		</view>
		<text class="iconfontWihte iconcaidan" @click="hanleClick2()"></text>
	</view>
</template>

<script>
	/*
	 * props
	 * 传入 icon 图片、标题title、子标题subTitle
	 *isFixed 固定在页面顶部保持不动  false 为不固定， true为固定
	 * 
	 */
	export default {
		name: 'top-title-two-row',
		componentName: 'topTitleTwoRow',
		props: {
			icon: {
				type: String,
				default: ''
			},
			title: {
				type: String,
				default: ''
			},
			subTitle: {
				type: String,
				default: ''
			},
			isFixed: {
				type: Boolean,
				default: false
			}
		},
		methods: {
			hanleClick() {
				this.$emit('click');
			},
			//点击右边菜单图标
			hanleClick2() {
				this.$emit('click');
			}

		}
	}
</script>

<style lang="scss" scoped>
	@import '../../../common/icons/iconfont.css';

	.top-title-two-row {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		height: 120rpx;
		padding-left: 15px;
		padding-right: 15px;

		image {
			width: 56rpx;
			height: 56rpx;
		}

		.showCol {
			display: flex;
			flex-direction: column;
		}

		.showRow {
			display: flex;
			flex-direction: row;
			margin-bottom: 10rpx;

			image {
				margin-right: 10rpx;
			}
		}

	}

	.top-title-two-row.isFixed {
		position: relative;
		top: 0;
	}
</style>
