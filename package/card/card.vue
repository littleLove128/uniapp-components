<template>
	<view :style="{ width:345*2+'rpx', height:'110rpx' }" class="card" id="card"></view>
</template>

<script>
/* 
		className-String-'card'-自定义类名
	 */
export default {
	name: 'Card',
	componentName: 'Card',
	props: {
		className: {
			type: String,
			default: 'card'
		},
		width: {
			type: String,
			default: '345rpx'
		},
		height: {
			type: String,
			default: '110rpx'
		}
	},

	mounted() {
		// 动态添加多个类名
		const dom = document.getElementById('card');
		dom.className += ' ' + this.className;
	}
};
</script>

<style lang="scss" scoped>
.card {
	// width: var(--width);
	// height: var(--height);
	background-color: red;
	border-radius: 20rpx;
}
</style>
