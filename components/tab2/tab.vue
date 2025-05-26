<template>
	<view class="van-tabs__nav van-tabs__nav--line" :style="{
	  '--zb-tabs-bottom-bar-color':lineColor
    }">
		<view class="van-tab" :class="[{
            'van-tab--active':activeIndex===index,
            'van-tab--disabled':item.disabled,
          }]" ref="tab" v-for="item,index in data" :key="item.value" @click="changeTab(item,index)">
			<view class="van-tab__text van-tab__text--ellipsis" :style="[activeIndex===index&&activeStyle]">
				{{item.name}}</view>
		</view>
		<view class="van-tabs__line" :style="[lineStyle]">

		</view>
	</view>
</template>

<script>
	export default {
		options: {
		 // #ifdef MP-WEIXIN
		   // 微信小程序中 options 选项
		   multipleSlots: true, //  在组件定义时的选项中启动多slot支持，默认启用
		   styleIsolation: "isolated",  //  启动样式隔离。当使用页面自定义组件，希望父组件影响子组件样式时可能需要配置。具体配置选项参见：微信小程序自定义组件的样式
		   addGlobalClass: true, //  表示页面样式将影响到自定义组件，但自定义组件中指定的样式不会影响页面。这个选项等价于设置 styleIsolation: apply-shared
		   virtualHost: true,  //  将自定义节点设置成虚拟的，更加接近Vue组件的表现。我们不希望自定义组件的这个节点本身可以设置样式、响应 flex 布局等，而是希望自定义组件内部的第一层节点能够响应 flex 布局或者样式由自定义组件本身完全决定
		 // #endif
		 },
		props: {
			lineWidth: {
				type: String,
				default: '#ee0a24'
			},
			lineColor: {
				type: String,
				default: '#ee0a24'
			},
			activeStyle: {
				type: Object,
				default: () => {}
			},
			value: {
				type: [Number, String],
				default: 0,
			},
			data: {
				type: Array,
				default: () => []
			}
		},

		data() {
			return {
				lineStyle: {},
				activeIndex: this.value
			}
		},
		mounted() {
			this.setLine()
		},
		watch: {
      value: {
				handler(val) {
					if (val !== this.value) {
						this.setCurrentIndexByName(val);
					}
				},
				immediate: true
			}
		},
		methods: {
			isNumeric(val) {
				return /^\d+(\.\d+)?$/.test(val);
			},
			addUnit(value) {
				if (value == null) {
					return undefined
				}
				value = String(value);
				return this.isNumeric(value) ? `${value}px` : value;
			},
			setCurrentIndexByName(val) {
				this.activeIndex = this.data.findIndex(item => item.value === val)
			},
			async getWidth() {
				return new Promise((resolve) => {
					let view = uni.createSelectorQuery().in(this).selectAll(".van-tab");
					view.boundingClientRect(data => {
						resolve(data)
					}).exec();
				})
			},
			async setLine() {
				let titles = await this.getWidth()
				let title = titles[this.activeIndex]
				const left = title.left + title.width / 2;
				const lineStyle = {
					width: this.addUnit(this.lineWidth),
					transform: `translateX(${left}px) translateX(-50%)`,
				};
				this.lineStyle = lineStyle;
			},
			changeTab(item, index) {
			  if(item.disabled)return
				this.activeIndex = index
				this.setLine()
				this.$emit('input', item.value);
				this.$emit('change', {
					...item
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	$zb-tabs-bottom-bar-color: var(--zb-tabs-bottom-bar-color);

	.van-tabs__nav--line {
		box-sizing: content-box;
		height: 100%;
		//padding-bottom: 15px;
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
		/* #ifdef H5 */
		cursor: pointer;
		/* #endif */

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
		bottom: 2px;
		left: 0;
		z-index: 1;
		width: 40px;
		height: 3px;
		background-color: $zb-tabs-bottom-bar-color;
		border-radius: 3px;
		transition-duration: 0.3s;
	}
  .van-tab--disabled{
    cursor: not-allowed;
    .van-tab__text{
      color: #c8c9cc;
    }
  }

	// .van-tab:nth-child(1){
	// 	flex: 0;
	// 	flex-shrink: 0;
	// 	flex-basis: 200px;
	// }
</style>
