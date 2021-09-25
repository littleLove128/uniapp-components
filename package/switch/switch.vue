<template>
	<view class="on-off-switch">
		<view class="switch-on-off" 
		 :class="[{'is-checked': value},{'is-large':large}]" @click="handelClick">
			 <span class="switch__core" ref="core">
				<span class="switch__button"></span>
			</span>
		</view>
	</view>
</template>

<script>
	/**
	 * 开关组件
	 * value 代表开关，圆形小圈所在位置，不传 在左边显示，传在右边显示
	 * large 代表 圆形小圈 的大小。默认false 则小圈在背景颜色内，否则会超出
	*/
	export default{
		name:'switch-on-off',
		componentName:'switchOnOff',
		props:{
			value:{
				type:Boolean,
				default:false
			},
			large:{
				type:Boolean,
				default:false
			}
		},
		 mounted() {
		        // 修改开关颜色
		        this.setColor()
		},
		methods: {
			// async, await this.$nextTick() 是处理异步的,这是一种方式。也可以写成this.$nextTick(() => {this.setColor()})
			async handelClick() {
				this.$emit('click',!this.value)
				// 点击的时候修改颜色
				 this.value = !this.value;
				console.log('点击切换颜色',this.value)
				await this.$nextTick()
				this.setColor()
			},
			setColor() {
				if(this.activeColor || this.inactiveColor) {
					let color = this.value ? this.activeColor : this.inactiveColor
					this.$refs.core.style.borderColor = color
					this.$refs.core.style.backgroundColor = color
				}
			}
		},
	}
</script>

<style lang="scss" scoped>
	.on-off-switch{
		.switch-on-off{
			display: inline-block;
			align-items: center;
			position: relative;
			font-size: 14px;
			line-height: 20px;
			height: 20px;
			vertical-align: middle;
			.switch__input {
				position: absolute;
				width: 0;
				height: 0;
				opacity: 0;
				margin: 0;
			}
			.switch__core {
				margin: 0;
				display: inline-block;
				position: relative;
				width: 40px;
				height: 20px;
				// border: 1px solid #dcdfe6;
				outline: none;
				border-radius: 10px;
				box-sizing: border-box;
				// background: #dcdfe6;
				cursor: pointer;
				transition: border-color .3s,background-color .3s;
				vertical-align: middle;
				.switch__button {
					position: absolute;
					top: 1px;
					left: 1px;
					border-radius: 100%;
					transition: all .3s;
					width: 16px;
					height: 16px;
					// background: #fff;
				}
				
			}
		}
		.switch-on-off.is-large{
			.switch__button {
				position: absolute;
				// top: 1px;
				// left: 1px;
				border-radius: 100%;
				transition: all .3s;
				// width: 16px;
				// height: 16px;
				width: 24px;
				height: 24px;
				top: -3px;
				left: 0px;
				// background: #fff;
			}
		}
		.switch-on-off.is-checked {
		    .switch__core {
		        // border-color: #409eff;
		        // background: #409eff;
		        .switch__button {
		            transform: translate(20px);
		        }
		    }
		}
	}
	
</style>
