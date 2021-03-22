<template>
    <div class="product-slider">
        <VueSlickCarousel v-bind="settings">
            <div class="product-slide">
                <div class="block"></div>
                <img src="/img/4.jpg" alt="">
            </div>
            <div class="product-slide">
                <div class="block"></div>
                <img src="/img/4.jpg" alt="">
            </div>
            <div class="product-slide">
                <div class="block"></div>
                <img src="/img/4.jpg" alt="">
            </div>
            <div class="product-slide">
                <div class="block"></div>
                <img src="/img/4.jpg" alt="">
            </div>
            <div class="product-slide">
                <div class="block"></div>
                <img src="/img/4.jpg" alt="">
            </div>
            <div class="product-slide">
                <div class="block"></div>
                <img src="/img/4.jpg" alt="">
            </div>
        </VueSlickCarousel>
    </div>
</template>

<script>
import VueSlickCarousel from 'vue-slick-carousel'
import '@/node_modules/vue-slick-carousel/dist/vue-slick-carousel.css'
import '@/node_modules/vue-slick-carousel/dist/vue-slick-carousel-theme.css'

export default {
    components: { VueSlickCarousel },

    data() {
        return {
            settings: {
                "arrows": false,
                "dots": false,
                "infinite": true,
                "initialSlide": 2,
                "speed": 500,
                "slidesToShow": 3,
                "slidesToScroll": 1,
                "swipeToSlide": true
            },
        }
    },
}
</script>

<style lang="scss">
    .product-slider {
        margin-top: 25px;
        width: 100%;
        position: relative;

        .block {
            width: 100%;
            height: 100%;
            position: absolute;
            top: 0;
            left: 0;
        }

        img {
            width: 100%;
        }

        .product-slide {
            width: 309px;
            height: 144.42px;
            position: relative;
            box-sizing: border-box;
            margin-top: 6px;
            overflow: hidden;
            outline: none;
            cursor: pointer;

            // img {
            //     width: 100%;
            // }
        }
    }
</style>