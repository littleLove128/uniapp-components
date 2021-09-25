<template>
	<view class="input-box"  >
		<view class="input-box-content" :class="[{'has-bg':bgColor},{'is-circle':circle}]" :style="{'border-color':borderColor}">
			<view class="fix-content" v-if="labelText||icon">
				<text :class="['iconfont',icon]" v-if="icon" style="margin-right: 10px;font-size: 44rpx;"></text>
				<text class="labelStyle">{{labelText}}</text>
			</view>
			<slot>
				
			</slot>
		</view>
	</view>
</template>

<script>
	/**
	 * bgColor 显示背景颜色
	 * icon 传入第一个图标
	 * labelText 传入标签的文字 比如 用户名这类似的
	 * borderColor 传入底部边框的颜色
	 * circle 是否圆形显示
	 * 
	*/
   export default {
	   name:'input-box',
	   componentName:'inputBox',
	   props:{
		   bgColor:{
			   type: Boolean,
			   default:false
		   },
		   circle:{
			   type: Boolean,
			   default:false
		   },
		   icon:{
			  type:String,
			  default:'' 
		   },
		   labelText:{
			   type:String,
			   default:'' 
		   },
		   borderColor:{
			   type:String,
			   default:'#EDEDED'
		   }
	   },
	   methods:{
		   
	   }
   }
</script>

<style lang="scss" scoped>
@import  '../../common/icons/iconfont.css';
.input-box{
	.input-box-content{
		width: 95%;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		border-bottom: 1px solid;
		padding-bottom: 10px;
		.fix-content{
			display: flex;
			flex-direction: row;
			justify-content: flex-start;
			align-items: center;
			margin-right: 10px;
			.labelStyle{
				font-size: 30rpx;
				// color: #1E262F;
				width: 100rpx;
			}
		}
	}
	.input-box-content.has-bg{
		border:none;
		// background-color: #E8EEF1;
		padding-top: 10px;
		padding-left: 10px;
		border-radius: 5px;
		
	}
	.input-box-content.is-circle{
		border-radius: 100rpx;
	}
	
}

</style>
