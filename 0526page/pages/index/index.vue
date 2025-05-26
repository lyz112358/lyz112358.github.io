<template>
    <view class="m-tab">
        <view class="demo-block">
            <!-- <view class="title">基础用法</view> -->
            <view>
                <view class="tab">
                    <zb-tab
                            :height="50"
                            lineWidth="50%"
                            :activeStyle="{
								fontWeight:'normal',
								fontSize:'16px',
								color:'#17c9cd',
								transform: 'scale(1.1)'
							  }" :data="list0" v-model="active0">
                    </zb-tab>
                </view>
                <view class="card" v-for="(item,index) in list0" v-show="item.value===active0" :key="item.value">
					<view v-if="item.value==0">
						<view style="font-size: 14px; line-height:20px; width: 90%; color: #df010e;">申请已截止，可点击不通过的申请信息进行修改并重新提交<br>
请已审核通过未领取校园通行证的车辆抓紧领取，保卫处统一(周五)集中审核，审核通过的车辆(周一)可到紫荆办公楼一楼112办公室领取校园通行证</view>
<view class="content">
	<image style="width: 63px; height: 63px; position: relative; top:-55px; left: -55px;"  src="../../static/img/bg.png"></image>
	<view style="position: relative; top: -115px; left: 230px; font-size:12px; color: #aeca80;">审核通过</view>
	<view style="line-height: 28px; margin-top:-80px">
		<view style="display: flex; align-items: center;">
			<i class="iconfont" style="margin-right: 10px;">&#xe627;</i> 姓名：张文祥<br>
		</view>
		
		<view style="display: flex; align-items: center;">
			<i class="iconfont" style="margin-right: 10px;">&#xe682;</i> 学号：20233002501</view>
		<view style="display: flex; align-items: center;">
					<i class="iconfont" style="margin-right: 10px;">&#xe6b9;</i> 联系方式：19891352015</view>
		<view style="display: flex; align-items: center;">
					<i class="iconfont" style="margin: 0 8px 0 2px;">&#xe651;</i> 学院名称：土木工程</view>
		<view style="display: flex; align-items: center;">
					<i class="iconfont" style="font-size: 28px; margin-right: 5px;">&#xe630;</i> 书院名称：子衿书院</view>
		<view style="display: flex; align-items: center;">
					<i class="iconfont" style="font-size: 16px; margin: 0 12px 0 5px;">&#xe603;</i>车牌号：海口-1205130</view>
	</view>
</view>
</view>
					<view v-if="item.value==1">
						<view style="font-size: 14px; line-height:20px; width: 90%; color: #df010e;">申请已截止，可点击不通过的申请信息进行修改并重新提交<br>
						请已审核通过未领取校园通行证的车辆抓紧领取，保卫处统一(周五)集中审核，审核通过的车辆(周一)可到紫荆办公楼一楼112办公室领取校园通行证</view>
						<view style="text-align: center; margin: 70px 0 0 -25px;">
							<image style="width: 102px; height: 107px;" src="../../static/img/empty.png"></image>
							<view style="margin-top: 20px;">暂无信息</view>
						</view>
					</view>
                    </view>
            </view>
        </view>

    </view>
</template>

<script>
import {
    list0,
    list1,
    list2
} from './data'

export default {
    components: {},
    data() {
        return {
            active0: 0,
            active: 1,
            active1: 0,
            active3: 1,
            list1,
            list0,
            list2,
        }
    },
    onLoad() {

        let obj = [
            {
            typeInfoList:[
                {
                    typeId:11,
                    typeName:''
                }
            ]
        }]



    },
    mounted() {},
    methods: {

        tabClick(item) {
            console.log(this.active, item)
            uni.showToast({
                icon: "none",
                title: `点击${item.name}`,
                duration: 2000,
            });
        }
    }
}
</script>

<style lang="scss">
.m-tab {
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  overflow-y: auto;
  overflow-x: hidden;
  padding: 0rpx 20rpx 60rpx 20rpx;
  background-color: #f8f8f8;
  display: flex;
  box-sizing: border-box;

  flex-direction: column;
}
@font-face {
  font-family: 'iconfont';
  src: url('../../static/font/iconfont.ttf?t=1748247495795') format('truetype');
}
.iconfont {
  font-family: "iconfont" !important;
  color: #17c9cd;
  font-size: 24px;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.demo-block {
  .title {
    font-weight: 400;
    font-size: 14px;
    line-height: 16px;
    margin: 0;
    padding: 16px 16px 16px;
  }
}

.content {
  background: white;
  padding: 55px;
  margin-top: 37px;
  border-radius: 10px;
  width: 63%;
}

.tab {
  width: 100%;
  //height: 90rpx;
  display: flex;
  align-items: center;
}

.card {
  width: 100%;
  padding: 24px 20px;
}
</style>