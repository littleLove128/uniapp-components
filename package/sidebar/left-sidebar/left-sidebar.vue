<template>
	<uni-drawer ref="showRight" :mode="mode" :mask-click="maskClick" :mask="mask">
		<view class="side-bar-list">
			<scroll-view style="height: 100%;" scroll-y="true">
				<view @click="handleClick(index)" v-for="(item,index) in list" :key="item.text" class="side-bar-item"
					:class="$route.path===item.to?'active-side-bar-item':''">
					<image class="icon" :src="item.icon" mode=""></image>
					<text class="text">{{item.text}}</text>
				</view>
			</scroll-view>
		</view>
		<footer class='footer'>
			<view class="theme">
				<view class="white" @click="changeTheme(0)">
					<!-- <image class="sun" src="../../../assets/images/white.png" mode=""></image>-->
					<span class='icona-zu1649 iconfont'></span>
				</view>
				<view class="black" @click="changeTheme(1)">
					<!-- <image class="moon" src="../../../assets/images/block.png" mode=""></image> -->
					<span class='icona-lujing2024 iconfont'></span>
				</view>
				<view class="block" :class="activeThemeBlock?'sunBlock':'moonBlock'"></view>
			</view>
			<view class="lang">
				<text :class="{cn:'cn',activeCn:activeLangBlock?'activeCn':''}" @click="changeLang(0)">中</text>
				<text :class="{en:'en',activeEn:!activeLangBlock?'activeEn':''}" @click="changeLang(1)">En</text>
				<view class="block" :class="activeLangBlock?'zhBlock':'enBlock'"></view>
			</view>
		</footer>
	</uni-drawer>
</template>

<script>
	/* 属性-数据类型-默认值-说明
		visibleSync-Boolean-false-侧边栏显示
		list-Array-[]-菜单列表
			{
				text: "首页",
				icon: require('@/assets/images/home.png'),
				to: '/pages/example/left-sidebar/left-sidebar'
			}
		mask-Boolean-true-是否显示遮罩
		maskClick-Boolean-true-点击遮罩是否可以关闭抽屉
		mode-String-left-Drawe滑出位置，可选值：left（从左侧滑出）， right（从右侧滑出）
		@click-Function-val(当前点击元素下标)
	 */
	export default {
		name: 'SlideBar',
		componentName: 'SlideBar',
		props: {
			visibleSync: {
				type: Boolean,
				default: false
			},
			list: {
				type: Array,
				default: []
			},
			mask: {
				type: Boolean,
				default: true
			},
			maskClick: {
				type: Boolean,
				default: true
			},
			mode: {
				type: String,
				default: 'left'
			}
		},
		data() {
			return {
				activeThemeBlock: true, // true - white false-black
				activeLangBlock: true, // true - zh false - en

			}
		},
		watch: {
			visibleSync: function(newVal) {
				if (newVal) {
					this.$refs.showRight.open();
				} else {
					this.$refs.showRight.close();
				}
			}
		},
		methods: {
			changeTheme(val) {
				// 0-white 1-black
				if (!val) {
					this.activeThemeBlock = true
					window.document.documentElement.setAttribute('data-theme', 'whiteBlueTheme');
					uni.setStorageSync('theme', 'whiteBlueTheme')
				} else {
					this.activeThemeBlock = false
					window.document.documentElement.setAttribute('data-theme', 'blackGoldTheme');
					uni.setStorageSync('theme', 'blackGoldTheme')
				}
			},
			changeLang(val) {
				// 0-ZH 1-EN
				if (!val) {
					this.activeLangBlock = true
				} else {
					this.activeLangBlock = false
				}
			},
			handleClick(val) {
				this.$emit('click', val)
			}
		},
		mounted() {
			const theme = uni.getStorageSync('theme')
			theme === 'whiteBlueTheme' ? this.activeThemeBlock = true : this.activeThemeBlock = false
		}

	}
</script>

<style lang="scss">
	@import '../../../common/icons/iconfont.css';

	.side-bar-list {
		width: 100%;
		height: calc(100% - 100rpx);

		.side-bar-item {
			width: 100%;
			height: 100rpx;
			display: flex;
			align-items: center;
			flex-direction: row;
			box-sizing: border-box;
			padding-top: 28rpx;
			padding-bottom: 28rpx;
			padding-left: 30rpx;

			.icon {
				width: 44rpx;
				height: 44rpx;
				margin-right: 20rpx;
			}

			.text {
				font-size: 32rpx;
				font-family: PingFang SC;
				font-weight: 400;
				// color: #1E262F;
			}
		}

		.active-side-bar-item {
			// background: #E5F7FE;

			.text {
				// color: #2EBEF3;
			}
		}
	}

	.footer {
		position: absolute;
		bottom: 0;
		width: 376rpx;
		height: 100rpx;
		// background: #E5F7FE;
		opacity: 1;
		display: flex;
		align-items: center;
		justify-content: space-around;

		.theme,
		.lang {
			width: 146rpx;
			height: 50rpx;
			// border: 1rpx solid #2EBEF3;

			opacity: 1;
			border-radius: 28rpx;
			display: flex;
			align-items: center;
			justify-content: space-around;
			flex-direction: row;

			.white,
			.black {
				width: 74rpx;
				height: 50rpx;
				position: relative;

				.sun,
				.moon,
					{
					z-index: 2;
					position: absolute;
					top: 50%;
					left: 50%;
					transform: translate(-50%, -50%);
					width: 30rpx;
					height: 30rpx;
				}

				.icona-zu1649,
				.icona-lujing2024 {
					z-index: 10;
					position: absolute;
					top: 50%;
					left: 50%;
					transform: translate(-50%, -50%);
					width: 30rpx;
					height: 30rpx;

				}

			}

			.en,
			.cn {
				font-size: 28rpx;
				font-family: PingFang SC;
				font-weight: bold;
				// color: #2EBEF3;
			}


		}

		.theme,
		.lang {
			.block {
				z-index: 1;
				position: absolute;
				left: 0;
				top: 0;
				width: 74rpx;
				height: 50rpx;
				// background: rgba(46, 190, 243, 0.08);
				border-radius: 28rpx;
				// border-right: 1rpx solid #2EBEF3;
				box-sizing: border-box;
				transition: left .2s ease-in-out;
			}

			.sunBlock,
			.zhBlock {
				left: 0rpx;
			}

			.moonBlock,
			.enBlock {
				left: 74rpx;
				border-right: none;
				// border-left: 2rpx solid #2EBEF3;
			}
		}
	}
</style>
