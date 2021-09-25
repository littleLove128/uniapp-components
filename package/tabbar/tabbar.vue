<template>
	<cover-view class="tabbar" :style="{'padding-bottom': paddingBottomHeight + 'rpx'}">
		<cover-view class="tabbar-item" v-for="(item, index) in list" :key="index"
			@click="tabbarChange(item.path,index)">
			<image class="item-img" :src="item.icon_a" v-if="tabbarCurrentIndex == index"></image>
			<image class="item-img" :src="item.icon" v-else></image>
			<cover-view class="item-name" :class="{'tabbarActive': tabbarCurrentIndex == index}" v-if="item.text">
				{{item.text}}
			</cover-view>
		</cover-view>
	</cover-view>
</template>

<script>
	/* 
		tabbarCurrentIndex:当前选中下表
		list:底部列表
			{
				text: string, // 文本
				icon: require('xxxxx'), //未选中图标
				icon_a: require('xxxxx'), //选中图片
				path: "#", //页面路
			}
	 */
	export default {
		name: "Tabbar",
		componentName: 'Tabbar',
		props: {
			list: Array,
			tabbarCurrentIndex: Number,
		},
		data() {
			return {
				page: 'contact',
				showPage: false,
				containerHeight: 400,
				paddingBottomHeight: 0, //苹果X以上手机底部适配高度
			}
		},
		created() {
			let that = this;
			uni.getSystemInfo({
				success: function(res) {
					let model = ['X', 'XR', 'XS', '11', '12', '13', '14', '15'];
					model.forEach(item => {
						//适配iphoneX以上的底部，给tabbar一定高度的padding-bottom
						if (res.model.indexOf(item) != -1 && res.model.indexOf('iPhone') != -1) {
							that.paddingBottomHeight = 40;
						}
					})
				}
			});
		},
		methods: {
			tabbarChange(path, index) {
				this.$emit('click', index)
			}
		}
	}
</script>

<style lang='scss' scoped>
	.tabbar {
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		width: 100%;
		height: 100rpx;
		background-color: #ffffff;
		display: flex;
		justify-content: space-around;
		align-items: center;
		z-index: 5;

		.tabbar-item {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			height: 100rpx;

			.item-img {
				width: 46rpx;
				height: 46rpx;
				margin-bottom: 4rpx;
			}

			.item-name {
				font-size: 26rpx;
				color: #A3A3A3;
			}


		}
	}
</style>
