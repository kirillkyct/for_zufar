<template>
    <div class="wrapper block">
        <div class="breadcrumps">
            <span class="crumps-main">
                <nuxt-link to="/">Главная</nuxt-link>
            </span>
            <span class="breadcrumps-lic"></span>
            <span class="crumps-dop">Получи подарок</span>
        </div>

        <div class="wrapper content page">
            <h1 class="page-title">Получи два подарка бесплатно!</h1>
            <h2>Уважаемые покупатели, в течение этого месяца Вы можете бесплатно <br /> получить целых 2 подарка от нашего магазина! </h2>

            <div class="page-section" style="display:flex;justify-content:center;">
                <div class="prize-block huarantee-block" style="margin-right: 25px;">
                    <img src="/img/stock/stock-1.jpg" alt="Получи аккаунт Origin в подарок">
                    <div class="title">Аккаунт Origin с играми</div>
                    <p>Возможны такие игры: Battlefield, FIFA, Need For Speed и другие.</p>
                    <div class="title-second">От 2 до 10 игр на аккаунте</div>
                </div>

                <div class="prize-block huarantee-block">
                    <img src="/img/stock/stock-2.jpg" alt="Получи аккаунт Origin в подарок">
                    <div class="title">Ключ от случайной игры Steam</div>
                    <p>Возможны такие игры: CS:GO, Rust, Rocket League и <br /> другие.</p>
                    <div class="title-second">Ценой от 100 Р до 499 Р</div>
                </div>
            </div>
        </div>
    </div>  
</template>

<style lang="scss">
    h2 {
        text-align: center;
        font-size: 16px;
        font-weight: 400;
        color: #939a9f;
        margin-bottom: 45px;
    }

    .prize-block {
        padding: 0 0 20px;
        width: calc(26%);
        height: auto;
        box-shadow: 0 20px 51px rgba(0,0,0,.03);
        transition: all .3s ease;
        cursor: pointer;

        &:hover {
            box-shadow: 0 20px 51px rgba(0,0,0,.065);
        }

        img {
            background-size: cover;
        }

        .title {
            font-weight: 800;
            text-align: center;
            font-size: 18px;
            margin-top: 35px;
            padding: 0 40px;
        }

        p {
            margin-top: 35px;
            text-align: center;
            color: #939a9f;
            font-size: 14px;
            font-weight: 400;
            padding: 0 40px;
        }

        .title-second {
            font-size: 15px;
            font-weight: 700;
            margin-top: 35px;
            text-align: center;
        }
    }
</style>