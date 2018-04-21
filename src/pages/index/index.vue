<template>
	<div class="container">
		<navbar :tabs="tabs" @tabChange="tabChange"></navbar>
		<vlist :listData="activeList" :label="tabLabel"></vlist>
		<!-- <button @click="clearStorage">清除所有数据</button> -->
		<footer>
			<button>明细</button>
			<a href="/pages/billinput/main" class="home">铅笔</a>
			<button>结算</button>
		</footer>
	</div>
</template>

<script>
import card from '@/components/card'
import vlist from '@/components/list'
import navbar from '@/components/navbar'
export default {
	
	components: {
		card,
		vlist,
		navbar
	},

	data () {
		return {
			motto: 'Hello World',
			userInfo: {},
			tabs: [
				{
					key: "day",
					value: "日"
				},
				{
					key: "week",
					value: "周"
				},
				{
					key: "month",
					value: "月"
				},
				{
					key: "year",
					value: "年"
				},
			],
			listData: [],
			tabLabel: '当日',
			tabId: 0
		}
	},
	methods: {
		tabChange(tabId){
			this.tabId = tabId;
			this.tabLabel = '当' + this.tabs[tabId].value;
		},
		bindViewTap () {
			const url = '../logs/main'
			wx.navigateTo({ url })
		},
		getUserInfo () {
			// 调用登录接口
			wx.login({
				success: () => {
					wx.getUserInfo({
						success: (res) => {
							this.userInfo = res.userInfo
						}
					})
				}
			})
		},
		clickHandle (msg, ev) {
			console.log('clickHandle:', msg, ev)
		},
		clearStorage(){ 
			this.listData = [];
			wx.clearStorage() 
		},
		getFilterList(reg){
			let activeList = []
			this.listData.forEach( value =>{
				if (value.date.match(reg)) {
					activeList.push(value);
				}
			})
			return activeList;
		}
	},

	created () {
		// 调用应用实例的方法获取全局数据
		this.getUserInfo();
	},
	onUnload(){
		console.log('onUnload');
	},
	onShow(){
		console.log('onShow');
		this.listData = wx.getStorageSync('billList');
	},
	computed:{
		activeList(){
			let date = new Date()
			switch (+this.tabId) {
				case 0:
					return this.getFilterList(/2018-04-21/);
				case 1:
					return this.getFilterList(/2018-04-21/);
				case 2:
					return this.getFilterList(/2018-04/);
				case 3:
					return this.getFilterList(/2018/);
			}
		}
	}


}
</script>

<style lang="less">
.container{
	padding: 0;
	height: 100vh;
	position: relative;
	justify-content: flex-start;
	footer{
		display:flex;
		width:100%;
		position: absolute;
		bottom: 0;
		>button{
			// position: absolute;
			width: 50%;
			background-color: #fff;
		}
		a{
			height:100rpx;
			width:100rpx;
			line-height: 100rpx;
			text-align: center;
			display:block;
			position: absolute;
			border-radius: 100rpx;
			border: 1rpx solid #ccc;
			left: 50%;
			transform: translate(-50%,0);
			bottom: 40rpx;
			z-index: 2;
			background-color: #fff;
		}
	}
}
.userinfo {
	display: flex;
	flex-direction: column;
	align-items: center;
}

.userinfo-avatar {
	width: 128rpx;
	height: 128rpx;
	margin: 20rpx;
	border-radius: 50%;
}

.userinfo-nickname {
	color: #aaa;
}

.usermotto {
	margin-top: 150px;
}

.form-control {
	display: block;
	padding: 0 12px;
	margin-bottom: 5px;
	border: 1px solid #ccc;
}

.counter {
	display: inline-block;
	margin: 10px auto;
	padding: 5px 10px;
	color: blue;
	border: 1px solid blue;
}
</style>
