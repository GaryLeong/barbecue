<template>
  <view class="page">
    <!-- 内容区 -->
    <view class="content-wrap">
      <!-- 左侧分类导航 -->
      <view class="sidebar">
      <scroll-view class="sidebar-scroll" scroll-y>
        <!-- 食材分类 -->
        <view class="category-group">
          <text class="group-title">食材分类</text>
          <view
            class="category-item"
            :class="{ active: activeCategory === 0 }"
            @click="activeCategory = 0"
          >
            <image
              v-if="activeCategory === 0"
              class="active-indicator"
              src="/static/menu/2.svg"
              mode="aspectFit"
            />
            <image class="cat-icon" src="/static/menu/1.svg" mode="aspectFit" />
            <text class="cat-name">招牌推荐</text>
          </view>
          <view
            class="category-item"
            :class="{ active: activeCategory === 1 }"
            @click="activeCategory = 1"
          >
            <image class="cat-icon" src="/static/menu/3.svg" mode="aspectFit" />
            <text class="cat-name">经典肉类</text>
          </view>
          <view
            class="category-item"
            :class="{ active: activeCategory === 2 }"
            @click="activeCategory = 2"
          >
            <image class="cat-icon" src="/static/menu/4.svg" mode="aspectFit" />
            <text class="cat-name">时令蔬菜</text>
          </view>
        </view>

        <!-- 味型风格 -->
        <view class="category-group">
          <text class="group-title">味型风格</text>
          <view
            class="category-item"
            :class="{ active: activeCategory === 3 }"
            @click="activeCategory = 3"
          >
            <image class="cat-icon" src="/static/menu/5.svg" mode="aspectFit" />
            <text class="cat-name">炭火烤制</text>
          </view>
          <view
            class="category-item"
            :class="{ active: activeCategory === 4 }"
            @click="activeCategory = 4"
          >
            <image class="cat-icon" src="/static/menu/6.svg" mode="aspectFit" />
            <text class="cat-name">生鲜刺身</text>
          </view>
        </view>
      </scroll-view>
    </view>

    <!-- 右侧商品列表 -->
    <view class="main">
      <scroll-view class="main-scroll" scroll-y>
        <!-- 列表头部 -->
        <view class="list-header">
          <text class="list-title">{{ currentCategoryName }}</text>
          <text class="list-count">共 {{ productList.length }} 款商品</text>
        </view>

        <!-- 商品卡片 -->
        <view class="product-list">
          <view class="product-card" v-for="(item, index) in productList" :key="index">
            <image class="product-img" :src="item.img" mode="aspectFill" />
            <view class="product-info">
              <text class="product-name">{{ item.name }}</text>
              <view class="product-tags">
                <view v-if="item.spicy" class="tag spicy-tag">
                  <image class="tag-icon" :src="item.spicyIcon" mode="aspectFit" />
                  <text>{{ item.spicy }}</text>
                </view>
                <view v-if="item.tag" class="tag gray-tag">
                  <text>{{ item.tag }}</text>
                </view>
              </view>
              <text class="product-spec">{{ item.spec }}</text>
              <view class="product-bottom">
                <view class="price-wrap">
                  <text class="price-symbol">¥</text>
                  <text class="price-num">{{ item.price }}</text>
                  <text class="price-unit">/份</text>
                </view>
                <view class="add-btn" @click="addToCart(item)">
                  <image class="add-icon" :src="item.addIcon" mode="aspectFit" />
                </view>
              </view>
            </view>
          </view>
        </view>

        <!-- 底部占位 -->
        <view class="bottom-placeholder" />
      </scroll-view>
    </view>
    </view>


  </view>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

const activeCategory = ref(0);

const categoryNames = ['招牌推荐', '经典肉类', '时令蔬菜', '炭火烤制', '生鲜刺身'];

const currentCategoryName = computed(() => categoryNames[activeCategory.value]);

const productList = ref([
  {
    name: '呼伦贝尔羊肉串',
    img: '/static/menu/12.png',
    spicy: '微辣',
    spicyIcon: '/static/menu/7.svg',
    tag: '招牌必点',
    spec: '3串起点 · 约150g',
    price: 18,
    addIcon: '/static/menu/8.svg',
  },
  {
    name: '秘制麻辣牛肉',
    img: '/static/menu/13.png',
    spicy: '特辣',
    spicyIcon: '/static/menu/9.svg',
    tag: '火爆人气',
    spec: '2串起点 · 约120g',
    price: 22,
    addIcon: '/static/menu/10.svg',
  },
  {
    name: '蒜蓉粉丝烤生蚝',
    img: '/static/menu/14.png',
    spicy: '',
    spicyIcon: '',
    tag: '每日限量',
    spec: '2只起点 · 产地直供',
    price: 28,
    addIcon: '/static/menu/11.svg',
  },
]);

const addToCart = (item: any) => {
  uni.showToast({
    title: `已添加 ${item.name}`,
    icon: 'none',
  });
};

const goHome = () => {
  uni.switchTab({ url: '/pages/index/index' });
};

const goToProfile = () => {
  uni.switchTab({ url: '/pages/profile/profile' });
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

/* 左侧分类栏 */
.sidebar {
  width: 96px;
  height: 100%;
  background: #F3F4F5;
  border-right: 1px solid rgba(223, 192, 183, 0.2);
  flex-shrink: 0;
  padding-top: var(--status-bar-height, 0);
}

.sidebar-scroll {
  height: 100%;
}

.category-group {
  padding: 16px 12px;
}

.group-title {
  font-size: 10px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  letter-spacing: 1px;
  color: #58423C;
  opacity: 0.6;
  margin-bottom: 12px;
  display: block;
}

.category-item {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 8px 0;
  margin-bottom: 4px;
}

.active-indicator {
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 3px;
  height: 20px;
}

.cat-icon {
  width: 24px;
  height: 24px;
}

.cat-name {
  font-size: 11px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 700;
  color: #58423C;
  margin-top: 4px;
}

.category-item.active .cat-name {
  color: #A43716;
}

/* 右侧主内容 */
.main {
  flex: 1;
  height: 100%;
  overflow: hidden;
}

.main-scroll {
  height: 100%;
  padding: 0 16px;
}

.list-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 0;
  margin-top: var(--status-bar-height, 0);
}

.list-title {
  font-size: 16px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 400;
  color: #191C1D;
}

.list-count {
  font-size: 12px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 500;
  color: #58423C;
}

/* 商品卡片 */
.product-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.product-card {
  display: flex;
  background: white;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 12px;
  outline: 1px solid rgba(223, 192, 183, 0.1);
  outline-offset: -1px;
  overflow: hidden;
}

.product-img {
  width: 128px;
  height: 126px;
  flex-shrink: 0;
}

.product-info {
  flex: 1;
  padding: 12px;
  display: flex;
  flex-direction: column;
}

.product-name {
  font-size: 16px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 400;
  color: #191C1D;
  line-height: 1.3;
}

.product-tags {
  display: flex;
  gap: 4px;
  margin-top: 8px;
  flex-wrap: wrap;
}

.tag {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 2px 6px;
  border-radius: 4px;
  height: 19px;
}

.spicy-tag {
  background: rgba(164, 55, 22, 0.1);
}

.spicy-tag text {
  font-size: 10px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 400;
  color: #A43716;
}

.gray-tag {
  background: #E1E3E4;
}

.gray-tag text {
  font-size: 10px;
  font-family: 'WenQuanYi Zen Hei', sans-serif;
  font-weight: 400;
  color: #58423C;
}

.tag-icon {
  width: 8px;
  height: 8px;
}

.product-spec {
  font-size: 10px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 400;
  color: #58423C;
  margin-top: 8px;
}

.product-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
}

.price-wrap {
  display: flex;
  align-items: baseline;
}

.price-symbol {
  font-size: 14px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  color: #A43716;
}

.price-num {
  font-size: 18px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 700;
  color: #A43716;
}

.price-unit {
  font-size: 10px;
  font-family: 'Plus Jakarta Sans', sans-serif;
  font-weight: 400;
  color: #58423C;
  margin-left: 2px;
}

.add-btn {
  width: 32px;
  height: 32px;
  background: #A43716;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.add-icon {
  width: 14px;
  height: 14px;
}

.bottom-placeholder {
  height: 20px;
}

/* Content Wrap */
.content-wrap {
  flex: 1;
  display: flex;
  overflow: hidden;
}


</style>
