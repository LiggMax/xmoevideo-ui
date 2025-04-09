<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const animeId = ref(route.params.id)
const animeDetail = ref(null)

onMounted(() => {
  // 这里将添加获取番剧详情的逻辑
  console.log('Anime ID:', animeId.value)
})
</script>

<template>
  <div class="anime-detail">
    <h2>番剧详情</h2>
    <div v-if="animeDetail" class="detail-content">
      <!-- 这里将添加番剧详情的展示内容 -->
    </div>
    <div v-else>
      加载中...
    </div>
  </div>
</template>

<style scoped>
.anime-detail {
  padding: 20px;
}

.detail-content {
  margin-top: 20px;
}
</style>