<script setup lang="ts">
import type { VedioItem } from "@/types/vedio.ts";
const { data: channelList } = await useFetch("/api/channel");
const { data: videoList } = await useFetch("/api/video");
// console.log(channelList);
// console.log(videoList);types/vedio.d.ts

const list = ref<VedioItem[]>([]);
const loading = ref(false);
const finished = ref(false);
let page = ref<number>(1);
let pageSize = ref<number>(20);
const onLoad = () => {
  loading.value = false;
  const data = videoList.value?.slice(
    (page.value - 1) * pageSize.value,
    page.value * pageSize.value
  ) as VedioItem[];
  list.value.push(...data);
  page.value++;
  if (videoList.value?.length === list.value.length) finished.value = true;
};


onLoad();
</script>

<template>
  <AppHeader></AppHeader>
  <!-- 频道模块 -->
  <van-tabs>
    <van-tab v-for="item in channelList" :key="item.id" :title="item.name" />
  </van-tabs>
  <!-- 视频列表 -->

  <van-list v-model:loading="loading" :finished="finished" finished-text="没有更多了" @load="onLoad">
    <div class="video-list">
    
      <AppVedio v-for="item in list" :key="item.bvid" :item="item" :to="`/video/${item.bvid}`"></AppVedio>
    </div>
  </van-list>
</template>

<style lang="scss">


// 视频列表
.video-list {
  display: flex;
  flex-wrap: wrap;
  padding: 10px 5px;
}

// 视频卡片
.v-card {
  width: 50%;
  padding: 0 5px 10px;

  .card {
    position: relative;
    background: #f3f3f3 url(@/assets/images/default.png) center no-repeat;
    background-size: 36%;
    border-radius: 2px;
    overflow: hidden;

    .card-img {
      .pic {
        height: 100px;
        width: 100%;
        object-fit: cover;
      }
    }

    .count {
      background-image: linear-gradient(0deg, #000000d9, #0000);
      color: #fff;
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      font-size: 12px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 5px 6px;

      span {
        .iconfont {
          font-size: 12px;
        }
      }
    }
  }

  .title {
    margin-top: 5px;
    font-size: 12px;
    color: #212121;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }
}
</style>
