<template>
    <div class="wrapper block">
        <div class="breadcrumps">
            <span class="crumps-main">
                <nuxt-link to="/">Главная</nuxt-link>
            </span>
            <span class="breadcrumps-lic"></span>
            <span class="crumps-dop">Гарантии</span>
        </div>

        <div class="wrapper content page">
            <h1 class="page-title">Гарантии</h1>

            <section class="page-section">
                <div class="garant-block">
                    <div class="garant-img">
                        <img src="/img/garant/1.png" alt="Магазин блогера">
                    </div>

                    <div class="block-title">
                        Магазин блогера
                    </div>

                    <p>Магазин принадлежит известному ютуберу с большой аудиторией.</p>
                </div>

                <div class="garant-block">
                    <div class="garant-img">
                        <img src="/img/garant/2.png" alt="Магазин блогера">
                    </div>

                    <div class="block-title">
                        Способы оплаты
                    </div>

                    <p>Вы можете оплатить покупку любым удобным способом: Банковская карта, Электронные деньги т.д.</p>
                </div>

                <div class="garant-block">
                    <div class="garant-img">
                        <img src="/img/garant/3.png" alt="Магазин блогера">
                    </div>

                    <div class="block-title">
                        Поддержка
                    </div>

                    <p>При возникновении любых затруднений обращайтесь в службу поддержки.</p>
                </div>

                <div class="garant-block">
                    <div class="garant-img">
                        <img src="/img/garant/4.png" alt="Магазин блогера">
                    </div>

                    <div class="block-title">
                        Гарантия на товар
                    </div>

                    <p>Покупая в нашем магазине, Вы можете быть уверены в работоспособности товара. Весь товар проходит проверку.</p>
                </div>

                <div class="garant-block">
                    <div class="garant-img">
                        <img src="/img/garant/5.png" alt="Магазин блогера">
                    </div>

                    <div class="block-title">
                        Подарок за покупку
                    </div>

                    <p>У нас никто не остаётся без подарка после покупки. За все время выдано уже более 200 000 подарков.</p>
                </div>

                <div class="garant-block">
                    <div class="garant-img">
                        <img src="/img/garant/6.png" alt="Магазин блогера">
                    </div>

                    <div class="block-title">
                        Моментальная доставка
                    </div>

                    <p>После оплаты вы моментально получаете товар, забрать вы сможете его в своем личном кабинете на сайте.</p>
                </div>
            </section>
        </div>
    </div>  
</template>

<style lang="scss" scoped>
    .garant-block {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: center;
        position: relative;
        width: calc(31.761%);
        margin-right: 25px;
        height: 340px;
        border-radius: 8px;
        box-shadow: 0 20px 51px rgba(0,0,0,.03);
        transition: all .3s ease;
        background: #fff;
        box-sizing: border-box;
        padding: 50px 10px;
        margin-bottom: 35px;
        cursor: pointer;
        overflow: hidden;

        &:nth-child(3n) {
            margin-right: 0;
        }

        &:hover {
            margin-top: -5px;
            box-shadow: 0 20px 51px rgba(0,0,0,.065);
        }

        .garant-img {
            width: 65px;
            height: 65px;
            border: 2px solid #f0f4f7;
            border-radius: 45px;
            box-sizing: border-box;
            position: relative;

            img {
                width: 25px;
                margin: auto;
                position: absolute;
                top: 0;
                bottom: 0;
                left: 0;
                right: 0;
            }
        }

        .block-title {
            font-weight: 800;
            text-align: center;
            font-size: 18px;
            margin-top: 35px;
        }

        p {
            margin-top: 35px;
            text-align: center;
            color: #939a9f;
            font-size: 14px;
            font-weight: 400;
            padding: 0 40px;
        }
    }
</style>