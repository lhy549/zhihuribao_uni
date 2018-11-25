<template>
	<view class="content">
		<text class="title">{{title}}</text>
	</view>
</template>
<template>
	<view class="content">
		
		<view class="uni-list">
			<swiper>
				<block v-for="(item,index) in stories" :key="index">
					<swiper-item>
					<image :src="item.images" class="slide-image" width="355" height="150"/>
					</swiper-item>
				</block>
			</swiper>
			
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in stories" :key="index" @tap="openinfo" :data-newsid="item.id">								
				<view class="uni-media-list">
					<image class="uni-media-list-logo" :src="item.images"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
						<view class="uni-media-list-text-bottom uni-ellipsis">{{item.ga_prefix}}</view>
					</view>
				</view>
			</view>
		</view>
	</view>	
</template>
<script>
	export default {
		data() {
			return {
				 stories : []
			};
		},
		onLoad:function(){
			uni.request({
				url: 'https://news-at.zhihu.com/api/4/news/latest',
				method: 'GET',
				data(){},
				success: res => {
					console.log(res.data.stories);
					this.stories = res.data.stories;
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods:{
			openinfo(e){
				
				var newsid = e.currentTarget.dataset.newsid;
				console.log(newsid);
				uni.navigateTo({
					url: '../info/info?id='+newsid					
				})
			}
		},
	}
</script>

<style>
	.uni-media-list-text-top{
		line-height: 1.5em;
	}
	.uni-media-list-body{
		
		height: auto;
	}
	.content {
		flex: 1;
		justify-content: center;
		align-items: center;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
