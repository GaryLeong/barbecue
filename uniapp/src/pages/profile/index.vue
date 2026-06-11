<template>
  <view class="page">
    <!-- 顶部导航栏 -->
    <view class="header">
      <view class="header-left">
        <image class="fire-icon" src="/static/profile/4.svg" mode="aspectFit" />
        <text class="brand">Beijing BBQ</text>
      </view>
      <view class="header-right">
        <image class="header-icon" src="/static/profile/5.svg" mode="aspectFit" />
        <image class="header-icon" src="/static/profile/6.svg" mode="aspectFit" />
      </view>
    </view>

    <!-- 主体内容 -->
    <scroll-view class="content" scroll-y>
      <!-- 用户信息 -->
      <view class="user-section">
        <view class="avatar-wrap">
          <image class="avatar" src="/static/profile/22.png" mode="aspectFill" />
          <view class="level-badge">
            <text>LV.4</text>
          </view>
        </view>
        <view class="user-info">
          <text class="user-name">撸串小王子</text>
          <view class="user-tag">
            <image class="crown-icon" src="/static/profile/7.svg" mode="aspectFit" />
            <text>尊享会员 · 终极吃货</text>
          </view>
        </view>
      </view>

      <!-- 数据卡片 -->
      <view class="stats-section">
        <!-- 累计撸串数 -->
        <view class="stat-card big">
          <text class="stat-label">累计撸串数</text>
          <view class="stat-value-wrap">
            <text class="stat-value">1,284</text>
            <text class="stat-unit">根</text>
          </view>
          <view class="progress-bar">
            <view class="progress-fill" />
          </view>
          <text class="stat-rank">击败了全国 98% 的串友</text>
        </view>

        <!-- 右侧两个小卡 -->
        <view class="stat-col">
          <view class="stat-card small" @click="goPoints">
            <view class="small-card-left">
              <text class="small-label">积分商城</text>
              <text class="small-value">4,520</text>
            </view>
            <image class="arrow-icon" src="/static/profile/8.svg" mode="aspectFit" />
          </view>
          <view class="stat-card small" @click="goFavorites">
            <view class="small-card-left">
              <text class="small-label">我的收藏</text>
              <image class="heart-icon" src="/static/profile/9.svg" mode="aspectFit" />
            </view>
            <image class="arrow-icon" src="/static/profile/10.svg" mode="aspectFit" />
          </view>
        </view>
      </view>

      <!-- 优惠券 -->
      <view class="coupon-section">
        <view class="section-header">
          <text class="section-title">我的优惠券</text>
          <view class="section-more" @click="goCoupons">
            <text>查看全部</text>
            <image class="more-arrow" src="/static/profile/11.svg" mode="aspectFit" />
          </view>
        </view>
        <scroll-view class="coupon-scroll" scroll-x>
          <view class="coupon-list">
            <view class="coupon-card orange">
              <view class="coupon-top">
                <image class="coupon-icon" src="/static/profile/12.svg" mode="aspectFit" />
                <view class="coupon-tag">
                  <text>酒水专享</text>
                </view>
              </view>
              <view class="coupon-bottom">
                <text class="coupon-price">¥20</text>
                <text class="coupon-desc">精酿啤酒抵扣券</text>
              </view>
              <image class="coupon-deco" src="/static/profile/13.svg" mode="aspectFit" />
            </view>
            <view class="coupon-card red">
              <view class="coupon-top">
                <image class="coupon-icon" src="/static/profile/14.svg" mode="aspectFit" />
                <view class="coupon-tag red-tag">
                  <text>通用券</text>
                </view>
              </view>
              <view class="coupon-bottom">
                <text class="coupon-price red-price">¥50</text>
                <text class="coupon-desc">全场满200可用</text>
              </view>
              <image class="coupon-deco" src="/static/profile/15.svg" mode="aspectFit" />
            </view>
          </view>
        </scroll-view>
      </view>

      <!-- 功能菜单 -->
      <view class="menu-card">
        <view class="menu-item" @click="goOrders">
          <view class="menu-left">
            <view class="menu-icon-wrap">
              <image class="menu-icon" src="/static/profile/16.svg" mode="aspectFit" />
            </view>
            <text class="menu-name">历史订单</text>
          </view>
          <image class="menu-arrow" src="/static/profile/17.svg" mode="aspectFit" />
        </view>
        <view class="menu-item" @click="goAddress">
          <view class="menu-left">
            <view class="menu-icon-wrap">
              <image class="menu-icon" src="/static/profile/18.svg" mode="aspectFit" />
            </view>
            <text class="menu-name">地址管理</text>
          </view>
          <image class="menu-arrow" src="/static/profile/19.svg" mode="aspectFit" />
        </view>
        <view class="menu-item" @click="goService">
          <view class="menu-left">
            <view class="menu-icon-wrap">
              <image class="menu-icon" src="/static/profile/20.svg" mode="aspectFit" />
            </view>
            <text class="menu-name">客服中心</text>
          </view>
          <image class="menu-arrow" src="/static/profile/21.svg" mode="aspectFit" />
        </view>
      </view>

      <!-- 邀请好友Banner -->
      <view class="invite-banner">
        <image class="banner-bg" src="/static/profile/23.png" mode="aspectFill" />
        <view class="banner-mask">
          <view class="banner-text">
            <text class="banner-title">邀请好友撸串</text>
            <text class="banner-sub">各享 8.8 折扣券</text>
          </view>
          <view class="invite-btn" @click="invite">
            <text>立即邀请</text>
          </view>
        </view>
      </view>

      <!-- 退出登录 -->
      <view class="logout-btn" @click="logout">
        <text>退出登录</text>
      </view>

      <!-- 底部占位 -->
      <view class="bottom-placeholder" />
    </scroll-view>


  </view>
</template>

<script setup lang="ts">
const goHome = () => {
  uni.switchTab({ url: '/pages/index' });
};

const goMenu = () => {
  uni.switchTab({ url: '/pages/menu' });
};

const goPoints = () => {
  uni.showToast({ title: '积分商城', icon: 'none' });
};

const goFavorites = () => {
  uni.showToast({ title: '我的收藏', icon: 'none' });
};

const goCoupons = () => {
  uni.showToast({ title: '查看全部优惠券', icon: 'none' });
};

const goOrders = () => {
  uni.showToast({ title: '历史订单', icon: 'none' });
};

const goAddress = () => {
  uni.showToast({ title: '地址管理', icon: 'none' });
};

const goService = () => {
  uni.showToast({ title: '客服中心', icon: 'none' });
};

const invite = () => {
  uni.showToast({ title: '邀请好友', icon: 'none' });
};

const logout = () => {
  uni.showModal({
    title: '提示',
    content: '确定要退出登录吗？',
    success: (res) => {
      if (res.confirm) {
        uni.showToast({ title: '已退出登录', icon: 'success' });
      }
    },
  });
};
</script>

<style scoped>
.page {
  width: 100vw;
  height: 100vh;
  background:
    radial-gradient(ellipse 141.42% 141.42% at 0% 0%, rgba(167, 57, 24, 0.05) 0%, rgba(167, 57, 24, 0) 50%),
    radial-gradient(ellipse 141.42% 141.42% at 100% 0%, rgba(138, 75, 46, 0.03) 0%, rgba(138, 75, 46, 0) 50%),
    white;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

/* Header */
.header {
  height: 66.59px;
  background: rgba(248, 249, 250, 0.8);
  border-bottom: 1px solid #E1E3E4;
  backdrop-filter: blur(6px);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 16px;
  padding-top: var(--status-bar-height, 0);
  flex-shrink: 0;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 8px;
}

.fire-icon {
  width: 20px;
  height: 20px;
  margin-top: 2px;
}

.brand {
  font-size: 24px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  color: #A43716;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 12px;
}

.header-icon {
  width: 20px;
  height: 20px;
}

/* Content */
.content {
  flex: 1;
  padding: 0 16px;
  overflow: hidden;
}

/* User Section */
.user-section {
  display: flex;
  align-items: center;
  gap: 16px;
  margin-top: 32px;
}

.avatar-wrap {
  position: relative;
  width: 80px;
  height: 80px;
}

.avatar {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  outline: 2px solid #C54F2C;
  outline-offset: -2px;
  padding: 4px;
}

.level-badge {
  position: absolute;
  right: -2px;
  bottom: 0;
  min-width: 42px;
  height: 24px;
  background: #C54F2C;
  border-radius: 9999px;
  outline: 2px solid #F8F9FA;
  outline-offset: -2px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 8px;
}

.level-badge text {
  font-size: 10px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  color: #FFFBFF;
}

.user-info {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.user-name {
  font-size: 24px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  color: #191C1D;
}

.user-tag {
  display: flex;
  align-items: center;
  gap: 4px;
}

.crown-icon {
  width: 14px;
  height: 14px;
}

.user-tag text {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  letter-spacing: 0.6px;
  color: #58423C;
}

/* Stats Section */
.stats-section {
  display: flex;
  gap: 16px;
  margin-top: 24px;
}

.stat-card {
  background: white;
  box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.05);
  border-radius: 12px;
  outline: 1px solid #EDEEEF;
  outline-offset: -1px;
}

.stat-card.big {
  flex: 1;
  padding: 16px 17px;
  height: 140px;
}

.stat-label {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 500;
  color: #58423C;
}

.stat-value-wrap {
  display: flex;
  align-items: baseline;
  gap: 4px;
  margin-top: 8px;
}

.stat-value {
  font-size: 32px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  color: #C54F2C;
}

.stat-unit {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  letter-spacing: 0.6px;
  color: #A43716;
}

.progress-bar {
  width: 100%;
  height: 4px;
  background: #E1E3E4;
  border-radius: 9999px;
  margin-top: 12px;
  overflow: hidden;
}

.progress-fill {
  width: 75%;
  height: 100%;
  background: #C54F2C;
  border-radius: 9999px;
}

.stat-rank {
  font-size: 10px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 400;
  color: #8B716A;
  margin-top: 8px;
}

.stat-col {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.stat-card.small {
  width: 171px;
  height: 74px;
  padding: 17px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.small-card-left {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.small-label {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 500;
  color: #58423C;
}

.small-value {
  font-size: 16px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  color: #191C1D;
}

.heart-icon {
  width: 16px;
  height: 16px;
}

.arrow-icon {
  width: 16px;
  height: 16px;
}

/* Coupon Section */
.coupon-section {
  margin-top: 24px;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}

.section-title {
  font-size: 24px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  color: #191C1D;
}

.section-more {
  display: flex;
  align-items: center;
  gap: 4px;
}

.section-more text {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  letter-spacing: 0.6px;
  color: #A43716;
}

.more-arrow {
  width: 12px;
  height: 12px;
}

.coupon-scroll {
  width: 100%;
}

.coupon-list {
  display: flex;
  gap: 16px;
  padding: 4px 0;
}

.coupon-card {
  width: 200px;
  height: 126px;
  border-radius: 12px;
  outline: 1px solid #DFC0B7;
  outline-offset: -1px;
  padding: 17px;
  position: relative;
  overflow: hidden;
  flex-shrink: 0;
}

.coupon-card.orange {
  background: #FFDBCC;
}

.coupon-card.red {
  background: #FFDBD1;
}

.coupon-top {
  display: flex;
  align-items: center;
  gap: 4px;
}

.coupon-icon {
  width: 16px;
  height: 16px;
}

.coupon-tag {
  padding: 2px 8px;
  border-radius: 4px;
}

.coupon-tag text {
  font-size: 10px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  color: #FFFBFF;
}

.coupon-card.orange .coupon-tag {
  background: #A76343;
}

.coupon-card.red .coupon-tag.red-tag {
  background: #C54F2C;
}

.coupon-bottom {
  margin-top: 16px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.coupon-price {
  font-size: 24px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  color: #8A4B2E;
}

.coupon-price.red-price {
  color: #C54F2C;
}

.coupon-desc {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 500;
  color: #FFFBFF;
}

.coupon-deco {
  position: absolute;
  right: -10px;
  top: -15px;
  width: 60px;
  height: 60px;
}

/* Menu Card */
.menu-card {
  background: white;
  box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.05);
  border-radius: 12px;
  outline: 1px solid #EDEEEF;
  outline-offset: -1px;
  margin-top: 24px;
  overflow: hidden;
}

.menu-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px;
  height: 72px;
}

.menu-item + .menu-item {
  border-top: 1px solid #E1E3E4;
}

.menu-left {
  display: flex;
  align-items: center;
  gap: 16px;
}

.menu-icon-wrap {
  width: 40px;
  height: 40px;
  background: #EDEEEF;
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.menu-icon {
  width: 18px;
  height: 18px;
}

.menu-name {
  font-size: 18px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 400;
  color: #191C1D;
}

.menu-arrow {
  width: 16px;
  height: 16px;
}

/* Invite Banner */
.invite-banner {
  margin-top: 24px;
  height: 96px;
  border-radius: 12px;
  overflow: hidden;
  position: relative;
}

.banner-bg {
  width: 100%;
  height: 100%;
}

.banner-mask {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 16px;
}

.banner-text {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.banner-title {
  font-size: 24px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  color: white;
}

.banner-sub {
  font-size: 12px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 500;
  color: rgba(255, 255, 255, 0.8);
}

.invite-btn {
  min-width: 82px;
  height: 32px;
  background: #C54F2C;
  border-radius: 9999px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 12px;
}

.invite-btn text {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  letter-spacing: 0.6px;
  color: #FFFBFF;
}

/* Logout */
.logout-btn {
  margin-top: 24px;
  height: 62px;
  border-radius: 12px;
  outline: 2px solid #DFC0B7;
  outline-offset: -2px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.logout-btn text {
  font-size: 16px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  color: #8B716A;
}

.bottom-placeholder {
  height: 20px;
}


</style>
