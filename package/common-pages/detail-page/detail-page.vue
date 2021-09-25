<template>
	<view class="detail-page">
		<view class="titlePosition">
			<uni-title :title="title"  type="h1"></uni-title>
		</view>
		<view class="authorPosition">
			<view class="left">
				{{author}}
			</view>
			<view class="right">
				{{time}}
			</view>
		</view>
		<view class="contentPosition">
			<text v-if="content.indexOf('</')==-1" v-html="content"></text>
			<text v-else>{{content}}</text>
		</view>
	</view>
</template>

<script>
	/**
	 * 详情页面，使用的时候直接使用 <detail-page></detail-page>
	 * title 传入标题
	 * author 传入作者
	 * time 传入时间
	 * content 传入内容，html格式
	*/
   export default {
	   name:'detail-page',
	   componentName:'detailPage',
	   props:{
		   title:{
			   type:String,
			   default:''
		   },
		   author:{
			   type:String,
			   default:''
		   },
		   time:{
			   type:String,
			   default:''
		   },
		   content:{
			   type:String,
			   default:''
		   }
	   }
   }
</script>

<style lang="scss" scoped>
.detail-page{
	margin: 20px 15px 15px 15px;
	.authorPosition{
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		margin-top: 15px;
		margin-bottom: 20px;
		.left{
			font-size: 26rpx;
			// color: #2EBEF3;
		}
		.right{
			font-size: 24rpx;
			// color: #BEBFC4;
		}
	}
	.contentPosition{
		font-size: 24rpx;
		font-weight: 500;
		line-height: 30rpx;
		// color: #1E262F;
	}
}
</style>
