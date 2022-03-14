<!--
 * @Author: KiraZz1
 * @Date: 2022-03-12 13:03:16
 * @LastEditTime: 2022-03-12 17:25:24
 * @Description: vue3整合Swiper8示例
 * @FilePath: /vue-swiper/src/components/Swiper.vue
-->
<template>
    <!-- <swiper
    :autoplay="swiper_options.autoplay"
    :loop="swiper_options.loop"
    :speed="swiper_options.speed"
    :spaceBetween="swiper_options.spaceBetween"
    :coverflowEffect="swiper_options.coverflowEffect"
    :centeredSlides="swiper_options.centeredSlides"
    :slidesPerView="swiper_options.slidesPerView"
    effect="coverflow"
    >-->
    <div style="width: 600px;">
        <Swiper
            :autoplay="swiper_options.autoplay"
            :loop="swiper_options.loop"
            :pagination="swiper_options.pagination"
            :navigation="swiper_options.navigation"
        >
            <SwiperSlide v-for="(item, index) in imgs" :key="index">
                <img :src="item.imgSrc" alt />
            </SwiperSlide>

            <div class="swiper-pagination"></div>
            <div class="swiper-button-next swiper-button-white"></div>
            <div class="swiper-button-prev swiper-button-white"></div>
        </Swiper>
    </div>
</template>
<script setup>
import { reactive, onUnmounted } from "vue";
import SwiperCore, { Autoplay, Pagination, Navigation } from "swiper";
import { Swiper, SwiperSlide } from "swiper/vue";

//swiper样式引入（详见https://swiperjs.com/migration-guide 中关于swiper7的说明）
import "swiper/swiper.less";
import "swiper/components/navigation/navigation.less"
import "swiper/components/pagination/pagination.less"

//使用SwiperCore注入才能使用swiper中的额外功能比如分页器
SwiperCore.use([Autoplay, Pagination, Navigation]);

const props = defineProps({

    imgs: {
        type: Array,
        default() {
            return [];
        },
    },
    slideStyle: {
        type: Object,
        default() {
            return {};
        },
    },
});

const paginationRender = function (swiper, current, total) {
    const { desc, redirectTo } = props.imgs[current - 1]
    console.log(props.imgs)
    return `<div class="custom-pagination" style="
                display:flex;
                justify-content:space-between;
                width:100%;
                height:50px;
                background-image: linear-gradient(rgba(255,255,255,0),black );">
                <div style="margin:15px;
                    ">
                    <a href="${redirectTo}" style="
                        width: 400px;
                        white-space: nowrap;
                        overflow: hidden;
                        text-overflow: ellipsis;            
                        display: block;color:white;
                        text-align:left;
                    ">${desc}</a>
                </div>
                <div style="margin:15px;color:white;display:flex;width:50px;justify-content:space-around;align-items: center;">
                    ${
                        props.imgs.map((item,index) => {
                            return index === current - 1 ? 
                            `<div style="background-color:#007aff;width:10px;height:10px"></div>` :
                            `<div style="background-color:white;width:10px;height:10px"></div>`
                        }).join("")
                    }
                </div>
          </div>`;
}

// swiper相关配置属性放在swiper_options这个变量里
const swiper_options = reactive({
    autoplay: {
        disableOnInteraction: false, // 鼠标滑动后继续自动播放
        delay: 4000, // 4秒切换一次
    },
    autoplay:false,
    speed: 500, //切换过渡速度
    loop: true,
    pagination: {
        el: ".swiper-pagination",
        type: 'custom',
        renderCustom: paginationRender
    },
    navigation: {
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev',
    },
});

</script>
<style lang="less" scoped>
img {
    width: 100%;
    height: 100%;
}
.swiper-pagination-custom {
    bottom: 1px;
}
</style>

