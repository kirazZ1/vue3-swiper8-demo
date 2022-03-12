<!--
 * @Author: your name
 * @Date: 2022-03-12 13:01:48
 * @LastEditTime: 2022-03-12 17:31:09
 * @LastEditors: your name
 * @Description: 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
 * @FilePath: /vue-swiper/README.md
-->
# Vue3整合Swiper8示例

本项目是Vue3整合Swiper8的尝试，看了不少网上的文章，并不都好用。官方文档是英文的，本人英语阅读能力也有限，读了很久文档才写出来这个示例，老笨比了。

在基本能用的基础上自定义了分页器，分页器左侧显示文字链接可以点击跳转，右侧显示页码。

由于Swiper的自定义分页器渲染函数拿不到组件实例中数据，所以在加载组件时把数据注入window对象中，组件销毁时移除。

不过这方法也有局限性，如果在同一页面上使用多个就GG了。
