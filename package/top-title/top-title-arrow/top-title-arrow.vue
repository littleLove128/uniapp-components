<template>
	<view class="showRelative">
		<view class="top-title-arrow" :class="[
			{'is-center':centerTitle},
			{'isFixed':isFixed},
			]">
			<span class="iconfontTopLeftArr iconfanhui" @click='backLastPage()'></span>
			<span class='title_text'>
			   <text v-if="title">{{title}}</text>
			   <slot v-else></slot>
			</span>
		</view>
	</view>
</template>

<script>
	/*
	 * centerTitle 表示标题是否居中显示默认为靠左边显示
	 * isFixed 固定在页面顶部保持不动  false 为不固定， true为固定
	 * slot 传入页面标题 如果传入 title也可以不用传入slot
	 */
	export default {
		name: 'top-title-arrow',
		componentName: 'topTitleArrow',
		props: {
			centerTitle: {
				type: Boolean,
				default: false
			},
			isFixed: {
				type: Boolean,
				default: false
			},
			title:{
				type: String,
				default: ''
			}
		},
		methods: {
			backLastPage() {
				uni.navigateBack()
			}
		}
	}
</script>

<style lang="scss">
	@import '../../../common/icons/iconfont.css';

	.iconfontTopLeftArr {
		font-family: iconfont;
		text-decoration: none;
		text-align: center;
		margin-left: 15px;
		margin-right: 10px;
	}

	.top-title-arrow {
		display: flex;
		flex-direction: row;
		align-items: center;
	}

	.top-title-arrow.isFixed {
		width: 100%;
		// position: fixed;
		// position: sticky;
		top: 0;
		z-index: 999;
		// margin-bottom: 88rpx;
	}

	.title_text {
		// width: 80%;
		
	}

	.top-title-arrow.is-center {
		.title_text{
			margin-left: 220rpx;
		}
		text-align: center;
	}

</style>
