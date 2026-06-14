<template>
  <view class="page">
    <!-- 主体内容 -->
    <scroll-view class="content"
                 scroll-y
                 :style="{ height: scrollHeight + 'px' }">
      <!-- 堂食/外卖切换 -->
      <view class="mode-switch">
        <view class="mode-bg">
          <view class="mode-btn active">
            <text>堂食 (Eat-in)</text>
          </view>
          <view class="mode-btn">
            <text>外卖 (Takeout)</text>
          </view>
        </view>
      </view>

      <!-- Banner轮播 -->
      <view class="banner">
        <swiper class="banner-swiper"
                indicator-dots
                autoplay
                circular>
          <swiper-item>
            <view class="banner-item">
              <image class="banner-img"
                     src="/static/images/17.png"
                     mode="aspectFill" />
              <view class="banner-mask">
                <view class="banner-tag">今日推荐</view>
                <text class="banner-title">至尊全羊盛宴 8.5折</text>
                <text class="banner-sub">限时深夜食堂专属优惠</text>
              </view>
            </view>
          </swiper-item>
        </swiper>
        <view class="banner-dots">
          <image class="dot"
                 src="/static/images/8.svg"
                 mode="aspectFit" />
          <image class="dot"
                 src="/static/images/9.svg"
                 mode="aspectFit" />
          <image class="dot"
                 src="/static/images/10.svg"
                 mode="aspectFit" />
        </view>
      </view>

      <!-- 必点招牌 -->
      <view class="section">
        <view class="section-header">
          <view class="section-title-wrap">
            <text class="section-title">必点招牌</text>
            <text class="section-en">Must-try</text>
          </view>
          <view class="section-more">
            <text>全部</text>
            <image class="more-icon"
                   src="/static/images/11.svg"
                   mode="aspectFit" />
          </view>
        </view>
        <view class="must-try-list">
          <!-- 大卡片 -->
          <view class="big-card">
            <image class="big-card-img"
                   src="/static/images/20.png"
                   mode="aspectFill" />
            <view class="big-card-info">
              <view class="hot-tag">
                <image class="fire-icon"
                       src="/static/images/15.svg"
                       mode="aspectFit" />
                <text>超人气</text>
              </view>
              <text class="big-card-name">秘制碳烤猪五花</text>
              <text class="big-card-desc">肥而不腻，唇齿留香</text>
              <view class="big-card-bottom">
                <text class="price">¥48</text>
                <view class="add-btn">
                  <image class="add-icon"
                         src="/static/images/16.svg"
                         mode="aspectFit" />
                </view>
              </view>
            </view>
          </view>
          <!-- 小卡片 -->
          <view class="small-cards">
            <view class="small-card">
              <image class="small-card-img"
                     src="/static/images/18.png"
                     mode="aspectFill" />
              <text class="small-card-name">呼伦贝尔羊肉串</text>
              <view class="tag spicy">
                <image class="tag-icon"
                       src="/static/images/12.svg"
                       mode="aspectFit" />
                <text>微辣</text>
              </view>
              <view class="small-card-bottom">
                <view class="price-wrap">
                  <text class="price">¥12</text>
                  <text class="unit">/串</text>
                </view>
                <view class="add-btn-gray">
                  <image class="add-icon"
                         src="/static/images/13.svg"
                         mode="aspectFit" />
                </view>
              </view>
            </view>
            <view class="small-card">
              <image class="small-card-img"
                     src="/static/images/19.png"
                     mode="aspectFill" />
              <text class="small-card-name">碳烤杏鲍菇</text>
              <view class="tag veggie">
                <text>素食精选</text>
              </view>
              <view class="small-card-bottom">
                <view class="price-wrap">
                  <text class="price">¥18</text>
                  <text class="unit">/份</text>
                </view>
                <view class="add-btn-gray">
                  <image class="add-icon"
                         src="/static/images/14.svg"
                         mode="aspectFit" />
                </view>
              </view>
            </view>
          </view>
        </view>
      </view>

      <!-- 酒水专区 -->
      <view class="section">
        <view class="section-header">
          <view class="section-title-wrap">
            <text class="section-title">酒水专区</text>
            <text class="section-en drinks">Drinks</text>
          </view>
        </view>
        <scroll-view class="drinks-scroll"
                     scroll-x>
          <view class="drinks-list">
            <view class="drink-card"
                  v-for="(item, index) in drinks"
                  :key="index">
              <view class="drink-img-wrap">
                <image class="drink-img"
                       :src="item.img"
                       mode="aspectFill" />
              </view>
              <text class="drink-name">{{ item.name }}</text>
              <text class="drink-price">¥{{ item.price }}</text>
            </view>
          </view>
        </scroll-view>
      </view>

      <!-- 底部占位 -->
      <view class="bottom-placeholder" />
    </scroll-view>

    <!-- 结算浮窗 -->
    <view class="checkout-bar">
      <view class="checkout-content">
        <view class="cart-info">
          <view class="cart-icon-wrap">
            <image class="cart-icon"
                   src="/static/images/4.svg"
                   mode="aspectFit" />
            <view class="cart-badge">
              <text>3</text>
            </view>
          </view>
          <view class="cart-price">
            <text class="total">¥78.00</text>
            <text class="delivery">另需配送费 ¥3 (外卖)</text>
          </view>
        </view>
        <view class="checkout-btn"
              @click="goToCheckout">
          <text>去结算</text>
        </view>
      </view>
    </view>

  </view>
</template>

<script setup lang="ts">
  import { ref, onMounted } from "vue";

  const scrollHeight = ref(600);

  const drinks = ref([
    { name: "青岛一厂原浆", price: 22, img: "/static/images/21.png" },
    { name: "海盐柠檬苏打", price: 15, img: "/static/images/22.png" },
    { name: "黑啤精酿", price: 28, img: "/static/images/23.png" },
    { name: "现榨西瓜汁", price: 18, img: "/static/images/24.png" },
  ]);

  const goToMenu = () => {
    uni.switchTab({
      url: "/pages/menu/index",
    });
  };

  const goToCheckout = () => {
    uni.navigateTo({
      url: "/pages/checkout/index",
    });
  };

  const goToProfile = () => {
    uni.switchTab({
      url: "/pages/profile/index",
    });
  };

  onMounted(() => {
    const sysInfo = uni.getSystemInfoSync();
    // 减去checkout(69) + safeArea
    const safeBottom = sysInfo.safeAreaInsets?.bottom || 0;
    scrollHeight.value = sysInfo.windowHeight - 69 - safeBottom;
  });
</script>

<style scoped>
  .page {
    width: 100vw;
    height: 100vh;
    background: #f8f9fa;
    display: flex;
    flex-direction: column;
    position: relative;
  }

  /* Content */
  .content {
    flex: 1;
    padding: 0 16px;
  }

  /* Mode Switch */
  .mode-switch {
    padding: 8px 0;
    display: flex;
    justify-content: center;
  }

  .mode-bg {
    width: 320px;
    height: 44px;
    background: #f3f4f5;
    box-shadow: inset 0px 2px 4px rgba(0, 0, 0, 0.05);
    border-radius: 9999px;
    display: flex;
    align-items: center;
    padding: 4px;
  }

  .mode-btn {
    flex: 1;
    height: 36px;
    border-radius: 9999px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .mode-btn text {
    font-size: 12px;
    font-family: "Be Vietnam Pro", sans-serif;
    font-weight: 700;
    letter-spacing: 0.6px;
    color: #58423c;
  }

  .mode-btn.active {
    background: #c54f2c;
    box-shadow: 0px 2px 4px -2px rgba(0, 0, 0, 0.1),
      0px 4px 6px -1px rgba(0, 0, 0, 0.1);
  }

  .mode-btn.active text {
    color: #fffbff;
  }

  /* Banner */
  .banner {
    margin-top: 8px;
    position: relative;
  }

  .banner-swiper {
    height: 156.63px;
    border-radius: 12px;
    overflow: hidden;
  }

  .banner-item {
    position: relative;
    width: 100%;
    height: 100%;
  }

  .banner-img {
    width: 100%;
    height: 100%;
  }

  .banner-mask {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(
      0deg,
      rgba(0, 0, 0, 0.6) 0%,
      rgba(0, 0, 0, 0) 100%
    );
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 16px;
  }

  .banner-tag {
    width: 56px;
    height: 19px;
    background: #c54f2c;
    border-radius: 2px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 4px;
  }

  .banner-tag text {
    font-size: 10px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 700;
    color: #fffbff;
  }

  .banner-title {
    font-size: 24px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 600;
    color: white;
  }

  .banner-sub {
    font-size: 12px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 400;
    color: rgba(255, 255, 255, 0.8);
    margin-top: 4px;
  }

  .banner-dots {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 6px;
    margin-top: 8px;
  }

  .dot {
    width: 6px;
    height: 4px;
  }

  /* Section */
  .section {
    margin-top: 24px;
  }

  .section-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 12px;
  }

  .section-title-wrap {
    display: flex;
    align-items: baseline;
    gap: 4px;
  }

  .section-title {
    font-size: 20px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 600;
    color: #191c1d;
  }

  .section-en {
    font-size: 14px;
    font-family: "Plus Jakarta Sans", sans-serif;
    font-weight: 600;
    color: #c54f2c;
  }

  .section-en.drinks {
    color: #8a4b2e;
  }

  .section-more {
    display: flex;
    align-items: center;
    gap: 4px;
  }

  .section-more text {
    font-size: 12px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 400;
    color: #a43716;
  }

  .more-icon {
    width: 12px;
    height: 12px;
  }

  /* Must Try */
  .must-try-list {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .big-card {
    display: flex;
    background: #f3f4f5;
    border-radius: 12px;
    overflow: hidden;
    outline: 1px solid rgba(223, 192, 183, 0.3);
    outline-offset: -1px;
  }

  .big-card-img {
    width: 178px;
    height: 160px;
  }

  .big-card-info {
    flex: 1;
    padding: 16px;
    display: flex;
    flex-direction: column;
  }

  .hot-tag {
    display: flex;
    align-items: center;
    gap: 4px;
    margin-bottom: 4px;
  }

  .hot-tag text {
    font-size: 10px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 700;
    color: #ba1a1a;
  }

  .fire-icon {
    width: 10px;
    height: 10px;
  }

  .big-card-name {
    font-size: 20px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 600;
    color: #191c1d;
  }

  .big-card-desc {
    font-size: 12px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 400;
    color: #58423c;
    margin-top: 4px;
  }

  .big-card-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: auto;
  }

  .price {
    font-size: 20px;
    font-family: "Be Vietnam Pro", sans-serif;
    font-weight: 700;
    color: #a43716;
  }

  .add-btn {
    width: 26px;
    height: 26px;
    background: #c54f2c;
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .add-icon {
    width: 14px;
    height: 14px;
  }

  .small-cards {
    display: flex;
    gap: 16px;
  }

  .small-card {
    flex: 1;
    background: #f3f4f5;
    border-radius: 12px;
    padding: 13px;
    outline: 1px solid rgba(223, 192, 183, 0.3);
    outline-offset: -1px;
  }

  .small-card-img {
    width: 100%;
    height: 128px;
    border-radius: 8px;
  }

  .small-card-name {
    font-size: 16px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 400;
    color: #191c1d;
    margin-top: 8px;
    display: block;
  }

  .tag {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    padding: 2px 6px;
    border-radius: 4px;
    margin-top: 8px;
  }

  .tag.spicy {
    background: #ffdad6;
  }

  .tag.spicy text {
    font-size: 10px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 400;
    color: #93000a;
  }

  .tag.veggie {
    background: #d9e2fa;
  }

  .tag.veggie text {
    font-size: 10px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 400;
    color: #5b6478;
  }

  .tag-icon {
    width: 8px;
    height: 8px;
  }

  .small-card-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 8px;
  }

  .price-wrap {
    display: flex;
    align-items: baseline;
    gap: 2px;
  }

  .unit {
    font-size: 10px;
    font-family: "Be Vietnam Pro", sans-serif;
    font-weight: 700;
    color: #58423c;
  }

  .add-btn-gray {
    width: 19.67px;
    height: 19.67px;
    background: #e1e3e4;
    border-radius: 6px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  /* Drinks */
  .drinks-scroll {
    width: 100%;
  }

  .drinks-list {
    display: flex;
    gap: 12px;
    padding: 8px 0;
  }

  .drink-card {
    width: 128px;
    background: #f3f4f5;
    border-radius: 12px;
    padding: 9px;
    outline: 1px solid rgba(223, 192, 183, 0.3);
    outline-offset: -1px;
    flex-shrink: 0;
  }

  .drink-img-wrap {
    width: 110px;
    height: 128px;
    background: #e1e3e4;
    border-radius: 8px;
    overflow: hidden;
  }

  .drink-img {
    width: 110px;
    height: 128px;
  }

  .drink-name {
    font-size: 12px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 700;
    letter-spacing: 0.6px;
    color: #191c1d;
    margin-top: 8px;
    display: block;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .drink-price {
    font-size: 16px;
    font-family: "Be Vietnam Pro", sans-serif;
    font-weight: 700;
    color: #a43716;
    margin-top: 4px;
    display: block;
  }

  .bottom-placeholder {
    height: 20px;
  }

  /* Checkout Bar */
  .checkout-bar {
    position: fixed;
    left: 16px;
    right: 16px;
    bottom: 66px;
    z-index: 100;
  }

  .checkout-content {
    height: 69px;
    background: rgba(255, 255, 255, 0.85);
    border-radius: 16px;
    outline: 1px solid rgba(164, 55, 22, 0.2);
    outline-offset: -1px;
    backdrop-filter: blur(6px);
    box-shadow: 0px 25px 50px -12px rgba(0, 0, 0, 0.25);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 13px;
  }

  .cart-info {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .cart-icon-wrap {
    position: relative;
    width: 42px;
    height: 39px;
  }

  .cart-icon {
    width: 42px;
    height: 39px;
  }

  .cart-badge {
    position: absolute;
    right: -4px;
    top: -4px;
    width: 21px;
    height: 21px;
    background: white;
    border-radius: 50%;
    outline: 1px solid #a43716;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .cart-badge text {
    font-size: 10px;
    font-family: "Be Vietnam Pro", sans-serif;
    font-weight: 800;
    color: #a43716;
  }

  .cart-price {
    display: flex;
    flex-direction: column;
  }

  .total {
    font-size: 20px;
    font-family: "Be Vietnam Pro", sans-serif;
    font-weight: 700;
    color: #191c1d;
  }

  .delivery {
    font-size: 10px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 400;
    color: #58423c;
  }

  .checkout-btn {
    width: 102px;
    height: 40px;
    background: #c54f2c;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .checkout-btn text {
    font-size: 12px;
    font-family: "WenQuanYi Zen Hei", sans-serif;
    font-weight: 700;
    letter-spacing: 0.6px;
    color: #fffbff;
  }
</style>
