<template>
	<div class="page tab-container">
		<div class="page__bd">
			<div class="weui-tab">
				<div class="weui-navbar">
					<block v-for="(item,index) in tabs" :key="index">
						<div :id="index" :class="{'weui-bar__item_on':activeIndex == index}" class="weui-navbar__item" @click="tabClick">
							<div class="weui-navbar__title">{{item.value}}</div>
						</div>
					</block>
					<div class="weui-navbar__slider" :class="navbarSliderClass"></div>
				</div>
				<!-- <div class="weui-tab__panel">
					<div class="weui-tab__content" :hidden="activeIndex != 0">选项一的内容</div>
					<div class="weui-tab__content" :hidden="activeIndex != 1">选项二的内容</div>
					<div class="weui-tab__content" :hidden="activeIndex != 2">选项三的内容</div>
				</div> -->
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: [
		"tabs",
		"activeIndex",
	],
	data() {
		return {
			// tabs: ["选项一", "选项二", "选项三"],
			// activeIndex: 0,
			fontSize: 20
		}
	},
	computed: {
		navbarSliderClass() {
			return `weui-navbar__slider_${this.activeIndex}`
		}
	},
	methods: {
		tabClick(e) {
			this.activeIndex = e.currentTarget.id;
			this.$emit('tabChange',this.activeIndex);
		}
	}
}
</script>

<style scoped>
.tab-container{
	height: 97rpx;
	background-color: #fff;
}
/*page,
.page,
.page__bd {
	height: 100%;
}*/
.page__bd {
	padding-bottom: 0;
}
.weui-tab__content {
	padding-top: 60px;
	text-align: center;
}
.weui-navbar__slider_0 {
	left: 0rpx;
	transform: translateX(0);
}
.weui-navbar__slider_1 {
	left: 0rpx;
	transform: translateX(100%);
}
.weui-navbar__slider_2 {
	left: 0rpx;
	transform: translateX(200%);
}
.weui-navbar__slider_3 {
	left: 0rpx;
	transform: translateX(300%);
}
</style>
