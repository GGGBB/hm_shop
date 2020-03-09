<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view 
				@click="leftClickHandle(index)"
				:class="active===index?'active':''" 
				v-for="(item, index) in cates" 
				:key="item.id">
				{{item.title}}
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				cates: [],
				active: 0
			}
		},
		methods: {
			async getPicsCate() {
				const res = await this.$myRuquest({
					url: '/api/getimgcategory'
				})
				this.cates = res.data.message
			},
			leftClickHandle(index) {
				this.active = index
			}
		},
		onLoad() {
			this.getPicsCate()
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
	.pics{
		height: 100%;
		.left{
			width: 200rpx;
			height: 100%;
			border-right: 1px solid #eee;
			view{
				height: 120rpx;
				line-height: 120rpx;
				color: #333;
				text-align: center;
				font-size: 30rpx;
				border-top: 2rpx solid #eee;
			}
			.active{
				background: $shop-color;
				color: #FFFFFF
			}
		}
	}
</style>
