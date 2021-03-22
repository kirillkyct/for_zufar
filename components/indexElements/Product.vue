<template>
    <nuxt-link :to="/goods/ + item.id" class="product">
        <div class="status" 
            :class="{
                'new': item.status === 'новинка',
                'hit': item.status === 'хит',
                'popular': item.status === 'популярно'
            }"
        >{{ ucString(item.status) }}</div>

        <div class="product-img" :style="{backgroundImage: 'url(' + item.img + ')'}">
            <div class="product-main">
                <div class="product-title">{{ item.title }}</div>
                <div class="product-platform">
                    <img :src="'/img/icons/' + item.platform + '.png'" :alt="item.platform">
                    {{ ucString(item.typeRu) }} {{ ucString(item.platform) }}
                </div>
            </div>
        </div>

        <div class="product-info">
            <div class="product-small-price"> -{{ item.discount() }}% </div>
            <div class="product-small-price black"> {{ item.oldPrice }}₽ </div>
            <div class="product-big-price"> {{ item.price }}₽ </div>
        </div>
    </nuxt-link>
</template>

<script>
export default {
    props: {
        item: {
            type: Object,
            required: true
        }
    },
    computed: {
        
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
    }
}
</script>

<style lang="scss">
    .products {

        .product {
            height: 317px;
            background: #fff;
            border-radius: 8px;
            box-shadow: 0 20px 51px rgba(0,0,0,.04);
            display: flex;
            width: calc(16.666666666666667% - 16px);
            flex-direction: column;
            justify-content: flex-start;
            align-items: center;
            position: relative;
            margin: 20px 8px 0;
            transition: all .35s cubic-bezier(0.595, 0.03, 0, 0.88);
            overflow: hidden;

            &:hover {
                margin-top: 14px;
                box-shadow: 0 20px 51px rgba(0,0,0,.065);
            }

            .status {
                position: absolute;
                top: 10px;
                left: 0;
                right: 0;
                display: block;
                text-align: center;
                color: #fff;
                font-size: 10px;
                height: 25px;
                line-height: 26px;
                width: 85px;
                margin: auto;
                border-radius: 6px;
                font-weight: 500;
                z-index: 1;

                &.new {
                    background: #ff0000;
                }

                &.hit {
                    background: #73cc31;
                }

                &.popular {
                    background: #41b5ff;
                }
            }

            .product-img {
                overflow: hidden;
                display: block;
                background-size: cover;
                position: relative;
                height: 450px;
                background-position: center center;
                background-repeat: no-repeat;
                width: 100%;

                .product-main {
                    position: absolute;
                    bottom: 13px;
                    width: 100%;

                    .product-title {
                        font-size: 12px;
                        color: #fff;
                        font-weight: 500;
                        line-height: 12px;
                        text-align: center;
                        padding: 0 10px;
                        text-shadow: 0 0 4px rgba(0,0,0,0.8);
                    }

                    .product-platform {
                        font-size: 10px;
                        color: rgba(255, 255, 255, 0.6);
                        font-weight: 400;
                        margin-top: 12px;
                        line-height: 15px;
                        display: flex;
                        justify-content: center;

                        img {
                            max-height: 15px;
                            margin-right: 3px;
                        }
                    }
                }
            }

            .product-info {
                margin-top: 10px;
                margin-bottom: 10px;
                display: flex;
                justify-content: center;

                .product-small-price {
                    font-size: 11px;
                    color: #fff;
                    font-weight: 400;
                    text-transform: uppercase;
                    padding: 7px 4px;
                    border-radius: 8px;
                    background: #ff9000;
                    margin-right: 10px;

                    &.black {
                        line-height: 25px;
                        font-weight: 500;
                        color: #000;
                        text-decoration: line-through;
                        background: none;
                        padding: 0;
                        margin-right: 10px;
                    }
                }

                .product-big-price {
                    font-size: 19px;
                    color: #ff0000;
                    font-weight: 600;
                    text-transform: uppercase;
                    line-height: 25px;
                }
            }
        }
    }
</style>