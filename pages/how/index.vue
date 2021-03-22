<template>
    <div class="wrapper block">
        <div class="breadcrumps">
            <span class="crumps-main">
                <nuxt-link to="/">Главная</nuxt-link>
            </span>
            <span class="breadcrumps-lic"></span>
            <span class="crumps-dop">Инструкция по покупке</span>
        </div>

        <div class="wrapper content page">
            <h1 class="page-title">Инструкция по покупке</h1>

            <div class="page-section" style="display:block;">
                <VueSlickCarousel>
                    <div class="how-slide">
                        <div class="block"></div>
                        <div class="title">Шаг 1</div>
                        <img src="/img/how/1.jpg" alt="Как купить игру шаг 1">
                        <p>Выбираем интересующий Вас товар на главной странице сайта</p>
                    </div>
                    <div class="how-slide">
                        <div class="block"></div>
                        <div class="title">Шаг 2</div>
                        <img src="/img/how/2.jpg" alt="Как купить игру шаг 2">
                        <p>Нажимаем на кнопку «купить игру»‎ на странице выбранного товара</p>
                    </div>
                    <div class="how-slide">
                        <div class="block"></div>
                        <div class="title">Шаг 3</div>
                        <img src="/img/how/3.jpg" alt="Как купить игру шаг 3">
                        <p>Выбираем удобный для Вас способ оплаты товара</p>
                    </div>
                    <div class="how-slide">
                        <div class="block"></div>
                        <div class="title">Шаг 4</div>
                        <img src="/img/how/4.jpg" alt="Как купить игру шаг 4">
                        <p>Получаете купленный Вами товар</p>
                    </div>
                    <div class="how-slide">
                        <div class="block"></div>
                        <div class="title">Шаг 5</div>
                        <img src="/img/how/5.jpg" alt="Как купить игру шаг 5">
                        <p>После поставленного положительного отзыва получаете <a href="/stock"></a> </p>
                    </div>
                </VueSlickCarousel>
            </div>
        </div>
    </div>  
</template>

<script>
import VueSlickCarousel from 'vue-slick-carousel'
import '@/node_modules/vue-slick-carousel/dist/vue-slick-carousel.css'
import '@/node_modules/vue-slick-carousel/dist/vue-slick-carousel-theme.css'

export default {
    components: { VueSlickCarousel }
}
</script>

<style lang="scss">
    .how-slide {
        position: relative;

        .block {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .title {
            font-size: 24px;
            font-weight: 500;
            text-align: center;
        }

        img {
            width: 100%;
        }

        p {
            font-size: 14px;
            font-weight: 400;
            text-align: center;
            
            a {
                display: inline-block;
                font-size: 14px;
                font-weight: 500;
                text-align: center;
                color: #ff0000;
                transition: all .3s ease;

                &:hover {
                    text-decoration: underline;
                }
            }
        }
    }
    .page-section .slick-prev,
    .page-section .slick-next {
        font-size: 0;
        line-height: 0;
        position: absolute;
        bottom: 5px;
        z-index: 50;
        display: block;
        width: 17px;
        height: 17px;
        padding: 0;
        transform: translate(0, -50%);
        cursor: pointer;
        color: transparent;
        border: none;
        outline: none;
        background: transparent;
        top: 0!important;
        bottom: 0!important;
        margin: auto!important;
    }
    .page-section .slick-next {
        right: 0!important;
        bottom: -25px!important;

    }
    .page-section .slick-next::before,
    .page-section .slick-prev::before {
        font-size: 40px !important;
        color: #989898 !important;
    }
    .page-section .slick-prev {
        bottom: -25px!important;
    }
</style>