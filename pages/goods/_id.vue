<template>
    <div>
        <div class="product-img" style="background-image: url('/img/main.jpg');">
            <div class="wrapper">
                <div class="product-brend">
                    <nuxt-link to="/">На главную</nuxt-link>
                    <h1>Купить {{ product.title }}</h1>
                    <div class="product-img-steam"></div>
                </div>
            </div>
        </div>

        <div class="wrapper">
            <main class="product">
                <div class="main-first">
                    <!-- Блок с описанием -->
                    <div class="desc">
                        <div class="title">Описание</div>
                        <p>{{ product.description }}</p>
                    </div>

                    <!-- Блок со слайдером -->
                    <div class="slider-block">
                        <div class="title">Скриншоты</div>
                        <SliderProduct />
                    </div>

                    <!-- Блок с найдом установки -->
                    <div class="guide-block">
                        <div class="title">Инструкция по активации</div>
                        <div class="guide-activate steam" v-if="product.platform === 'steam'">
                            <ul>
                                <li>
                                    <div class="li-number">1</div>
                                    <a href="https://store.steampowered.com/about/Steam?l=russian&amp;ref=dtf.ru">Скачать</a> и установить клиент Steam.
                                </li>

                                <li>
                                    <div class="li-number">2</div>
                                    Войдите в свой аккаунт Steam или зарегистрируйте новый, если у вас его нет.
                                </li>

                                <li>
                                    <div class="li-number">3</div>
                                    Введите ключ активации.
                                </li>

                                <li>
                                    <div class="li-number last">4</div>
                                   Устанавливайте игру и играйте!
                                </li>
                            </ul>
                        </div>
                    </div>

                    <div class="chance-block">
                        Шансы выигрыша 60%
                    </div>
                </div>

                
                <div class="main-second">
                    <!-- Блок с покупкой -->
                    <div class="buy-block content">
                        <div class="price-buy">
                            <div class="right-line-price">
                                <div class="line-discount">-{{ product.discount() }}%</div>
                                <div class="line-price-block">
                                    <div class="line-old-price">{{ product.oldPrice }}₽</div>
                                    <div class="line-price">{{ product.price }}₽</div>
                                </div>
                            </div>

                            <nuxt-link to="?buy" class="buy-product">купить игру</nuxt-link>

                            <ul>
                                <li>
                                    <div class="buy-imgs-block">
                                        <img src="/img/buy-1.png" alt="Игра в наличии">
                                    </div>
                                    Игра в наличии
                                </li>
                                <li>
                                    <div class="buy-imgs-block">
                                        <img src="/img/buy-2.png" alt="Игра в наличии">
                                    </div>
                                    Моментальная доставка 
                                </li>
                                <li>
                                    <div class="buy-imgs-block">
                                        <img src="/img/buy-3.png" alt="Игра в наличии">
                                    </div>
                                    100% гарантия 
                                </li>
                            </ul>
                        </div>
                    </div>

                    <div class="info-block content">
                        <table>
                            <tbody>
                                <tr>
                                    <td>Активация</td>
                                    <td>{{ ucString(product.platform) }}</td>
                                </tr>
                                <tr>
                                    <td>Платформа</td>
                                    <td>{{ ucString(product.os) }}</td>
                                </tr>
                                <tr>
                                    <td>Язык</td>
                                    <td>{{ ucString(product.lang) }}</td>
                                </tr>
                                <tr>
                                    <td>Регион</td>
                                    <td>{{ ucString(product.region) }}</td>
                                </tr>
                                <tr>
                                    <td>Тип товара</td>
                                    <td>{{ ucString(product.type) }}</td>
                                </tr>
                                <tr>
                                    <td>Гарантия</td>
                                    <td>100%</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                    <div class="system-block content">
                        <div class="title">Системные требования</div>

                        <ul>
                            <li>{{ product.system }}</li>
                            <li>{{ product.cpu }}</li>
                            <li>{{ product.ram }}</li>
                            <li>{{ product.video }}</li>
                            <li>{{ product.directx }}</li>
                            <li>{{ product.hard }}</li>
                        </ul>
                    </div>
                </div>
            </main>
        </div>
    </div>
</template>

<script>
import SliderProduct from '@/components/productElements/SliderProduct'

export default {
    components: { SliderProduct },

    /**
     * проверка на число
     * validate() должен возвращать true, иначе ошибка
     */
    validate({ params }) {
        return /^\d+$/.test(params.id)
    },

    methods: {
        /**
         * @method
         * 
         * Принимает строку и возвращает ее с заглавной буквы.
         */
        ucString(string) {
            return string[0].toUpperCase() + string.slice(1);
        }
    },

    data() {
        return {
            product: {
                id: 2,
                title: 'Cyberpunk 2077',
                platform: 'steam', 
                price: 149, 
                oldPrice: 1999, 
                discount() {
                    return Math.floor(100 - (this.price / (this.oldPrice / 100)))
                },
                img: '/img/main.jpg',
                type: 'ключ',
                description: 'Cyberpunk 2077 — приключенческая ролевая игра, действие которой происходит в мегаполисе Найт-Сити, где власть, роскошь и модификации тела ценятся выше всего. Вы играете за V, наёмника в поисках устройства, позволяющ...',
                lang: 'русский',
                region: 'RU + СНГ',
                system: 'Windows 10 64bit only',
                cpu: 'AMD FX-8310',
                ram: '8 GB',
                video: 'NVIDIA GeForce GTX 780 or AMD Radeon RX 470',
                directx: 'DerectX Версии 11.0c',
                hard: '70GB',
                os: 'windows'
            }
        }
    },
}
</script>

<style lang="scss">
    .main-first {
        width: 73.5%;

        .desc {
            .title {
                font-size: 16px;
                font-weight: 500;
                margin: 0
            }

            p {
                font-size: 13px;
                color: #505050;
                font-weight: 400;
                margin-top: 25px;
                line-height: 18px;
                display: flex;

                &::before {
                    content: '';
                    background: url("/img/info.png") center center no-repeat;
                    width: 24px;
                    height: 24px;
                    min-width: 24px;
                    min-height: 24px;
                    position: relative;
                    float: left;
                    margin-right: 16px;
                }
            }
        }

        .chance-block,
        .slider-block,
        .guide-block {
            box-sizing: border-box;
            display: block;
            margin-top: 20px;
            background: #fff;
            border-radius: 8px;
            box-shadow: 0 20px 51px rgba(0,0,0,.03);
            display: flex;
            justify-content: flex-start;
            flex-wrap: wrap;
            padding-bottom: 20px;
            padding-right: 8px;
            padding-left: 8px;
            transition: all .3s ease;

            .title {
                font-size: 16px;
                font-weight: 500;
                margin: 0;
                padding-top: 25px;
                padding-left: 25px;
            }
        }

        .chance-block {
            font-size: 14px;
            color: #cacaca;
            font-weight: 400;
            padding: 25px;
            display: flex;
            justify-content: center;
        }

        .guide-block {
            padding: 25px;
            display: block;

            .guide-activate {
                margin-top: 25px;

                ul {
                    margin: 0;
                    padding: 0;

                    li {
                        margin: 0;
                        padding: 0;
                        list-style-type: none;
                        font-size: 14px;
                        font-weight: 400;
                        display: flex;
                        line-height: 55px;
                        margin-top: 30px;

                        &:first-child {
                            margin-top: 0;
                        }

                        .li-number {
                            box-sizing: border-box;
                            display: inline-block;
                            width: 49px;
                            height: 49px;
                            min-width: 49px;
                            min-height: 49px;
                            border: 3px solid #ff9000;
                            -webkit-border-radius: 50px;
                            -moz-border-radius: 50px;
                            border-radius: 50px;
                            line-height: 49px;
                            text-align: center;
                            margin-right: 15px;
                            color: #ff9000;
                            font-weight: 500;
                            font-size: 18px;
                            position: relative;

                            &.last {
                                background: #ff9000;
                                border: none;
                                color: #fff;

                                &::before {
                                    display: none;
                                }
                            }

                            &::before {
                                content: '';
                                width: 2px;
                                height: 20px;
                                background: #f0f4f7;
                                position: absolute;
                                bottom: -28px;
                                left: 50%;
                                margin-left: -1.5px;
                            }
                        }

                        a {
                            margin-right: 5px;
                            color: #ff9000;
                            font-weight: 400;
                            transition: all .3s ease;

                            &:hover {
                                text-decoration: underline;
                            }
                        }
                    }
                }
            }
        }
    }

    .main-second {
        width: 24%;

        .info-block {
            table {
                text-align: center;
                width: 100%;

                tr {
                    padding-bottom: 8px;
                }

                td {
                    font-size: 13px;
                    font-weight: 400;

                    &:first-child {
                        text-align: right;
                        color: #bdbdbd;
                    }

                    &:last-child {
                        text-align: left;
                        padding-left: 14px;
                        color: #000;
                        font-weight: 500;
                    }
                }
            }
        }

        .system-block {
            .title {
                font-size: 14px;
                font-weight: 500;
                color: #000;
                margin-bottom: 25px;
            }

            ul {
                margin: 0;
                padding: 0;

                li {
                    font-size: 13px;
                    font-weight: 400;
                    color: #bdbdbd;
                    margin-top: 12px;

                    &:first-child {
                        margin-top: 0;
                    }
                }
            }
        }

        .buy-block,
        .info-block,
        .system-block {
            padding: 25px;
        }

        .buy-block {
            
            .price-buy {
                width: 100%;
            }

            .price-buy {

                .right-line-price {
                    display: flex;

                    .line-discount {
                        width: 55px;
                        height: 60px;
                        background: #ff9000;
                        color: #fff;
                        font-size: 11px;
                        font-weight: 500;
                        text-align: center;
                        line-height: 60px;
                        -webkit-border-radius: 8px;
                        -moz-border-radius: 8px;
                        border-radius: 8px;
                        margin-right: 15px;
                    }

                    .line-price-block {
                        padding-top: 5.5px;

                        .line-old-price {
                            color: #bdbdbd;
                            font-size: 12px;
                            text-decoration: line-through;
                        }

                        .line-price {
                            color: #000;
                            font-size: 32px;
                            font-weight: 700;
                            margin-top: 5px;
                        }
                    }
                }

                .buy-product {
                        margin-top: 30px;
                        width: 100%;
                        height: 79px;
                        display: block;
                        background: #ff0000;
                        border-radius: 8px;
                        color: #fff;
                        text-align: center;
                        line-height: 79px;
                        font-size: 12px;
                        font-weight: 400;
                        text-transform: uppercase;
                        transition: all 0.3s cubic-bezier(0.595, 0.03, 0, 0.88);

                        &:hover {
                            background: #da0000;
                        }
                    }

                ul {
                    margin-top: 30px;

                    li {
                        font-size: 13px;
                        color: #d9d9d9;
                        font-weight: 400;
                        margin-top: 5px;
                        line-height: 25px;
                        display: flex;

                        &:first-child {
                            margin-top: 0;
                        }

                        .buy-imgs-block {
                            width: 25px;
                            height: 25px;
                            border-radius: 8px;
                            background: #d9d9d9;
                            display: inline-block;
                            margin-right: 10px;
                            position: relative;

                            img {
                                position: absolute;
                                top: 0;
                                left: 0;
                                right: 0;
                                bottom: 0;
                                margin: auto;
                            }
                        }
                    }
                }
            }
        }
    }

    main.product {
        padding-top: 25px;
        display: flex;
        justify-content: space-between;
        overflow: hidden;
    }
    .wrapper {
        position: relative;
    }
    .product-img {
        overflow: hidden;
        display: block;
        background-size: cover;
        position: relative;
        width: 100%;
        height: 450px;
        background-position: center center;
        background-repeat: no-repeat;

        .product-brend {
            position: absolute;
            bottom: 25px;
            left: 15px;

            a {
                padding-left: 50px;
                position: relative;
                line-height: 14px;
                color: #fff;
                font-size: 15px;
                font-weight: 400;
                filter: progid:DXImageTransform.Microsoft.DropShadow(offX=1, offY=1, color=#000000, positive=true);
                text-shadow: 1px 1px 3px rgba(0,0,0,0.8);
                display: flex;
                align-items: center;

                &:hover::before {
                    left: 22px;
                }

                &::before {
                    content: '';
                    position: absolute;
                    width: 22px;
                    height: 17px;
                    background: url('/img/back.png') center center no-repeat;
                    left: 17px;
                    transition: all .1s ease;
                }
            }

            h1 {
                margin-top: 20px;
                font-size: 48px;
                color: #fff;
                font-weight: 900;
                filter: progid:DXImageTransform.Microsoft.DropShadow(offX=4, offY=4, color=#000000, positive=true);
                text-shadow: 4px 4px 5px rgba(0,0,0,0.5);
            }

            .product-img-steam {
                background: url("/img/steam-product.png");
                width: 116px;
                height: 37px;
                margin-top: 50px;
            }
        }
    }
    
</style>