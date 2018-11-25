<template>
	<view class="content">
		<view class="title">{{title}}</view>
		<view class="api-centent">
			<rich-text class="richText" :nodes="bodys"  style="width: 100%; height: 100%;"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '',
				bodys: '',
				share_url:''
			}
		},
		onLoad: function(e) {
			console.log(e.newsid);
			uni.request({
				url: 'https://news-at.zhihu.com/api/4/news/' + e.newsid,
				method: 'GET',
				data: {},
				success: res => {
					/* console.log(res.data); */
					
				/* 	this.title = res.data.title; */
				
					this.bodys = res.data.body;
					/* this.bodys = this.bodys.indexOf("“");
					console.log(this.bodys); */
					
					//replace()方法在字符串中用一些字符替换另一些字符
					//stringObject.replace(regexp/substr,replacement)
					this.bodys = this.bodys.replace(/“/g, '"');
					this.bodys = this.bodys.replace(/”/g, '"');
					
					
				},
				fail: () => {
					console.log("eeeeee");
				},
				complete: () => {}
			});
		}
	}
</script>

<style>
	.content {
		/* flex-wrap:wrap允许下面元素自动换行 */
		padding: 10upx 2%;
		width: 96%;
		flex-wrap: wrap;
	}

	.title {
		line-height: 2em;
		font-weight: 700;
		font-size: 38upx;
	}

	.api-centent {
		line-height: 2em;
	}
</style>
