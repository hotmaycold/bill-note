<template>
    <div class="page list">
        <div class="weui-cells weui-cells_after-title">
            <div class="weui-cell">
                <div class="weui-cell__bd">{{label}}</div>
                <div class="weui-cell__ft">￥{{total}}</div>
            </div>
            <div class="weui-cell"
                v-for="item in listData">
                <div class="weui-cell__bd">{{item.date}}</div>
                <div class="weui-cell__bd">{{item.type}}</div>
                <div class="weui-cell__ft">￥{{item.cost}}</div>
            </div>
        </div>
    </div>
</template>

<script>
// Use Vuex
import base64 from '../../static/images/base64';
export default {
    data() {
        return {
            icon: '',
        }
    },
    props:["listData","label"],
    mounted() {
        this.icon = base64.icon20;
    },
    computed:{
        total(){
            let amount = 0
            this.listData.forEach((value)=>{
                amount += +value.cost;
            })
            return amount;
        }
    }
}

</script>
<style lang="less">
.page{
    width: 100%;
}
.list{
    .weui-cell__bd{
        width: 100rpx;
    }
}
</style>
