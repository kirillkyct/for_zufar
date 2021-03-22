<template>
    <div class="sliders">
        <div class="sliders-wrapper">
            <nuxt-link to="/stock" class="banner">
                <img class="banner-ava" src="/img/ava.png" alt="Страшилки от Дядюшки">
                <div class="priz">
                    <img class="banner-priz" src="/img/priz-bg.png" alt="Подарок в магазине Дядюшки">
                    <p>Забрать подарок</p>
                </div>
            </nuxt-link>

            <div class="slider">
                <!-- Компонент слайдера -->
                <VueSlickCarousel v-bind="sliderSettings">
                    <div @mousedown="sliderClick" @click="sliderRoute(slide.url) " class="slide-link" v-for="(slide, index) in sliders" :key="index">
                        <div class="block"></div>

                        <div class="slider-info">
                            <div class="slider-info-wrapper">
                                <div class="slider-name">{{ slide.title }}</div>
                                <div class="slider-price">{{ slide.price }}₽</div>
                            </div>
                        </div>

                        <img :src="slide.img" alt="slide.title">
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
    components: { VueSlickCarousel },

    methods: {
        /**
         * @number event.clientX - Координаты отпускания кнопки мыши по оси X
         * @number event.clientY - Координаты отпускания кнопки мыши по оси Y
         * @number this.slideClientX - Координаты клика по оси X
         * @number this.slideClientY - Координаты клика по оси Y
         * 
         * 
         * @info
         * Вызывается в момент отпускания кнопки мыши на слайдере.
         * Внутри метода осуществляется проверка на то, равны ли координаты мыши в момент клика (вычисляются внутри метода sliderClick) 
         * и в момента отпускания кнопки мыши.
         * Если равны, был клик, происходит смена роута.
         * Иначе была попытка двигать слайдер и ничего не происходит.
         */
        sliderRoute(url){
            if(event.clientX == this.slideClientX && this.slideClientY == event.clientY) this.$router.push(url)
        },

        /**
         * @number this.slideClientX - Свойство, куда записывается координаты мыши в момент клика по слайдеру по оси X
         * @number this.slideClientY - Свойство, куда записывается координаты мыши в момент клика по слайдеру по оси Y
         * @number event.clientX - координаты мыши в момент клика по слайдеру по оси X
         * @number event.clientY - координаты мыши в момент клика по слайдеру по оси Y
         * 
         * @info
         * Вызывается в момент клика по слайдеру.
         * Записываем в свойства данные о клике на слайдер для будущего сравнения, это попытка перейти по товару или двинуть слайдер.
         */
        sliderClick() {
            this.slideClientX = event.clientX
            this.slideClientY = event.clientY
        }
    },

    data() {
        return {
            // Свойства для записи координат мыши в момент клика по слайдеру
            //      для определения нужна ли смена роута.
            slideClientX: '',
            slideClientY: '',

            // Конфиг слайдера
            sliderSettings: {
                "infinite": true,
                "slidesToShow": 1,
                "speed": 500,
                "rows": 2,
                "slidesPerRow": 1,
                "dots": true,
                "arrows": true,
                // "autoplay": true,
                "autoplaySpeed": 5000,
                "pauseOnDotsHover": true,
                "pauseOnFocus": true,
                "pauseOnHover": true,
                "touchThreshold": 5,
                "slidesToScroll": 1,
            },

            // Товары слайдера
            sliders: [
                { title: 'Rocket League', price: 99, url: '/goods/1', img: '/img/slider.jpg' },
                { title: 'Rocket League', price: 99, url: '/goods/2', img: '/img/slider.jpg' },
                { title: 'Rocket League', price: 99, url: '/goods/3', img: '/img/slider.jpg' },
                { title: 'Rocket League', price: 99, url: '/goods/4', img: '/img/slider.jpg' },
                { title: 'Rocket League', price: 99, url: '/goods/5', img: '/img/slider.jpg' },
                { title: 'Rocket League', price: 99, url: '/goods/6', img: '/img/slider.jpg' },
            ]
        }
    }
}
</script>

<style lang="scss">
.slick-dots li.slick-active button::before,
.slick-dots li button::before,
.slick-prev::before,
.slick-next::before {
    color: red;
}
.slick-prev,
.slick-next {
    top: auto;
    bottom: -35px;
    z-index: 1;
}
.slick-prev {
    left: 0;
}
.slick-next {
    right: 0;
}

.sliders-wrapper {
    display: flex;
    justify-content: space-between;
    border-radius: 8px;
}

.banner {
    width: 785px;
    position: relative;
    background-image: url('/img//banner-full.jpg');
    height: 300px;
    background-size: cover;
    margin-top: 6px;
    border-radius: 8px;

    .banner-ava {
        position: absolute;
        top: 44px;
        left: 79px;
        transition: all 300ms cubic-bezier(0.595, 0.03, 0, 0.88);

        &:hover {
            top: 40px;
        }
    }

    .priz {
        position: absolute;
        right: 141px;
        bottom: 44px;
        transition: all 300ms cubic-bezier(0.595, 0.03, 0, 0.88);

        &:hover {
            bottom: 48px;
        }

        p {
            position: absolute;
            color: #fff;
            font-size: 16px;
            font-weight: 400;
            text-align: center;
            text-transform: uppercase;
            left: 0;
            right: 0;
            bottom: 0;
            margin: auto;
            top: 18px;
        }
    }
}

.slider {
    width: 309px;
    position: relative;

    .slide-link {
        width: 309px;
        height: 144.42px;
        position: relative;
        background: #cacaca;
        box-sizing: border-box;
        margin-top: 6px;
        border-radius: 8px;
        overflow: hidden;
        outline: none;
        cursor: pointer;

        &:hover {
            .block {
                opacity: 0.09;
            }
        }

        .block {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #fff;
            opacity: 0;
            transition: all 400ms cubic-bezier(0.595, 0.03, 0, 0.88);
        }

        img {
            background-size: cover;

            &:hover {
                transition: .9;
            }
        }

        .slider-info {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;

            .slider-info-wrapper {
                display: flex;
                justify-content: space-between;
                width: 100%;
                padding: 5px 10px;
                box-sizing: border-box;
                background: rgba(0, 0, 0, 0.6);

                .slider-name,
                .slider-price {
                    font-size: 14px;
                    font-weight: 600;
                    color: #fff;
                    line-height: 18px;
                }

                .slider-name {
                    font-size: 13px;
                }
            }
        }
    }
}
</style>