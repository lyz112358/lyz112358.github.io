<template>
	<view class="van-tabs__nav van-tabs__nav--line">
		<view class="van-tab" :class="[{
            'van-tab--active':activeIndex===index
          }]" ref="tab" v-for="item,index in data" :key="index" @click="changeTab(index)">
			<view class="van-tab__text van-tab__text--ellipsis">{{item.name}}</view>
		</view>
		<view class="van-tabs__line" :style="[lineStyle]">

		</view>
	</view>
</template>

<script>
	export default {
		props: {
		  value:null,
			data: {
				type: Array,
				default: () => []
			}
		},
    watch:{

    },
		data() {
			return {
				lineStyle:{},
				activeIndex: 0
			}
		},
		mounted(){
			this.setLine()
		},
		methods: {
			async getWidth(){
				return new Promise((resolve)=>{
					let view = uni.createSelectorQuery().in(this).selectAll(".van-tab");
					view.boundingClientRect(data => {
						resolve(data)
					}).exec();
				})
			},
			async setLine() {
				let titles = await this.getWidth()
				let title= titles[this.activeIndex]
				 const left = title.left+ title.width / 2;
				 const lineStyle = {


				          transform: `translateX(${left}px) translateX(-50%)`,
				        };
				console.log('tab',titles)
				  this.lineStyle = lineStyle;
			},
			changeTab(index) {
				this.activeIndex = index
				this.setLine()
			}
		}
	}
</script>

<style lang="scss">
	.van-tabs__nav--line {
		box-sizing: content-box;
		height: 100%;
		padding-bottom: 15px;
	}

	.van-tabs__nav {
		width: 100%;
		position: relative;
		display: -webkit-box;
		display: -webkit-flex;
		display: flex;
		background-color: #fff;
		-webkit-user-select: none;
		user-select: none;
	}

	.van-tab {
		position: relative;
		display: -webkit-box;
		display: -webkit-flex;
		display: flex;
		-webkit-box-flex: 1;
		-webkit-flex: 1;
		flex: 1;
		-webkit-box-align: center;
		-webkit-align-items: center;
		align-items: center;
		-webkit-box-pack: center;
		-webkit-justify-content: center;
		justify-content: center;
		box-sizing: border-box;
		padding: 0 4px;
		color: #646566;
		font-size: 14px;
		line-height: 20px;
		cursor: pointer;
	}

	.van-tab__text--ellipsis {
		display: -webkit-box;
		overflow: hidden;
		-webkit-line-clamp: 1;
		-webkit-box-orient: vertical;
	}

	.van-tab--active {
		color: #323233;
		font-weight: bold;

	}

	.van-tabs__line {
		position: absolute;
		bottom: 15px;
		left: 0;
		z-index: 1;
		width: 40px;
		height: 3px;
		background-color: #ee0a24;
		border-radius: 3px;
		transition-duration: 0.3s;
	}
	// .van-tab:nth-child(1){
	// 	flex: 0;
	// 	flex-shrink: 0;
	// 	flex-basis: 200px;
	// }
</style>
