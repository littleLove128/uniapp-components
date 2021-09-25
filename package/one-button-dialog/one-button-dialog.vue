<template>
	<transition name="dialog-pop">
		<view class="one-button-dialog" v-show="visible" @click.self="handCloses">
			<view class="dialog-content" :class="['dialog-content--'+dialogType]" :style="{'min-height':height,'top':top}">
				<view class="dialog_header">
					<slot name="titles">
						<span class="dialog_title">{{title}}</span>
					</slot>
				</view>
				<view class="dialog_body" >
					<image :src="picture" v-if="picture"  mode=""></image>
					<slot></slot>
					<view v-if="contents" class="bodyContent">{{contents}}</view>
					<input style="background: none;outline: none;border: none;" 
					:type="inputType" 
					class="inputClass" 
					v-model="inputValue" 
					:placeholder="placeholder" 
					v-if="dialogType=='inputDialog'"/>
				</view>
				<view class="dialog_footer" >
					<text v-if="cancelText" class="buttonTextClass" @click="handCloses">{{cancelText}}</text>
					<text v-if="confirmText" class="buttonTextClass" @click="handleOk">{{confirmText}} </text>
					
					<view class="buttons" v-if="dialogType=='inputDialog'">
						<view class="left buttonTextClass" @click="handCloses">取消</view>
						<view class="right buttonTextClass" @click="handleOk">确认</view>
					</view>
				</view>
			</view>
		</view>
	</transition> 
</template>	

<script>
	/**
	 * visible 传入的值可以为bool 或者 String 类型， 是否弹出遮罩层
	 * title 弹框的名称
	 * height 白色内容区域宽高
	 * top 白色内容框距离顶部的距离
	 * picture 传入中间显示图片
	 * cancelText 文字按钮的实现
	 * dialogType= [comfirmDialog,inputDialog] 确认弹框和 输入框弹框
	 * contents 中间的内容
	 * inputType 输入框的类型  取值为 input 标签的值 ，默认为文本
	 * placeholder 输入框提示
	*/
export default{
   name:'one-button-dialog',
   componentName:'oneButtonDialog',
   data(){
	   return {
		   inputValue:''
	   }
   },
   props:{
	   visible: {
		   type: [Boolean,String],
		   default: false
	   },
	   title:{
		   type:String,
		   default:''
	   },
	   contents:{
		   type:String,
		   default:''
	   },
	   picture:{
		   type:String,
		   default:''
	   },
	   height: {
		   type: String,
		   default: '10%'
	   },
	   top: {
		   type: String,
		   default: '10vh'
	   },
	   cancelText:{
		   type:[Boolean,String],
		   default:''
	   },
	   confirmText :{
		  type:[Boolean,String],
		  default:'' 
	   },
	   dialogType:{
		   type:String,
		   default:'comfirmDialog'
	   },
	   inputType:{
		   type:String,
		   default:'text'
	   },
	   placeholder:{
		   type:String,
		   default:''
	   }
   },
	methods: {
	   handCloses() {
		   this.$emit('close',false)
	   },
	   handleOk(){
		   if(this.dialogType=='inputDialog'){
			   console.log('inputValue==',this.inputValue)
			   this.$emit('confirm',this.inputValue)
		   } else {
			   this.$emit('confirm')
		   }
	   }
	},
	
}
</script>

<style lang="scss" scoped>
.dialog-pop-enter-active {
  animation: dialog-fade-in .4s;
}
.dialog-pop-leave-active {
  animation: dialog-fade-out .4s;
}
@keyframes dialog-fade-in {
  0% {
    transform: translate3d(0, -20px, 0);
    opacity: 0;
  }
  100% {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
}
@keyframes dialog-fade-out {
  0% {
    transform: translate3d(0, 0, 0);
    opacity: 1;
  }
  100% {
    transform: translate3d(0, -20px, 0);
    opacity: 0;
  }
}
	
.one-button-dialog{
	position: fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	overflow: auto;
	margin: 0;
	z-index: 2001;
	.dialog-content{
		position: relative;
		margin: 15vh auto 50px;
		box-sizing: border-box;
		width: 90%;
		border-radius: 10px;
		
		.dialog_title{
			text-align: center;
			font-size: 36rpx;
			font-weight: bold;
		}
	}
	.dialog-content--comfirmDialog{
		padding: 15px;
		.dialog_body{
			image{
				width: 120rpx;
				height: 120rpx;
				margin: 15px  auto ;
			}
			.bodyContent{
				width: 100%;
				padding-bottom: 10px;
				font-size: 28rpx;
				margin: 15px  auto ;
			}
		}
		.dialog_footer{
			display: flex;
			flex-direction: row;
			justify-content: flex-end;
		}
		.buttonTextClass{
			font-size: 32rpx;
			font-weight: 500;
		}
		.buttonTextClass:nth-child(2){
			margin-left: 50rpx;
		}
	}
	
	.dialog-content--inputDialog{
		.dialog_title{
			margin-top: 15px;
		}
		.dialog_body{
			width: 90%;
			// border: 1px solid #BEBFC4;
			margin:  15px  auto ;
			padding-top: 8rpx;
			padding-bottom: 8rpx;
			border-radius: 6rpx;
			.inputClass{
				text-indent: 10rpx;
				font-size: 28rpx;
				// color: #1E262F;
				
			}
			input::-webkit-input-placeholder{   /* 使用webkit内核的浏览器 */
				// color: #BEBFC4;
				font-size: 28rpx;
				text-indent: 10rpx;
			}
			input:-moz-placeholder{    /* Firefox版本4-18 */
				// color: #BEBFC4;
				font-size: 28rpx;
				text-indent: 10rpx;
			}              
			input::-moz-placeholder{    /* Firefox版本19+ */
				// color: #BEBFC4;
				font-size: 28rpx;
				text-indent: 10rpx;
			}              
			input:-ms-input-placeholder{   /* IE浏览器 */
				// color: #BEBFC4;
				text-indent: 10rpx;
				font-size: 28rpx;
				text-indent: 10rpx;
			} 
		}
		.dialog_footer{
			border-top: 1px solid #EDEDED;
			.buttons{
				display: flex;
				flex-direction: row;
				.left,.right{
					width: 50%;
					display: flex;
					justify-content: center;
					align-items: center;
					padding-top: 15px;
					padding-bottom: 15px;
				}
				.left{
					// border-right: 1px solid #EDEDED;
				}
			}
		}
	
	}
	
	 
}



</style>
