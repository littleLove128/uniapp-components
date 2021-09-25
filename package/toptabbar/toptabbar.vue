<template>

	<ul
		:class="{'top-tabbar':'top-tabbar','top-tabbar-list':'top-tabbar-list', 'active-top-tabbar':show?'active-top-tabbar':''}">
		<li v-for="(item,index) in list" :key="item.text" class="top-tabbar-item">
			<view @click="handleClick(index)"
				:class="{text:'text','active-text':$route.path===item.to?'active-text':''}">{{item.text}}</view>
		</li>
	</ul>

</template>
<script>
	/* 
		show-Boolean-false-是否显示下拉菜单
		list-Array-[]-下拉菜单数据
			{
				text: 'Start',
				to: '/pages/example/right-sidebar/right-sidebar'
			}
		@click-index-自定义点击事件
	 */
	export default {
		name: 'TopTabbar',
		componentName: 'TopTabbar',
		props: {
			show: {
				type: Boolean,
				default: false
			},
			list: {
				type: Array,
				default: []
			}
		},
		methods: {
			handleClick(index) {
				this.$emit('click', index)
			}
		}

	}
</script>

<style lang="scss" scoped>
	.top-tabbar-list {
		box-sizing: border-box;
		padding-left: 0rpx;
		width: 100%;
		height: 0;
		display: flex;
		align-items: center;
		flex-direction: column;
		overflow-y: scroll;
		transition: height .2s ease-in-out;
		.top-tabbar-item {
			list-style-type: none;
			box-sizing: border-box;
			padding-top: 40rpx;
			padding-bottom: 40rpx;
			font-size: 32rpx;
			font-family: PingFang SC;
			font-weight: 500;
		}
	}

	.active-top-tabbar {
		height: 776rpx;
	}
</style>
