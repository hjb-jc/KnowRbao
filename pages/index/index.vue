<template>
	<view class="content">
		<view class="uni-list">
			<swiper style="width: 100%; height: 40%;" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="500">
					<swiper-item v-for="item in news" :key="item">
						<image :src="item.images[0]" @tap="opendet" :data-newsid="item.id"></image>
					</swiper-item>
				</swiper>
			<!-- <navigator url="">页面跳转</navigator> -->
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in news" :key="index" @tap="opendet" :data-newsid="item.id">
				<view class="uni-media-list">
						<image class="uni-media-list-logo" :src="item.images[0]"></image>
						<view class="uni-media-list-body">
							<view class="uni-media-list-text-top">{{item.title}}</view>
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
		line-height: auto;
	}

	.uni-media-list-text-top {
		line-height: 2em;
	}
	.uni-media-list-logo{
	}
</style>
