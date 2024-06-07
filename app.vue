<template>
 <!-- 页面路由 -->
 <NuxtLink to="/"></NuxtLink>
 <NuxtLink to="/video"></NuxtLink>

 <NuxtPage keepalive="{max:10"/>
</template>

<script setup lang="ts">
useSeoMeta({
    title:'哔哩哔哩  bilibili',
    description:'哔哩哔哩 (bilibili.com)是国内知名的视频弹幕网站 ',
    keywords:'哔哩哔哩,B站,bilibili,动画，电影，动漫'
})

</script>
<style lang="scss">
// 基础样式
@import './assets/styles/base.scss';
// 字体图标
@import './assets/styles/iconfont.scss';
:root{
    --van-primary-color: #FB7299 !important;
}

</style>
