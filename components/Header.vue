<template>
    <header :class="{'hide': headerHide}">
        <div class="wrapper">
            <section>
                <!-- Логотип -->
                <div class="logo">
                    <nuxt-link to="/" class="logo-ava"></nuxt-link>
                    <div class="logo-text">
                        <div class="text">
                            <div class="first">Страшилки от Дядюшки <img src="/img/logo-part.png"></div>
                            <div class="second">horror-shop.ru</div>
                        </div>
                    </div>
                </div>

                <!-- Навигация -->
                <nav class="main-nav">
                    <ul>
                        <nuxt-link v-for="(link, index) in links" :key="index" :to="link.href" class="nav-link">
                            <img :src="link.img" :alt="link.title" class="nav-img">
                            <li class="nav-li">{{ link.title }}</li>
                        </nuxt-link>
                    </ul>
                </nav>

                <!-- Мои покупки -->
                <a href="#" target="_blank" class="buy-btn">мои покупки</a>
            </section>
        </div>
    </header>
</template>

<script>
import navImgHome from "@/assets/img/home.png"
import navImgGuarantee from "@/assets/img/garant.png"
import navImgHow from "@/assets/img/how.png"
import navImgContacts from "@/assets/img/contacts.png"


export default {
    mounted() {
        // вызов метода отслеживания скролла после отрисовки DOM дерева
        this.scrollListener();
    },
    data() {
        return {
            // состояние скрытия шапки
            headerHide: false,
            // актуальное значение скролла вниз
            actualScroll: 0,

            // массив кнопок навигации шапки
            links: [
                { title: 'Главная', href: '/', img: navImgHome },
                { title: 'Гарантии', href: '/guarantee', img: navImgGuarantee },
                { title: 'Как купить', href: '/how', img: navImgHow },
                { title: 'Контакты', href: '/contacts', img: navImgContacts },
            ],
        }
    },

    methods: {
        /**
         * @method
         * Отслеживание скролла для скрытия или показа шапки.
         * 
         * @event scroll - событие скрола
         * 
         * @number document.documentElement.scrollTop - Значение скрола вниз
         * @number this.actualScroll - сохраненное значение скрола
         * @number this.headerHide - состояние скрытия шапки
         * 
         * @info
         * Если новое значение скролла вниз больше последнего сохраненного, значит прокрутка идет вниз, скрываем шапку.
         * Иначе прокрутка идет наверх, возвращаем шапку на место.
         * В конце перезаписываем новое состояние скролла.
         */
        scrollListener() {
            window.addEventListener('scroll', e => {
                if(document.documentElement.scrollTop > this.actualScroll) this.headerHide = true
                else this.headerHide = false
                this.actualScroll = document.documentElement.scrollTop
            });
        }
    }
}
</script>

<style lang="scss">
    header {
        max-height: 115px;
        transition: all 550ms cubic-bezier(0.595, 0.03, 0, 0.88);
        z-index: 100;
        position: fixed;
        width: 100%;
        top: 0;

        &.hide {
            transform: translateY(-100%);
        }

        .wrapper {
            background: #fff;
            box-sizing: border-box;
            border-radius: 8px;
            box-shadow: 0 20px 51px rgba(0,0,0,.03);
            width: 100%;

            section {
                width: 1140px;
                box-sizing: border-box;
                padding: 0 15px;
                margin: 0 auto;
                display: flex;
                justify-content: space-between;
                height: inherit;
                overflow: hidden;

                .logo {
                    display: flex;
                    justify-content: left;
                    margin: 29px 0;

                    .logo-ava {
                        background: url("/img/logo.png") no-repeat center center;
                        width: 40px;
                        height: 40px;
                        -webkit-transition: all .2s ease;
                        -moz-transition: all .2s ease;
                        -ms-transition: all .2s ease;
                        -o-transition: all .2s ease;
                        transition: all .2s ease;
                        margin-right: 13px;
                        transition: all 300ms cubic-bezier(0.595, 0.03, 0, 0.88);

                        &:hover {
                            opacity: .9;
                        }
                    }

                    .logo-text {
                        box-sizing: border-box;
                        position: relative;

                        .text {
                            margin-top: 3.8px;
                        }

                        .first {
                            display: flex;

                            img {
                                margin-left: 5px;
                                margin-top: -2px;
                                width: 12px;
                                height: 19px;
                            }
                        }

                        .second {
                            color: #606060;
                            font-size: 11px;
                            font-weight: 400;
                            text-transform: uppercase;
                        }
                    }
                }

                .main-nav {

                    ul {
                        height: 100%;
                        display: flex;

                        .nav-link {
                            position: relative;
                            margin-right: 53px;
                            line-height: 101px;
                            display: flex;
                            align-items: center;

                            &:last-child {
                                margin-right: 0;
                            }

                            &::after {
                                content: '';
                                display: block;
                                position: absolute;
                                left: 0;
                                bottom: 0;
                                opacity: 0;
                                height: 2px;
                                background: #ff0000;
                                width: 100%;
                                transition: all 400ms cubic-bezier(0.595, 0.03, 0, 0.88);
                            }

                            &::before {
                                content: '';
                                display: block;
                                background: url("@/assets/img/pic.png") no-repeat center center;
                                width: 3px;
                                height: 8px;
                                position: absolute;
                                top: 50%;
                                right: -28px;
                                margin-top: -6px;
                                cursor: auto;
                            }

                            &:last-child::before {
                                display: none;
                            }

                            &:hover,
                            &.nuxt-link-exact-active {
                                &::after {
                                    bottom: 0;
                                    opacity: 1;
                                }
                                img {
                                    filter: grayscale(0) !important;
                                }

                                .nav-li {
                                    color: #ff0000;
                                }
                            }

                            img {
                                margin-top: -3px;
                                margin-right: 7px;
                                height: inherit;
                                filter: grayscale(1);
                                height: 16px;
                            }

                            .nav-li {
                                font-size: 14px;
                                color: #000;
                                font-weight: 400;
                                text-transform: uppercase;
                                line-height: 16px;
                                display: inline-block;
                            }
                        }
                    }
                }

                .buy-btn {
                    font-size: 12px;
                    color: #fff;
                    box-sizing: border-box;
                    font-weight: 400;
                    text-transform: uppercase;
                    background: #ff0000;
                    border-radius: 8px;
                    box-shadow: 0 20px 51px rgba(0,0,0,.03);
                    display: inline-block;
                    height: 35px;
                    width: 115px;
                    text-align: center;
                    line-height: 38px;
                    margin: 29px 0 29px 0;
                    transition: all .3s cubic-bezier(0.595, 0.03, 0, 0.88);

                    &:hover {
                        background: #da0000;
                    }
                }
            }
        }
    }
</style>