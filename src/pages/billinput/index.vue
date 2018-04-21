<template>
    <div>
        <!-- <select v-model="selectedType" placeholder="选择类型">
            <option v-for="(item, index) in costTypes" 
            :value="item.value"
            :key="index">{{item.text}}</option>
        </select> -->
        <div class="weui-cell weui-cell_input">
            <div class="weui-cell__hd">
                <div class="weui-label">日期</div>
            </div>
            <div class="weui-cell__bd">
                <picker mode="date" value="date"  @change="bindDateChange">
                    <div class="weui-input">{{date}}</div>
                </picker>
            </div>
        </div>
        <div class="weui-cell weui-cell_input">
            <div class="weui-cell__hd">
                <div class="weui-label">金额</div>
            </div>
            <div class="weui-cell__bd">
                <input class="weui-input" step="0.1" type="number" placeholder="请输入金额" 
                    v-model="money"/>
            </div>
        </div>
        <div class="weui-cell weui-cell_input">
            <div class="weui-cell__hd">
                <div class="weui-label">类别</div>
            </div>
            <div class="weui-cell__bd">
                <picker @change="bindTypeChange" :value="index" :range="costTypes">
                    <div class="weui-input">{{billType.text}}</div>
                </picker>
            </div>
        </div>
        <div class="weui-btn-area">
            <button class="weui-btn" type="primary" @click="saveBill">确定</button>
        </div>
    </div>
</template>
<script>
// import picker from '@/components/picker'
export default {
    // components:{
    //     picker
    // },
    data () {
        return {
            selected: "day",
            cost: null,
            selectedType: 'lunch',
            costTypes: [
                '早餐',
                '中餐',
                '晚餐',
                '交通',
                '线下购物',
                '网购',
                '旅游',
                '化妆品',
                '服饰',
                '其他',
            ],
            billType:{
                id: 0,
                text: '早餐',
            },
            date:'',
            money:null
        }
    },
    methods:{
        saveBill(){
            if (this.date && this.money){
                let data = {
                    date: this.date,
                    cost: this.money,
                    type: this.billType.text
                }
                let list = wx.getStorageSync('billList');
                if (list) {
                    list.push(data);
                }
                else {
                    list = [];
                    list.push(data);
                }
                wx.setStorage({key: 'billList',data: list});
                wx.navigateTo({
                    url: `/pages/index/main`
                })
            }

        },
        bindTypeChange(e) {
            this.billType.id = e.mp.detail.value;
            this.billType.text = this.costTypes[e.mp.detail.value];
        },
        bindDateChange(e) {
            this.date = e.mp.detail.value;
        },
    },
    onShow(){
        this.date = '',
        this.money = null
    }
}
</script>
<style lang="less">
    .mint-cell-title{
        text-align: left;
    }   
    .mint-field-core{
        text-align: right;
        padding-right: 20px;
    }
    .mint-cell-wrapper{
        border-width: 1px 0 1px 0;
        border-color: #cacaca;
        border-style: solid;
    }
</style>
