<template>
	<view v-show="show" ref='domCont'>
		<view @click.self="closeOverlay" ref='overlay' id="overlay" class="overlay" :style="{'--z-index':zIndex}">
			<slot></slot>
		</view>
	</view>
</template>

<script>
	/* 
		zIndex:Number 
		show:Boolean
		close:Function 
	 */
	export default {
		name: "OverLay",
		componentName: "OverLay",
		props: {
			zIndex: {
				type: Number,
				default: 999
			},
			show: {
				type: Boolean,
				default: false
			},

		},
		watch: {
			show: function(newVal) {
				if (newVal) {
					setTimeout(() => {
						this.$refs.overlay.$el.style.opacity = '0.7'
					}, 100)
				} else {
					this.$refs.overlay.$el.style.opacity = '0'
				}
			}
		},
		methods: {
			closeOverlay() {
				const _this = this
				_this.$emit('close')

			}
		}
	}
</script>

<style lang='scss' scoped>
	.overlay {
		position: fixed;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		background-color: #000;
		opacity: 0;
		z-index: var('--z-index');

		transition: opacity .3s linear;
	}
</style>
