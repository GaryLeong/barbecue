<template>
  <view class="page">
    <!-- 顶部导航栏 -->
    <view class="header">
      <view class="header-left">
        <image class="fire-icon" src="/static/checkout/1.svg" mode="aspectFit" />
        <text class="brand">Beijing BBQ</text>
      </view>
      <image class="close-icon" src="/static/checkout/2.svg" mode="aspectFit" @click="goBack" />
    </view>

    <!-- 主体内容 -->
    <scroll-view class="content" scroll-y>
      <!-- 桌号信息卡片 -->
      <view class="table-card">
        <view class="table-header">
          <view class="table-info">
            <text class="table-label">当前桌号</text>
            <text class="table-no">A-12 桌</text>
          </view>
          <view class="status-badge">
            <image class="status-icon" src="/static/checkout/3.svg" mode="aspectFit" />
            <text>制作中</text>
          </view>
        </view>
        <view class="table-stats">
          <view class="stat-card">
            <text class="stat-label">总计串数</text>
            <view class="stat-value">
              <text class="stat-num">42</text>
              <image class="stat-icon" src="/static/checkout/4.svg" mode="aspectFit" />
            </view>
          </view>
          <view class="stat-card">
            <text class="stat-label">口味概览</text>
            <view class="stat-value">
              <image class="flavor-icon" src="/static/checkout/5.svg" mode="aspectFit" />
              <text class="flavor-text">重辣为主</text>
            </view>
          </view>
        </view>
      </view>

      <!-- 操作按钮 -->
      <view class="action-btns">
        <view class="btn-outline" @click="urgeCook">
          <image class="btn-icon" src="/static/checkout/6.svg" mode="aspectFit" />
          <text>催烤</text>
        </view>
        <view class="btn-primary" @click="goToMenu">
          <image class="btn-icon" src="/static/checkout/7.svg" mode="aspectFit" />
          <text>继续加菜</text>
        </view>
      </view>

      <!-- 订单详情 -->
      <view class="order-section">
        <view class="order-header">
          <text class="order-title">订单详情</text>
          <text class="order-batch">(共3个批次)</text>
        </view>

        <!-- 重辣口味批次 -->
        <view class="batch">
          <view class="batch-header spicy">
            <image class="batch-icon" src="/static/checkout/8.svg" mode="aspectFit" />
            <text class="batch-name">重辣口味</text>
            <text class="batch-count">18串</text>
          </view>
          <view class="batch-items">
            <view class="item-card">
              <image class="item-img" src="/static/checkout/13.png" mode="aspectFill" />
              <view class="item-info">
                <text class="item-name">秘制羊肉串</text>
                <text class="item-sub">小计: 10串</text>
                <view class="item-bottom">
                  <text class="item-price">¥60.00</text>
                  <view class="status-tag served">
                    <text>已上桌</text>
                  </view>
                </view>
              </view>
            </view>
            <view class="item-card">
              <image class="item-img" src="/static/checkout/14.png" mode="aspectFill" />
              <view class="item-info">
                <text class="item-name">火辣牛蹄筋</text>
                <text class="item-sub">小计: 8串</text>
                <view class="item-bottom">
                  <text class="item-price">¥48.00</text>
                  <view class="status-tag cooking">
                    <text>烤制中</text>
                  </view>
                </view>
              </view>
            </view>
          </view>
        </view>

        <!-- 蒜香/微辣批次 -->
        <view class="batch">
          <view class="batch-header mild">
            <image class="batch-icon" src="/static/checkout/9.svg" mode="aspectFit" />
            <text class="batch-name">蒜香/微辣</text>
            <text class="batch-count">12串</text>
          </view>
          <view class="batch-items">
            <view class="item-card">
              <image class="item-img" src="/static/checkout/15.png" mode="aspectFill" />
              <view class="item-info">
                <text class="item-name">蒜香大生蚝</text>
                <text class="item-sub">小计: 4只</text>
                <view class="item-bottom">
                  <text class="item-price">¥88.00</text>
                  <view class="status-tag pending">
                    <text>待准备</text>
                  </view>
                </view>
              </view>
            </view>
          </view>
        </view>
      </view>

      <!-- 底部占位 -->
      <view class="bottom-placeholder" />
    </scroll-view>

    <!-- 底部结算栏 -->
    <view class="checkout-bar">
      <view class="checkout-content">
        <view class="amount-wrap">
          <text class="amount-label">待付金额</text>
          <view class="amount-value">
            <text class="amount-symbol">¥</text>
            <text class="amount-num">196.00</text>
          </view>
        </view>
        <view class="pay-btn" @click="pay">
          <text>结账</text>
        </view>
      </view>
    </view>


  </view>
</template>

<script setup lang="ts">
const goBack = () => {
  uni.navigateBack();
};

const goHome = () => {
  uni.switchTab({ url: '/pages/index/index' });
};

const goToMenu = () => {
  uni.switchTab({ url: '/pages/menu/index' });
};

const goToProfile = () => {
  uni.switchTab({ url: '/pages/profile/index' });
};

const urgeCook = () => {
  uni.showToast({ title: '已发送催烤通知', icon: 'none' });
};

const pay = () => {
  uni.showToast({ title: '正在跳转支付...', icon: 'none' });
};
</script>

<style scoped>
.page {
  width: 100vw;
  height: 100vh;
  background: #F8F9FA;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

/* Header */
.header {
  height: 65.59px;
  background: #F8F9FA;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
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

.close-icon {
  width: 20px;
  height: 20px;
}

/* Content */
.content {
  flex: 1;
  padding: 0 16px;
  overflow: hidden;
}

/* Table Card */
.table-card {
  background: #EDEEEF;
  box-shadow: 0px 4px 12px rgba(167, 57, 24, 0.1);
  border-radius: 12px;
  outline: 1px solid rgba(164, 55, 22, 0.1);
  outline-offset: -1px;
  overflow: hidden;
  padding: 17px;
  margin-top: 16px;
}

.table-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 16px;
}

.table-info {
  display: flex;
  flex-direction: column;
}

.table-label {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 500;
  letter-spacing: 0.6px;
  color: #58423C;
}

.table-no {
  font-size: 28px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  color: #A43716;
  margin-top: 2px;
}

.status-badge {
  display: flex;
  align-items: center;
  gap: 4px;
  background: #A43716;
  border-radius: 9999px;
  padding: 3px 10px 3px 6px;
}

.status-badge text {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  letter-spacing: 0.6px;
  color: white;
}

.status-icon {
  width: 12px;
  height: 12px;
}

.table-stats {
  display: flex;
  gap: 16px;
}

.stat-card {
  flex: 1;
  background: rgba(225, 227, 228, 0.5);
  border-radius: 8px;
  outline: 1px solid rgba(223, 192, 183, 0.3);
  outline-offset: -1px;
  padding: 8px;
}

.stat-label {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 500;
  color: #555E72;
}

.stat-value {
  display: flex;
  align-items: center;
  gap: 4px;
  margin-top: 4px;
}

.stat-num {
  font-size: 20px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 600;
  color: #191C1D;
}

.stat-icon {
  width: 16px;
  height: 16px;
}

.flavor-icon {
  width: 16px;
  height: 16px;
}

.flavor-text {
  font-size: 20px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 600;
  color: #191C1D;
}

/* Action Buttons */
.action-btns {
  display: flex;
  gap: 16px;
  margin-top: 16px;
}

.btn-outline {
  flex: 1;
  height: 46px;
  background: #F8F9FA;
  border-radius: 12px;
  outline: 1px solid #A43716;
  outline-offset: -1px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
}

.btn-outline text {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  letter-spacing: 0.6px;
  color: #A43716;
}

.btn-primary {
  flex: 1;
  height: 46px;
  background: #A43716;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  box-shadow: 0px 4px 6px -4px rgba(164, 55, 22, 0.2), 0px 10px 15px -3px rgba(164, 55, 22, 0.2);
}

.btn-primary text {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  letter-spacing: 0.6px;
  color: white;
}

.btn-icon {
  width: 16px;
  height: 16px;
}

/* Order Section */
.order-section {
  margin-top: 24px;
}

.order-header {
  display: flex;
  align-items: baseline;
  gap: 8px;
  margin-bottom: 16px;
}

.order-title {
  font-size: 20px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 600;
  color: #191C1D;
}

.order-batch {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 400;
  color: #58423C;
}

/* Batch */
.batch {
  margin-bottom: 16px;
}

.batch-header {
  display: flex;
  align-items: center;
  gap: 6px;
  height: 26px;
  padding-left: 12px;
  margin-bottom: 8px;
}

.batch-header.spicy {
  border-left: 4px solid #BA1A1A;
}

.batch-header.mild {
  border-left: 4px solid #8A4B2E;
}

.batch-icon {
  width: 16px;
  height: 16px;
}

.batch-name {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  letter-spacing: 0.6px;
}

.batch-header.spicy .batch-name {
  color: #BA1A1A;
}

.batch-header.mild .batch-name {
  color: #8A4B2E;
}

.batch-count {
  font-size: 12px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 500;
  color: #58423C;
}

.batch-items {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.item-card {
  display: flex;
  background: #F3F4F5;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 12px;
  outline: 1px solid rgba(223, 192, 183, 0.1);
  outline-offset: -1px;
  padding: 9px;
}

.item-img {
  width: 80px;
  height: 80px;
  border-radius: 8px;
  flex-shrink: 0;
}

.item-info {
  flex: 1;
  margin-left: 16px;
  display: flex;
  flex-direction: column;
}

.item-name {
  font-size: 18px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 400;
  color: #191C1D;
}

.item-sub {
  font-size: 12px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 500;
  color: #58423C;
  margin-top: 4px;
}

.item-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
}

.item-price {
  font-size: 16px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 400;
  color: #A43716;
}

.status-tag {
  padding: 2px 8px;
  border-radius: 4px;
}

.status-tag text {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 500;
}

.status-tag.served {
  background: #D9E2FA;
}

.status-tag.served text {
  color: #5B6478;
}

.status-tag.cooking {
  background: #A76343;
}

.status-tag.cooking text {
  color: #FFFBFF;
}

.status-tag.pending {
  background: #E7E8E9;
}

.status-tag.pending text {
  color: #555E72;
}

.bottom-placeholder {
  height: 20px;
}

/* Checkout Bar */
.checkout-bar {
  height: 101px;
  background: rgba(248, 249, 250, 0.9);
  border-top: 1px solid rgba(223, 192, 183, 0.3);
  backdrop-filter: blur(6px);
  box-shadow: 0px 4px 6px -4px rgba(0, 0, 0, 0.1), 0px 10px 15px -3px rgba(0, 0, 0, 0.1);
  flex-shrink: 0;
}

.checkout-content {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 16px;
}

.amount-wrap {
  display: flex;
  flex-direction: column;
}

.amount-label {
  font-size: 12px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 500;
  color: #58423C;
}

.amount-value {
  display: flex;
  align-items: baseline;
  gap: 2px;
  margin-top: 4px;
}

.amount-symbol {
  font-size: 16px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 400;
  color: #A43716;
}

.amount-num {
  font-size: 24px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  color: #191C1D;
}

.pay-btn {
  width: 120px;
  height: 52px;
  background: #A43716;
  border-radius: 9999px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0px 4px 6px -4px rgba(164, 55, 22, 0.2), 0px 10px 15px -3px rgba(164, 55, 22, 0.2);
}

.pay-btn text {
  font-size: 20px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 600;
  color: white;
}


</style>
