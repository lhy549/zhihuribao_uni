<template>
	<view class="content">
		<view class="title">{{title}}</view>
		<view class="art-content">
			<rich-text class="rich-text" :nodes="strings"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title:'',
				strings:''
			};
		},
		onLoad:function(e){
			console.log(e);				
			uni.request({
				//url: 'https://news-at.zhihu.com/api/4/news/latest/9702106',
				url: 'https://news-at.zhihu.com/api/4/news/'+e.id,
				method: 'GET',
				data: {},
				success: res => {
					//console.log(res.data);
					this.title = res.data.title;
					this.strings = res.data.body;
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.content{
	padding: 10upx 2%;
	width: 96%;
	flex-wrap: wrap;
}
.art-content{
	line-height: 2em;
	font-size: 24upx;
}
.title{
	line-height: 2em;
	font-weight: 600;
	font-size: 30upx;
}
</style>
