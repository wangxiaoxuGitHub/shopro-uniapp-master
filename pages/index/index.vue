<!-- 首页 -->
<template>
	<view class="home-wrap u-m-b-20">
		<!-- 空白页 -->
		<!-- #ifdef APP-PLUS -->
<!--		<u-no-network @retry="init"></u-no-network>-->
		<!-- #endif -->
<!--		<shopro-empty v-if="!hasTemplate" :image="$IMG_URL + '/imgs/empty/template_empty.png'" tipText="暂未找到模板，请前往装修~"></shopro-empty>-->

		<view class="content-box">
			<!-- 导航栏 -->
<!--			<home-head v-if="headSwiperList && headSwiperList.length" :isScorll="isScorll" borderRadius="0" :navTitle="initShop.name" :list="headSwiperList"></home-head>-->
			<!-- 自定义模块 -->
            <!-- 搜索框 -->
            <my-search></my-search>
            <!-- tab -->
            <view class="head_box">
                <view class="order-nav u-flex">
                    <view class="nav-item u-flex-col u-flex-1 u-row-center u-col-center" v-for="nav in groupState" :key="nav.id" @tap="onNav(nav.id)">
                        <view class="item-title">{{ nav.title }}</view>
                        <text class="nav-line" :class="{ 'line-active': stateId === nav.id }"></text>
                    </view>
                </view>
            </view>
            <view class="content_box">
                <scroll-view scroll-y="true" enable-back-to-top @scrolltolower="loadMore" refresher-background="#f5f5f5" class="scroll-box">
                    <view class="template-box">
                        <!-- 轮播 -->
                        <sh-banner
                                :Px="0"
                                :Py="0"
                                :borderRadius="0"
                                :height="330"
                                :list="bannerList"
                        ></sh-banner>
                        <view class="cell">
                            <view>正品保障</view>
                            <view>7天无理由退换</view>
                            <view>会员优惠</view>
                        </view>
<!--                        <good-list1></good-list1>-->
                        <u-divider color="#101010" border-color="#aaa">健康精选</u-divider>
                        <good-list2 :goodList2="goodList2"></good-list2>
                        <block v-for="(item, index) in homeTemplate" :key="item.id">
                            <!-- 轮播 -->
                            <sh-banner
                                    v-if="item.type === 'banner' && index !== 0"
                                    :Px="item.content.x"
                                    :Py="item.content.y"
                                    :borderRadius="item.content.radius"
                                    :height="item.content.height"
                                    :list="item.content.list"
                            ></sh-banner>

                            <!-- 搜索 -->
                            <sh-search v-if="item.type === 'search'"></sh-search>

                            <!-- 滑动宫格 -->
                            <sh-grid-swiper v-if="item.type === 'menu'" :list="item.content.list" :oneRowNum="item.content.style"></sh-grid-swiper>

                            <!-- 推荐商品 -->
                            <sh-hot-goods v-if="item.type === 'goods-list' || item.type === 'goods-group'" :detail="item.content"></sh-hot-goods>
                            <!-- 广告魔方 -->
                            <sh-adv v-if="item.type === 'adv'" :detail="item.content"></sh-adv>
                            <!-- 优惠券 -->
                            <sh-coupon v-if="item.type === 'coupons'" :detail="item.content"></sh-coupon>
                            <!-- 秒杀-->
                            <sh-seckill v-if="item.type === 'seckill'" :detail="item.content"></sh-seckill>
                            <!-- 拼团 -->
                            <sh-groupon v-if="item.type === 'groupon'" :detail="item.content"></sh-groupon>
                            <!-- 富文本 -->
                            <sh-richtext v-if="item.type === 'rich-text'" :richId="item.content.id"></sh-richtext>
                            <!-- 功能标题 -->
                            <sh-title-card v-if="item.type === 'title-block'" :title="item.content.name" :bgImage="item.content.image" :titleColor="item.content.color"></sh-title-card>
                            <!-- 直播 -->
                            <!-- #ifdef MP-WEIXIN -->
                            <sh-live v-if="item.type === 'live' && HAS_LIVE" :detail="item.content"></sh-live>
                            <!-- #endif -->
                        </block>
                    </view>

                    <!-- 空白页 -->
                    <shopro-empty
                            v-if="isEmpty"
                            :image="$IMG_URL + '/imgs/empty/empty_groupon.png'"
                            tipText="暂无拼团商品，更多拼团好货等着你噢~"
                            btnText="去首页逛逛"
                            @click="$Router.pushTab('/pages/index/index')"
                    ></shopro-empty>

                    <!-- 加载更多 -->
                    <u-loadmore v-if="myGrouponList.length" height="80rpx" :status="loadStatus" icon-type="flower" color="#ccc" />
                </scroll-view>
            </view>
			<view class="template-box">
				<block v-for="(item, index) in homeTemplate" :key="item.id">
					<!-- 轮播 -->
					<sh-banner
						v-if="item.type === 'banner' && index !== 0"
						:Px="item.content.x"
						:Py="item.content.y"
						:borderRadius="item.content.radius"
						:height="item.content.height"
						:list="item.content.list"
					></sh-banner>

					<!-- 搜索 -->
					<sh-search v-if="item.type === 'search'"></sh-search>

					<!-- 滑动宫格 -->
					<sh-grid-swiper v-if="item.type === 'menu'" :list="item.content.list" :oneRowNum="item.content.style"></sh-grid-swiper>

					<!-- 推荐商品 -->
					<sh-hot-goods v-if="item.type === 'goods-list' || item.type === 'goods-group'" :detail="item.content"></sh-hot-goods>
					<!-- 广告魔方 -->
					<sh-adv v-if="item.type === 'adv'" :detail="item.content"></sh-adv>
					<!-- 优惠券 -->
					<sh-coupon v-if="item.type === 'coupons'" :detail="item.content"></sh-coupon>
					<!-- 秒杀-->
					<sh-seckill v-if="item.type === 'seckill'" :detail="item.content"></sh-seckill>
					<!-- 拼团 -->
					<sh-groupon v-if="item.type === 'groupon'" :detail="item.content"></sh-groupon>
					<!-- 富文本 -->
					<sh-richtext v-if="item.type === 'rich-text'" :richId="item.content.id"></sh-richtext>
					<!-- 功能标题 -->
					<sh-title-card v-if="item.type === 'title-block'" :title="item.content.name" :bgImage="item.content.image" :titleColor="item.content.color"></sh-title-card>
					<!-- 直播 -->
					<!-- #ifdef MP-WEIXIN -->
					<sh-live v-if="item.type === 'live' && HAS_LIVE" :detail="item.content"></sh-live>
					<!-- #endif -->
				</block>
			</view>

			<!-- 分类选项卡 -->
			<sh-category-tabs
				v-if="categoryTabsData && categoryTabsData.category_arr && categoryTabsData.category_arr.length"
				:enable="enable"
				:styleType="categoryTabsData.style"
				:tabsList="categoryTabsData.category_arr"
			></sh-category-tabs>
			<!-- 登录提示 -->
			<shopro-auth-modal></shopro-auth-modal>
			<!-- 悬浮按钮 -->
			<shopro-float-btn></shopro-float-btn>
			<!-- 连续弹窗提醒 -->
<!--			<shopro-notice-modal v-if="!showPrivacy && isLogin"></shopro-notice-modal>-->
			<!-- 隐私协议 -->
			<!-- #ifdef APP-PLUS -->
			<privacy-modal v-if="initShop && initShop.name" v-model="showPrivacy"></privacy-modal>
			<!-- #endif -->
			<!-- #ifdef H5 -->
			<view class="tabbar-hack" style="height: 120rpx; width:100%;"></view>
			<!-- #endif -->
		</view>
		<!-- <shopro-tabbar></shopro-tabbar> -->
	</view>
</template>

<script>
    import mySearch from './components/my-search.vue';
    import goodList1 from './components/good-list1';
    import goodList2 from './components/good-list2';
import shBanner from './components/sh-banner.vue';
import shGridSwiper from './components/sh-grid-swiper.vue';
import shHotGoods from './components/sh-hot-goods.vue';
import shAdv from './components/sh-adv.vue';
import shCoupon from './components/sh-coupon.vue';
import shSeckill from './components/sh-seckill.vue';
import shGroupon from './components/sh-groupon.vue';
import shRichtext from './components/sh-richtext.vue';
import shTitleCard from './components/sh-title-card.vue';
import shSearch from './components/sh-search.vue';
import shCategoryTabs from './components/sh-category-tabs.vue';

import privacyModal from './index/privacy-modal.vue';
import homeHead from './index/home-head.vue';

// #ifdef MP-WEIXIN
import { HAS_LIVE } from '@/env';
import shLive from './components/sh-live.vue';
// #endif

import { mapMutations, mapActions, mapState, mapGetters } from 'vuex';
export default {
	components: {
        mySearch,
        goodList1,
        goodList2,
		shBanner,
		shGridSwiper,
		shGroupon,
		shHotGoods,
		shAdv,
		shCoupon,
		shSeckill,
		shRichtext,
		shTitleCard,
		shSearch,
		shCategoryTabs,

		privacyModal,
		homeHead,

		// #ifdef MP-WEIXIN
		shLive
		// #endif
	},
	data() {
		return {
			// #ifdef MP-WEIXIN
			HAS_LIVE: HAS_LIVE,
			// #endif
            // tab   data
            groupState: [
                {
                    id: 'all', //0
                    title: '全部'
                },
                {
                    id: 'ing', //1
                    title: '进行中'
                },
                {
                    id: 'finish', //2
                    title: '成功'
                },
                {
                    id: 'invalid', //3
                    title: '失败'
                }
            ],
            isEmpty: false,
            loadStatus: 'loadmore', //loadmore:加载前的状态，loading:加载中的状态，nomore-没有更多的状态
            lastPage: 1,
            currentPage: 1,
            stateId: 'all',
            myGrouponList: [], //我的拼团列表。

            // 轮播
            bannerList:[
                {bgcolor: "#aaeeb2",
                image: "http://file.shopro.top/uploads/20210518/919a402e8aabfa0a2100a4215b586286.jpg",
                name: "",
                path: "",
                path_name: "",
                path_type: 1},
                {bgcolor: "#aaeeb2",
                    image: "http://file.shopro.top/uploads/20210518/919a402e8aabfa0a2100a4215b586286.jpg",
                    name: "",
                    path: "",
                    path_name: "",
                    path_type: 1},
                {bgcolor: "#aaeeb2",
                    image: "http://file.shopro.top/uploads/20210518/919a402e8aabfa0a2100a4215b586286.jpg",
                    name: "",
                    path: "",
                    path_name: "",
                    path_type: 1},
            ],

            // 商品2数据
            goodList2:[
                {
                    image: "https://demo.shopro.top/uploads/20210915/860ac615dc5fa2f41fa1f76352cefa07.png",
                    title: "让我们的世界充满阳光，护眼，你必须知道的几件事。",
                    name: "让我们的世界充满阳光，护眼，你必须知道的几件事。",
                },
                {
                    image: "https://demo.shopro.top/uploads/20210915/860ac615dc5fa2f41fa1f76352cefa07.png",
                    title: "让我们的世界充满阳光，护眼，你必须知道的几件事。",
                    name: "让我们的世界充满阳光，护眼，你必须知道的几件事。",
                },
                {
                    image: "https://demo.shopro.top/uploads/20210915/860ac615dc5fa2f41fa1f76352cefa07.png",
                    title: "让我们的世界充满阳光，护眼，你必须知道的几件事。",
                    name: "让我们的世界充满阳光，护眼，你必须知道的几件事。",
                }
            ],


			isRefresh: true,

			enable: false, //是否开启吸顶。
			isConnected: true, //是否有网
			showPrivacy: false, //协议
			isScorll: false
		};
	},
	computed: {
		...mapGetters(['initShop', 'homeTemplate', 'hasTemplate', 'isLogin']),
		// 头部模块数据
		headSwiperList() {
		    console.log("homeTemplate",this.homeTemplate)
			if (this.homeTemplate?.length) {
				return this.homeTemplate[0]?.content?.list;
			}
		},
		// 分类选项卡数据
		categoryTabsData() {
			if (this.homeTemplate?.length) {
				return this.homeTemplate[this.homeTemplate.length - 1]?.content;
			}
		}
	},
    mounted(){
	  console.log("homeTemplate",this.homeTemplate)
    },
	onPullDownRefresh() {
		this.init();
	},
	onPageScroll(e) {
		this.isScorll = e.scrollTop > 100 ? true : false;
	},
	onShow() {
		let that = this;
		this.enable = true;
		this.isLogin && this.getCartList();
		// 网络变化检测
		uni.onNetworkStatusChange(res => {
			this.isConnected = res.isConnected;
			res.isConnected && this.init();
		});
	},
	onHide() {
		this.enable = false;
	},
	onLoad() {
		// #ifdef APP-VUE
		// app隐私协议弹窗
		if (!plus.runtime.isAgreePrivacy()) {
			this.showPrivacy = true;
			this.showNoticeModal = false;
		}
		// #endif
	},
	methods: {
		...mapActions(['appInit', 'getTemplate', 'getCartList']),
		// 初始化
		init() {
			this.isRefresh = false;
			return Promise.all([this.getTemplate()]).then(() => {
				uni.stopPullDownRefresh();
				this.isRefresh = true;
			});
		},
        onNav(id) {
            if (this.stateId !== id) {
                this.stateId = id;
                this.myGrouponList = [];
                this.currentPage = 1;
                this.getMyGroupon();
            }
        },
        getMyGroupon() {
            let that = this;
            that.loadStatus = 'loading';
            that.$http(
                'goods.myGroupon',
                {
                    type: that.stateId,
                    page: that.currentPage
                },
                '加载中'
            ).then(res => {
                uni.stopPullDownRefresh();
                if (res.code === 1) {
                    that.myGrouponList = [...that.myGrouponList, ...res.data.data];
                    that.isEmpty = !that.myGrouponList.length;
                    that.lastPage = res.data.last_page;
                    that.loadStatus = that.currentPage < res.data.last_page ? 'loadmore' : 'nomore';
                }
            });
        }
	}
};
</script>

<style lang="scss">
    .order-nav {
        background: #fff;
        height: 80rpx;

        .nav-item {
            flex: 1;

            .item-title {
                font-size: 30rpx;

                font-weight: 400;
                color: rgba(51, 51, 51, 1);
                line-height: 76rpx;
            }

            .nav-line {
                width: 120rpx;
                height: 4rpx;
                background: #fff;
            }

            .line-active {
                background: rgba(230, 184, 115, 1);
            }
        }
    }
    .cell{
        display: flex;
        justify-content: space-around;
    }
</style>
