<template>
	<view class="top-title-home" @click="hanleClick()" :class="[{'isFixed':isFixed}]">
		<view class='title_text'>
			<slot></slot>
		</view>
	</view>
</template>

<script>
	/*
	 * 
	 * isFixed 固定在页面顶部保持不动  false 为不固定， true为固定
	 *
	 */
	export default {
		name: 'top-title-home',
		componentName: 'topTitleHome',
		props: {
			isFixed: {
				type: Boolean,
				default: false
			}
		},
		methods: {
			hanleClick() {
				this.$emit('click');
			},
		}
	}
</script>

<style lang="scss" scoped>
	.top-title-home {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		height: 47px;
		padding-left: 15px;
		padding-right: 15px;
	}

	.top-title-home.isFixed {
		position: fixed;
		height: 94rpx;
		width: 100%;
		top: 0;
		z-index: 15;
	}
</style>
