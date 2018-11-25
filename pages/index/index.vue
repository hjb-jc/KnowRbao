<template>
	<view class="content">
		<view class="uni-list">
			<!-- <navigator url="">页面跳转</navigator> -->
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in news" :key="index" @tap="opendet" :data-newsid="item.id">
				<view class="uni-media-list">
			
						<image class="uni-media-list-logo" :src="item.images[0]"></image>
						<view class="uni-media-list-body">
							<view class="uni-media-list-text-top">{{item.title}}</view>
							<view class="uni-media-list-text-bottom uni-ellipsis">{{item.ga_prefix }}</view>
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
				news: []
			};
		},
		onLoad: function() {
			uni.request({
				url: 'https://news-at.zhihu.com/api/4/news/latest',
				method: 'GET',
				data: {},
				success: res => {
					//console.log(res);
					this.news = res.data.stories;
				}
			});
		},
		methods: {
			opendet(e){
				var newid = e.currentTarget.dataset.newsid;
				console.log(newid);
				
				uni.navigateTo({
					url: '../index/details?newsid='+newid
				});
				
			}
		}
	}
</script>

<style>
	.uni-media-list-body {
		height: auto;
	}

	.uni-media-list-text-top {
		line-height: 1.6em;
	}
</style>
