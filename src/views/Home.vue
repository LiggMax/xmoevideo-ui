<script setup>
import {ref} from 'vue';

// 模拟数据
const categories = ref(['推荐', '番剧', '剧场版', '4K', '特次元']);
const activeCategory = ref('推荐');

const bannerData = ref([{
      title: '快露起来！绝望啊同学!!',
      image: 'https://play.xfvod.pro/images/hb/ywsns2.jpg'
    },
      {
        title: '快露起来！绝望啊同学!!',
        image: 'https://play.xfvod.pro/images/hb/ywsns2.jpg'
      }
    ]
);

const notificationText = ref('软件使用指南');

const categoryButtons = ref([
  {id: 1, name: '全部', image: '/src/assets/svg/category-all.svg'},
  {id: 2, name: '榜单', image: '/src/assets/svg/category-ranking.svg'},
  {id: 3, name: '海贼王', image: '/src/assets/svg/category-onepiece.svg'},
  {id: 4, name: '追番', image: '/src/assets/svg/category-following.svg'}
]);

const animeCalendar = ref([
  {
    id: 1,
    title: '夏日重现',
    episode: '第13集',
    day: '每周一',
    time: '21:30更新',
    image: '/src/assets/svg/anime1.svg'
  },
  {
    id: 2,
    title: '鱼旅 That',
    episode: '',
    day: '每周一',
    time: '22:00更新',
    image: '/src/assets/svg/anime2.svg'
  },
  {
    id: 3,
    title: '测不准的阿波连同学 第二季',
    episode: '',
    day: '每周一',
    time: '21:30更新',
    image: '/src/assets/svg/anime3.svg'
  },
  {
    id: 4,
    title: '快露起来！绝望啊同学!!',
    episode: '',
    day: '每周一',
    time: '01:00更新',
    image: '/src/assets/svg/anime4.svg'
  },
  {
    id: 5,
    title: '记忆链接',
    episode: '',
    day: '每周三',
    time: '21:45更新',
    image: '/src/assets/svg/anime5.svg'
  },
  {
    id: 6,
    title: '凡德回道道理上无敌',
    episode: '',
    day: '每周三',
    time: '23:00更新',
    image: '/src/assets/svg/anime6.svg'
  }
]);

const newAnimes = ref([
  {
    id: 1,
    title: '猎人×猎人',
    views: '播放量 401万',
    image: '/src/assets/svg/new-anime1.svg'
  },
  {
    id: 2,
    title: '间谍过家家',
    views: '播放量 401万',
    image: '/src/assets/svg/new-anime2.svg'
  }
]);
</script>

<template>
  <div class="home-container">
    <!-- 顶部导航栏 -->
    <div class="header">
      <div class="avatar">
        <img src="/src/assets/images/avatar.jpg" alt="头像">
      </div>
      <div class="search-bar">
        <img src="../assets/svg/SearchIcon.svg" style="width: 25px " alt="搜索">
        <span class="search-placeholder">搜索</span>
      </div>
      <div class="header-icons">
        <img src="../assets/svg/Recording.svg" style="width: 25px" alt="">
        <i class="menu-icon">⋮</i>
      </div>
    </div>

    <!-- 分类标签栏 -->
    <div class="category-tabs">
      <div
          v-for="category in categories"
          :key="category"
          :class="['category-tab', { active: category === activeCategory }]"
          @click="activeCategory = category"
      >
        {{ category }}
      </div>
    </div>

    <!-- 轮播图 -->
    <div class="banner">
      <img :src="bannerData.image" alt="Banner">
      <div class="banner-title">{{ bannerData.title }}</div>
    </div>

    <!-- 通知栏 -->
    <div class="notification-bar">
      <i class="notification-icon">🔔</i>
      <span class="notification-text">{{ notificationText }}</span>
      <i class="arrow-icon">›</i>
    </div>

    <!-- 分类按钮 -->
    <div class="category-buttons">
      <div
          v-for="button in categoryButtons"
          :key="button.id"
          class="category-button"
      >
        <img :src="button.image" alt="Category">
        <div class="category-name">{{ button.name }}</div>
      </div>
    </div>

    <!-- 追番日历 -->
    <div class="anime-calendar-section">
      <div class="section-header">
        <div class="section-title">
          <i class="calendar-icon">📅</i>
          <span>追番日历</span>
        </div>
        <div class="more-link">更多</div>
      </div>
      <div class="anime-calendar">
        <div class="calendar-column">
          <div
              v-for="anime in animeCalendar.slice(0, 4)"
              :key="anime.id"
              class="calendar-item"
              @click="handleAnimeClick(anime)"
          >
            <div class="calendar-item-image">
              <img :src="anime.image" alt="Anime">
              <div class="episode-badge">更新至第{{ anime.currentEpisode }}话</div>
            </div>
            <div class="calendar-item-info">
              <div class="anime-title">{{ anime.title }}</div>
              <div class="anime-episode">{{ anime.episode }}</div>
              <div class="anime-schedule">
                <span class="schedule-day">{{ anime.day }}</span>
                <span class="schedule-time">{{ anime.time }}</span>
              </div>
            </div>
          </div>
        </div>
        <div class="calendar-column">
          <div
              v-for="anime in animeCalendar.slice(4, 6)"
              :key="anime.id"
              class="calendar-item"
          >
            <div class="calendar-item-image">
              <img :src="anime.image" alt="Anime">
            </div>
            <div class="calendar-item-info">
              <div class="anime-title">{{ anime.title }}</div>
              <div class="anime-episode">{{ anime.episode }}</div>
              <div class="anime-schedule">{{ anime.day }} · {{ anime.time }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 四月新番 -->
    <div class="new-anime-section">
      <div class="section-header">
        <div class="section-title">
          <i class="new-icon">🌸</i>
          <span>四月新番</span>
        </div>
        <div class="new-anime-tag">更多新番</div>
      </div>
      <div class="new-anime-list">
        <div
            v-for="anime in newAnimes"
            :key="anime.id"
            class="new-anime-item"
            @click="handleAnimeClick(anime)"
        >
          <div class="new-anime-image">
            <img :src="anime.image" alt="New Anime">
            <div class="new-anime-overlay">
              <div class="new-anime-rating">⭐ {{ anime.rating }}</div>
              <div class="new-anime-episode-count">更新至{{ anime.episodeCount }}话</div>
            </div>
          </div>
          <div class="new-anime-info">
            <div class="new-anime-title">{{ anime.title }}</div>
            <div class="new-anime-meta">
              <span class="new-anime-views">{{ anime.views }}观看</span>
              <span class="new-anime-category">{{ anime.category }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 底部导航栏 -->
    <div class="bottom-nav">
      <div class="nav-item active">
        <i class="nav-icon">🏠</i>
        <span class="nav-text">首页</span>
      </div>
      <div class="nav-item">
        <i class="nav-icon">🎬</i>
        <span class="nav-text">影视名录</span>
      </div>
      <div class="nav-item">
        <i class="nav-icon">👤</i>
        <span class="nav-text">我的</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home-container {
  max-width: 100%;
  margin: 0 auto;
  padding: 0;
  font-family: 'PingFang SC', 'Helvetica Neue', Arial, sans-serif;
  color: #333;
  background-color: #f5f5f5;
  position: relative;
  min-height: 100vh;
}

/* 顶部导航栏样式 */
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 15px;
  background-color: #ffb6c1;
  position: sticky;
  top: 0;
  z-index: 100;
}

.avatar img {
  width: 32px;
  height: 32px;
  border-radius: 50%;
}

.search-bar {
  display: flex;
  align-items: center;
  background-color: rgba(255, 255, 255, 0.3);
  border-radius: 20px;
  padding: 6px 15px;
  flex: 1;
  margin: 0 15px;
}

.search-icon {
  margin-right: 8px;
  color: #666;
}

.search-placeholder {
  color: #666;
  font-size: 14px;
}

.header-icons {
  display: flex;
  gap: 15px;
}

/* 分类标签栏样式 */
.category-tabs {
  display: flex;
  overflow-x: auto;
  padding: 10px 0;
  background-color: #fff;
  border-bottom: 1px solid #eee;
}

.category-tab {
  padding: 5px 15px;
  font-size: 14px;
  white-space: nowrap;
  cursor: pointer;
}

.category-tab.active {
  color: #ff6b81;
  font-weight: bold;
  position: relative;
}

.category-tab.active::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 20px;
  height: 2px;
  background-color: #ff6b81;
}

/* 轮播图样式 */
.banner {
  position: relative;
  width: 100%;
  height: 180px;
  overflow: hidden;
  margin-bottom: 10px;
}

.banner img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.banner-title {
  position: absolute;
  bottom: 15px;
  left: 15px;
  color: #fff;
  font-size: 16px;
  font-weight: bold;
  text-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
}

/* 通知栏样式 */
.notification-bar {
  display: flex;
  align-items: center;
  background-color: #fff;
  padding: 10px 15px;
  margin-bottom: 10px;
  border-radius: 5px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.notification-icon {
  margin-right: 10px;
  color: #ff6b81;
}

.notification-text {
  flex: 1;
  font-size: 14px;
}

.arrow-icon {
  color: #999;
}

/* 分类按钮样式 */
.category-buttons {
  display: flex;
  justify-content: space-between;
  padding: 0 10px 15px;
  background-color: #fff;
  margin-bottom: 10px;
}

.category-button {
  width: 22%;
  text-align: center;
}

.category-button img {
  width: 100%;
  height: 40px;
  border-radius: 10px;
  object-fit: cover;
  margin-bottom: 5px;
}

.category-name {
  font-size: 12px;
  color: #666;
}

/* 追番日历样式 */
.anime-calendar-section {
  background-color: #fff;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 5px;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 15px;
}

.section-title {
  display: flex;
  align-items: center;
  font-size: 16px;
  font-weight: bold;
}

.calendar-icon, .new-icon {
  margin-right: 5px;
  color: #ff6b81;
}

.more-link {
  font-size: 12px;
  color: #999;
  padding: 2px 8px;
  background-color: #f5f5f5;
  border-radius: 10px;
}

.anime-calendar {
  display: flex;
  gap: 10px;
}

.calendar-column {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.calendar-item {
  display: flex;
  background-color: #f9f9f9;
  border-radius: 5px;
  overflow: hidden;
}

.calendar-item-image {
  width: 120px;
  height: 80px;
  flex-shrink: 0;
  position: relative;
  border-radius: 8px;
  overflow: hidden;
}

.calendar-item-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.calendar-item:hover .calendar-item-image img {
  transform: scale(1.05);
}

.episode-badge {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.6);
  color: #fff;
  font-size: 10px;
  padding: 2px 6px;
  text-align: center;
}

.calendar-item-info {
  padding: 8px 12px;
  flex: 1;
}

.anime-title {
  font-size: 14px;
  font-weight: bold;
  margin-bottom: 4px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  color: #333;
}

.anime-episode {
  font-size: 12px;
  color: #666;
  margin-bottom: 4px;
}

.anime-schedule {
  font-size: 11px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.schedule-day {
  color: #ff6b81;
  font-weight: 500;
}

.schedule-time {
  color: #999;
}

/* 四月新番样式 */
.new-anime-section {
  background-color: #fff;
  padding: 15px;
  margin-bottom: 70px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.new-anime-tag {
  font-size: 12px;
  color: #ff6b81;
  background-color: #fff0f5;
  padding: 4px 12px;
  border-radius: 15px;
  transition: all 0.3s ease;
  cursor: pointer;
}

.new-anime-tag:hover {
  background-color: #ff6b81;
  color: #fff;
}

.new-anime-list {
  display: flex;
  gap: 15px;
  overflow-x: auto;
  padding: 10px 0;
  scrollbar-width: none;
}

.new-anime-list::-webkit-scrollbar {
  display: none;
}

.new-anime-item {
  width: 45%;
  flex-shrink: 0;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.new-anime-item:hover {
  transform: translateY(-2px);
}

.new-anime-image {
  width: 100%;
  height: 140px;
  border-radius: 8px;
  overflow: hidden;
  margin-bottom: 8px;
  position: relative;
}

.new-anime-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.new-anime-item:hover .new-anime-image img {
  transform: scale(1.05);
}

.new-anime-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 8px;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.7));
  color: #fff;
  font-size: 11px;
}

.new-anime-rating {
  margin-bottom: 4px;
}

.new-anime-episode-count {
  font-size: 10px;
  opacity: 0.9;
}

.new-anime-info {
  padding: 0 4px;
}

.new-anime-title {
  font-size: 14px;
  font-weight: bold;
  margin-bottom: 4px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  color: #333;
}

.new-anime-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 11px;
}

.new-anime-views {
  color: #666;
}

.new-anime-category {
  color: #ff6b81;
  background-color: #fff0f5;
  padding: 2px 6px;
  border-radius: 8px;
  font-size: 10px;
}

/* 底部导航栏样式 */
.bottom-nav {
  display: flex;
  justify-content: space-around;
  align-items: center;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #fff;
  padding: 10px 0;
  box-shadow: 0 -1px 5px rgba(0, 0, 0, 0.1);
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-size: 12px;
  color: #999;
}

.nav-item.active {
  color: #ff6b81;
}

.nav-icon {
  font-size: 20px;
  margin-bottom: 3px;
}
</style>