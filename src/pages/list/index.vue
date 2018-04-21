<template>
	<div class="page">
		<div class="weui-cells weui-cells_after-title"
			v-for="item in listData">
	        <div class="weui-cell">
				<div class="weui-cell__bd">{{item.title}}</div>
				<div class="weui-cell__ft">{{item.tip}}</div>
	        </div>
      	</div>
	</div>
</template>

<script>
// Use Vuex
import base64 from '../../../static/images/base64';
export default {
	data() {
		return {
			icon: ''
		}
	},
	props:{
		"listData":{
			type: Array,
            default: null
		}
	},
	mounted() {
		this.icon = base64.icon20;
	}
}

</script>
<style>

</style>
