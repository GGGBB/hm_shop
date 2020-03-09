<template>
	<view class="home">
		
		<swiper indicator-dots circular>
			<swiper-item v-for="item in swipers" :key="item.id">
				<image :src="item.img"></image>
			</swiper-item>
		</swiper>		
		
		<!-- 导航区域 -->
		<view class="nav">
			<view class="nav_item" v-for="(item, id) in navs" :key="id" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{item.title}}</text>
			</view>
		</view>
		
		<!-- 推存商品 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goods-list :goods="goods"></goods-list>
		</view>
		
	</view>
</template>

<script>
	import goodsList from '@/components/goods.list/goods.list.vue'
	export default {
		data() {
			return {
				swipers: [],
				goods: [],
				navs: [
					{
						id: 0,
						icon: 'iconfont icon-ziyuan',
						title: '超市',
						path: '/pages/goods/goods'
					},{
						id: 1,
						icon: 'iconfont icon-guanyuwomen',
						title: '联系我们',
						path: '/pages/contact/contact'
					},{
						id: 2,
						icon: 'iconfont icon-tupian',
						title: '社区图片',
						path: '/pages/pics/pics'
					},{
						id: 3,
						icon: 'iconfont icon-shipin',
						title: '学习视频',
						path: '/pages/videos/videos'
					}
				]
			}
		},
		onLoad() {
			this.getSwipers()
			this.getHotGoods()
		},
		components: {"goods-list": goodsList},
		methods: {
			// 获取轮播图的数据
			async getSwipers() {
				const res = await this.$myRuquest({
					url: '/api/getlunbo'
				})
				this.swipers = res.data.message
			},
			// 获取热门商品列数据
			async getHotGoods(){
				const res = await this.$myRuquest({
					url: '/api/getgoods?pageindex=1'
				})
				this.goods = res.data.message
			},
			// 导航点击的处理函数
			navItemClick(url) {
				uni.navigateTo({
					url
				})
			}
		}
	}
</script>

<style lang="scss">
	.home{
		swiper{
			width: 750rpx;
			height: 380rpx;
			image{
				height: 100%;
				width: 100%;
			}
		}
		.nav{
			display: flex;
			.nav_item{
				width: 25%;
				text-align: center;
				view{
					width: 120rpx;
					height: 120rpx;
					background: $shop-color;
					border-radius: 60rpx;
					margin: 20rpx auto;
					line-height: 120rpx;
					color: #FFFFFF;
					font-size: 50rpx;
				}
				text{
					font-size: 30rpx
				}
			}
		}
		.hot_goods {
			background: #eee;
			overflow: hidden;
			margin-top: 20rpx;
			.tit{
				height: 100rpx;
				line-height: 100rpx;
				color: $shop-color;
				text-align: center;
				letter-spacing: 40rpx;
				background: #fff;
				margin: 8rpx auto;
			}
		}
	}
</style>
