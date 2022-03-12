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

//将props中数据注入windows（主要是因为自定义分页器的渲染器访问不到vue组件实例，这是折中的办法）
//如果一个页面使用多个轮播图组件，这样使用会有问题
window["swiper_data"] = props.imgs

//组件销毁时及时清理掉
onUnmounted(() => {
    delete window["swiper_data"]
})



const paginationRender = function (swiper, current, total) {
    const { desc, redirectTo } = window["swiper_data"][current - 1]

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
                <div style="margin:15px;color:white">
                    第${current}页
                </div>
          </div>`;
}

// swiper相关配置属性放在swiper_options这个变量里
const swiper_options = reactive({
    autoplay: {
        disableOnInteraction: false, // 鼠标滑动后继续自动播放
        delay: 4000, // 4秒切换一次
    },
    speed: 500, //切换过渡速度
    loop: true,
    //   slidesPerView: "auto", //解决最后一张切换到第一张中间的空白
    //   spaceBetween: 0,
    //   coverflowEffect: {
    //     rotate: 0, //slide做3d旋转时Y轴的旋转角度。默认50。
    //     stretch: 0, //每个slide之间的拉伸值（距离），越大slide靠得越紧。 默认0。
    //     depth: 100, //slide的位置深度。值越大z轴距离越远，看起来越小。 默认100。
    //     modifier: 1, //depth和rotate和stretch的倍率，相当于            depth*modifier、rotate*modifier、stretch*modifier，值越大这三个参数的效果越明显。默认1。
    //     // slideShadows: false, //开启slide阴影。默认 true。
    //   },
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

