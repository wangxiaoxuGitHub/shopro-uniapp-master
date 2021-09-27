<template>
    <view class="adv-box u-m-y-10 u-m-x-20" v-for="item in advList">
        <view class="img-box">
            <image style="width:710rpx;height:220rpx;border-radius: 20rpx" @tap="jump(item.image)" :src="item.image" mode="aspectFill"></image>
        </view>
        <view class="info">{{item.title}}</view>
    </view>
</template>

<script>
    /**
     * 自定义之广告魔方
     * @property {Object} detail -广告魔方信息
     */
    export default {
        components: {},
        data() {
            return {
                advList:this.goodList2
            };
        },
        props: {
            goodList2: {}
        },
        computed: {},
        created() {},
        methods: {
            // 路由跳转
            jump(path) {
                this.$tools.routerTo(path);
            }
        }
    };
</script>

<style lang="scss">
    @mixin grid($row: 1) {
        width: (710 - ($row - 1) * 10) / $row + rpx;
        border-radius: 10rpx;
    }
    .adv-box {
        .img-box{
            border: 1px  solid #ccc;
            border-radius: 8px 8px 0 0;
            box-sizing: border-box;
            padding: 8px 8px 5px 8px;
            image{
                /*margin: 8px;*/
                width: 90%;
            }
        }
        .info{
            font-size: 28rpx;
            border: 1px  solid #ccc;
            border-top: none;
            border-radius: 0 0 8px 8px;
            padding: 8px;
        }
    }
</style>
