<template>
    <div class="wrapper block">
        <div class="breadcrumps">
            <span class="crumps-main">
                <nuxt-link to="/">Главная</nuxt-link>
            </span>
            <span class="breadcrumps-lic"></span>
            <span class="crumps-dop">Контакты</span>
        </div>

        <div class="wrapper content page">
            <h1 class="page-title">Контакты</h1>

            <div class="page-section" style="display:flex;justify-content:center;">
                <div class="contacts-block">
                    <div class="contacts-img">
                        <img src="/img/contacts/1.png" alt="Техническая поддержка">
                    </div>
                    <div class="contact-title">
                        Поддержка
                    </div>
                    <p>Возник какой-либо вопрос? <br />Пиши vk.com/support</p>
                </div>

                <div class="contacts-block">
                    <div class="contacts-img">
                        <img src="/img/contacts/2.png" alt="Техническая поддержка">
                    </div>
                    <div class="contact-title">
                        Сотрудничество
                    </div>
                    <p>Хочешь создать крутой проект? Мы сделаем сайт любой сложности vk.com/your_project</p>
                </div>
            </div>
        </div>
    </div>  
</template>

<style lang="scss">
    .contacts-block {
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

        &:hover {
            box-shadow: 0 20px 51px rgba(0,0,0,.065);
        }

        .contacts-img {
            width: 65px;
            height: 65px;
            border: 2px solid #f0f4f7;
            border-radius: 45px;
            box-sizing: border-box;
            position: relative;
            background: rgba(255, 144, 0, 0.8);

            img {
                width: 25px;
                height: 25px;
                margin: auto;
                position: absolute;
                top: 0;
                bottom: 0;
                left: 0;
                right: 0;
            }
        }

        .contact-title {
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