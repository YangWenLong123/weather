<template>
	<view class="container">
		<scroll-view scroll-y="true" class="container-scroll">
			<view class="container-wrap" v-if="cityList.length > 0">
				<view
					class="container-list"
					v-for="(item,index) in cityList"
					:key="index"
					@click="fnGetCode(item)"
				>
					{{ item['中文名']}}
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	const city = require('@/common/json/city.json');
	export default {
		data () {
			return {
				cityList: []
			}
		},
		onLoad() {
			this.cityList = city ? city : [];
			
			// this.init();
		},
		methods: {
			fnGetCode (item) {
				uni.$emit('sendCode', JSON.stringify(item));
				// console.log(item,'item')
				uni.navigateBack();
			},
			init () {
				let list = [];
				if(city.length > 0) {
					city.map(item=>{
						list.push({
							city: item['中文名'],
							adcode: item.adcode
						})
					})
					this.cityList = list;
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	page{
		width: 100%;
		height: 100%;
		background-color: #FFFFFF;
	}
	.container {
		height: 100%;
		display: flex;
		flex-direction: column;
		.container-scroll {
			flex: 1;
			.container-wrap {
				width: 750rpx;
				padding: 30rpx;
				box-sizing: border-box;
				.container-list {
					margin: 0 30rpx;
					height: 90rpx;
					line-height: 90rpx;
					background-color: #F4F4F4;
					margin-bottom: 40rpx;
					font-size: 30rpx;
					box-sizing: border-box;
					padding-left: 30rpx;
				}
				
			}
		}
	}
</style>
