<template>
  <view class="rich-wrap">
    <view class="content_box title"
      ><u-parse :html="richText.content_1"></u-parse>
    </view>
    <view class="content_box">
      <u-parse :html="richText.content_2"></u-parse>
    </view>
    <view class="content_box">
      <u-parse :html="richText.content_3"></u-parse>
    </view>
    <view class="content_box">
      <u-parse :html="richText.content_4"></u-parse>
    </view>
     <view class="content_box">
      <u-parse :html="richText.content_5"></u-parse>
    </view>
     <view class="content_box">
      <u-parse :html="richText.content_6"></u-parse>
    </view>
    <view class="content_box">
      <u-parse :html="richText.content_7"></u-parse>
    </view>
    <view class="content_box">
      <u-parse :html="richText.content_8"></u-parse>
    </view>
     <view class="content_box">
      <u-parse :html="richText.content_9"></u-parse>
    </view>
    <view class="content_box">
      <u-parse :html="richText.content_10"></u-parse>
    </view>
    <view class="content_box">
      <button>下一步</button>
    </view>
  </view>
  
</template>

<script>
export default {
  data() {
    return {
      richText: {
           content_1: `注销账号需满足以下条件：`,
           content_2: `1、账号内的所有交易均已完结`,
           content_3: `用户账户中的所有订单交易均已完成交易或售后,无任何未完结或者有纠纷的订单需要处理`,
           content_4: `2、账号无任何纠纷`,   
           content_5: `账户未处于任何纠纷,包括但不限于投诉举报、被投诉举`,
           content_7: `3、账号处于正常状态,且无违规行为`,
           content_8: `账户为正常使用的账号且无任何尚未完成处理的违规行为`,   
           content_9: `4、账号资产已结清`,            
           content_10: `没有未结清的收益、欠款或未结清的个人资产 `,               
      },
    };
  },
};
</script>
<style lang="scss" scoped>
.rich-wrap{
    height:100%
}
.content_box {
  background: #fff;
  padding: 30rpx;
}
.title {
    color: rgb(136, 134, 134);
    font-size:14px
}
</style>