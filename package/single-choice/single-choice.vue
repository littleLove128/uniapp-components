<template> 
   <view class="single-choice"  >
   <view class="single-choice-content" :class="{
	   'is-selected':selected
   }" :style="{'width':width,'height':width}" @click="handleClick">
   	
   </view>
	   
   </view>
</template>

<script> 
/**
 * 圆环选中或者未选中
 * 
*/
export default{
	name:'single-choice',
	componentName:'singleChoice',
	props:{
		width:{
			type:String,
			default:'36rpx'
		},
		selected:{
			type:[Boolean,String],
			default:false
		}
	},
	methods:{
		handleClick(){
			this.$emit('click');
		}
	}
}
</script>

<style lang="scss" scoped>
	.single-choice{
		.single-choice-content{
			// border: 2rpx solid #BEBFC4;
			border-radius: 50%;
			box-sizing: border-box;
		}
		.single-choice-content.is-selected{
			// border: 10rpx solid #BEBFC4;
			border-radius: 50%;
			box-sizing: border-box;
		}
	}
</style>
