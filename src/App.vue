<!--
 * @Author: KiraZz1
 * @Date: 2022-03-12 13:01:48
 * @LastEditTime: 2022-03-12 17:23:43
 * @Description: vue3整合Swiper8示例
 * @FilePath: /vue-swiper/src/App.vue
-->
<script setup>
import Swiper from './components/Swiper.vue'

const imgs = [
  {
    imgSrc: "https://ts2.cn.mm.bing.net/th?id=ORMS.40721fe2da4d2f909da27a182649516e&pid=Wdp&w=612&h=304&qlt=60&c=1&rs=1&dpr=1&p=0",
    redirectTo:"https://www.msn.cn/zh-cn/money/news/280%E7%B1%B3%E9%AB%98%E7%A9%BA-%E4%BB%96%E4%BB%AC-%E8%B5%B0%E9%92%A2%E4%B8%9D-%E8%B7%A8%E8%B6%8A%E9%95%BF%E6%B1%9F-%E4%B8%BA%E8%83%BD%E6%BA%90%E5%A4%A7%E5%8A%A8%E8%84%89-%E4%BD%93%E6%A3%80/ar-AAUVgbn?ocid=msedgntp",
    desc:"1336胜，NBA历史第一！波波维奇26载生涯早已荣誉满身"
  },
 {
    imgSrc: "https://ts1.cn.mm.bing.net/th?id=ORMS.406f254e68fde72e2de5fe6873e1beeb&pid=Wdp&w=612&h=304&qlt=60&c=1&rs=1&dpr=1&p=0",
    redirectTo:"https://pc.yiyouliao.com/msn/article.html?recId=925a24fc4e6e406a8d64b8bd4b9cc8f8_s&infoId=II00KVX5SRGCD7B",
    desc:"诺兰《奥本海默》继续加人《神偷大军》锁匠加盟"
  },
  {
    imgSrc: "https://ts1.cn.mm.bing.net/th?id=ORMS.0fe21454edfff644f6ca0cb4e224c8ed&pid=Wdp&w=612&h=304&qlt=60&c=1&rs=1&dpr=1&p=0",
    redirectTo:"https://www.msn.cn/zh-cn/entertainment/news/%E9%87%91%E5%BA%B8%E8%AF%9E%E8%BE%B098%E5%91%A8%E5%B9%B4-%E7%BF%81%E7%BE%8E%E7%8E%B2%E6%9C%B1%E8%8C%B5%E5%91%A8%E8%BF%85%E6%BC%94%E7%BB%8E%E7%9A%84-%E5%B0%84%E9%9B%95%E8%8B%B1%E9%9B%84%E4%BC%A0-%E4%B8%8E%E5%85%88%E7%94%9F%E4%B8%80%E5%90%8C%E8%BF%9C%E5%8E%BB/ar-AAUUKux?ocid=msedgntp",
    desc:"金庸诞辰98周年，翁美玲朱茵周迅演绎的《射雕英雄传》与先生一同远去"
  }
];

</script>

<template>
    <Swiper :imgs="imgs" :slideStyle="{ width: '305px', height: '149px'}" />
</template>

<style>

</style>
