<template>
    <div class="wrapper">
        <footer>
            <section class="footer-line">
                <div class="footer-block">
                    <div class="footer-title">Способы оплаты</div>
                    <img src="/img/payments.png" alt="Способы оплаты">
                </div>
                <div class="footer-block">
                    <div class="footer-title">Популярные издатели</div>
                    <img src="/img/izdatel.png" alt="Популярные издатели">
                </div>
            </section>
            <section class="footer-line">
                <div class="logo">
                    <nuxt-link to="/" class="logo-ava"></nuxt-link>
                    <div class="logo-font">
                        <div class="title">
                            Страшилки от Дядюшки 
                            <img src="/img/logo-part.png" alt="Страшилки от Дядюшки">
                        </div>
                        <div class="info">
                            Тут Вы можете купить игры для Steam, Origin. В магазине <br />
                            действуют постоянные скидки, конкурсы, специальные предложения.
                        </div>
                    </div>
                </div>

                <nav>
                    <ul>
                        <li v-for="(btn, index) in btns" :key="index">
                            <nuxt-link :to="btn.href"> {{ btn.title }} </nuxt-link>
                        </li>
                    </ul>
                </nav>
            </section>
        </footer>
    </div>
</template>

<script>
export default {
    data() {
        return {
            btns: [
                { title: 'Контакты', href: '/contacts' },
                { title: 'Гарантии', href: '/guarantee' },
                { title: 'Инструкция по покупке', href: '/how' },
                { title: 'Пользовательское соглашение', href: '/rules' },
            ]
        }
    }
}
</script>

<style lang="scss">
    footer {
        margin-top: 30px;
        padding: 20px 0 60px;

        .footer-line {
            display: flex;
            justify-content: space-between;

            &:last-child {
                margin-top: 45px;
            }

            .footer-block {
                .footer-title {
                    font-size: 16px;
                    text-transform: uppercase;
                    color: #000;
                    font-weight: 400;
                    margin-bottom: 25px;
                }

                img {
                    height: 24px;
                }
            }

            .logo {
                display: flex;
                justify-content: left;
                margin: 0;
                align-items: center;

                .logo-ava {
                    background: url("/img/logo.png") no-repeat center center;
                    width: 40px;
                    height: 40px;
                    transition: all .2s ease;
                    margin-right: 13px;

                    &:hover {
                        opacity: .9;
                    }
                }

                .logo-font {
                    .title {
                        margin-bottom: 0px;
                        font-size: 18px;
                        color: #000;
                        font-weight: 400;

                        img {
                            margin-top: -2px;
                        }
                    }

                    .info {
                        color: #606060;
                        font-size: 11px;
                        font-weight: 400;
                    }
                }
            }

            nav {
                display: flex;
                align-items: center;

                ul {
                    margin: 0;
                    padding: 0;

                    li {
                        margin: 0;
                        padding: 0;
                        list-style-type: none;
                        display: inline-block;
                        margin-right: 15px;

                        a {
                            font-size: 13px;
                            color: #000;
                            font-weight: 400;
                            line-height: 40px;
                            transition: all .2s ease;

                            &:hover {
                                opacity: .7;
                            }
                        }
                    }
                }
            }
        }
    }
</style>