<template>
	<view class="bc-drop">
		<view @click="toggle">
			<slot name="title">
				{{title}}
				<!-- {{show}} -->
			</slot>
		</view>
		<view :class="[contentClass,'bc-drop-content',dropSize]" v-show="show" :style="[contentColStyle]"
			@click="close">
			<slot>
				<view :class="['bc-drop-item', border && index !== list.length - 1 && 'bc-drop-item-border', dropItemSize]" :style="[dropItemStyle,item.style]"
					@click="clickItem(item,index)" v-for="(item,index) in list" :key="index">
					{{item.name}}
				</view>
			</slot>
		</view>
		<view class="bc-drop-mask" v-if="show" @click="close" :style="{zIndex: zIndex}"></view>
	</view>
</template>

<script>
	export default {
		name: 'fDropMenu',
		data() {
			return {
				contentClass: "",
				contentColStyle: {
					"max-width": isNaN(Number(this.maxWidth)) ? this.maxWidth : this.maxWidth + "rpx",
					'border-radius': this.radius + 'rpx',
					zIndex: this.zIndex + 1
				}
			};
		},
		computed: {
			show: {
				get() {
					return this.value;
				},
				set(value) {
					this.$emit("input", value);
					this.$emit("change", value);
				}
			},
			dropSize() {
				return this.size ? `bc-drop-${this.size}` : ''
			},
			dropItemSize() {
				return this.size ? `bc-drop-item-${this.size}` : ''
			},
			dropItemStyle() {
				return {
					textAlign: this.align,
				}
			}
		},
		props: {
			value: Boolean,
			title: String,
			maxWidth: [Number, String],
			radius: {
				type: Number,
				default: 12
			},
			list: {
				type: Array,
				default: () => ([])
			},
			border: {
				type: Boolean,
				default: false
			},
			align: {
				type: String,
				default: "center",
				validator(val) {
					return ['center', 'left', 'right'].indexOf(val) !== -1;
				}
			},
			size: {
				type: String,
				validator(val) {
					return ['', 'mini', 'small', 'large'].indexOf(val) !== -1;
				}
			},
			zIndex: {
				type: Number,
				default: 10001
			}
		},
		methods: {
			close() {
				this.show = false;
			},
			toggle() {
				this.show = !this.show;
				this.updatePosition();
			},
			clickItem(item, index) {//将选中的内容返回父组件
				this.$emit("click",item, index);
				this.close();
			},
			updatePosition() {
				console.log('更新高度')
				// 获取屏幕宽高 data.windowWidth ，data.windowHeight
				uni.getSystemInfo({
					success: (data) => {
						if (!data) {
							return;
						}
				
						let query = uni.createSelectorQuery().in(this);
				
						// 获取开关宽高
						query.select('.bc-drop').boundingClientRect(dom => {
							let {
								left,
								top
							} = dom;
				
							/* 如果按钮的位置在屏幕宽度的40%内，下拉内容居左
							如果按钮的位置在屏幕宽度的60%内，下拉内容居右
							如果按钮的位置 <= 屏幕高度的50%内，下拉方向向下
							如果按钮的位置 >屏幕高度的50%内，下拉方向向上 */
				
							if (left / data.windowWidth < 0.5) {
								this.contentClass = "left";
							} else {
								this.contentClass = "right";
							}
				
							if (top / data.windowHeight < 0.5) {
								delete this.contentColStyle.bottom
								this.contentColStyle.top = dom.height + 5 + 'px';
							} else {
								delete this.contentColStyle.top
								this.contentColStyle.bottom = dom.height + 5 + 'px';
							}
						}).exec();
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.bc-drop {
		display: inline-block;
		position: relative;

		.bc-drop-mask {
			position: fixed;
			left: 0;
			right: 0;
			top: 0;
			bottom: 0;
		}

		.bc-drop-content {
			// color: $uni-text-color;
			position: absolute;
			// background: #FFFFFF;
			z-index: 10002;
			box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
			padding: 0 20rpx;
			overflow: hidden;
			text-align: center;

			&.left {
				left: 0;
			}

			&.right {
				right: 0;
			}
		}


		.bc-drop-small {
			padding: 0 16rpx;
		}

		.bc-drop-mini {
			padding: 0 10rpx;
		}

		.bc-drop-large {
			padding: 0 34rpx;
		}
	}

	.bc-drop-item {
		padding: 20rpx 0;
		white-space: nowrap;
		min-width: 120rpx;
		font-size: 28rpx;
	}

	.bc-drop-item-border {
		position: relative;

		&::after {
			content: "";
			position: absolute;
			height: 2rpx;
			width: 100%;
			// background: #f1f1f1;
			left: 50%;
			bottom: 0;
			transform: translateX(-50%);
		}
	}

	.bc-drop-item-small {
		padding: 14rpx 0;
		min-width: 100rpx;
	}

	.bc-drop-item-mini {
		padding: 10rpx 0;
		min-width: 80rpx;
		font-size: 24rpx;
	}

	.bc-drop-item-large {
		padding: 24rpx 0;
		min-width: 160rpx;
		font-size: 32rpx;
	}
</style>
