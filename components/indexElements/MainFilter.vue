<template>
<div class="filter">
    <div class="filter-btns">
        <!-- Кнопка категорий -->
        <div 
            class="filter-btn" 
            v-for="(btn, index) in catBtns" 
            :key="index" 
            :class="{'active': btn.id == activeBtnCat}"
            @click="btnCatSort(btn.sort, btn.id)"
        >
            <div class="filter-btn-title" :class="{'prize': btn.styled === 'prize'}">{{ btn.title }}</div>
        </div>
    </div>

    <!-- Все кнопки фильтра -->
    <div class="filter-wrapper">
        <div class="filter-line">
            <div class="filter-platforms">
                <div class="title">Фильтр: </div>

                <div 
                    class="filter-platform" 
                    v-for="(btn, index) in platformBtns" 
                    :key="index"
                    :class="{'active': btn.id == activeBtnPlatform}"
                    @click="btnPlatformSort(btn.sort, btn.id)"
                >
                    <img class="filter-img-platform" :src="btn.img" :alt="btn.sort">
                </div>
            </div>

            <div class="filter-line-second">
                <form>
                    <div @click="searchBtn" class="search-btn"></div>
                    <input v-model="searchInput" :class="{'full': visibleSearch}" type="text">
                </form>

                <div class="category-wrapper">
                    <div class="category" :class="{'active': visibleGenres}" @click="genreBtn">
                        <div class="title">{{ ucFirst(genreSort) || 'Все жанры' }}</div>
                        <img src="/img/category-img.png" alt="Все жанры игр">
                    </div>
                    <div class="category-list" :class="{'active': visibleGenres}">
                        <ul>
                            <li @click="btnGenreSort('')">Все жанры</li>
                            <li v-for="(genre, index) in genres" :key="index" @click="btnGenreSort(genre)">{{ genre }}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        <div class="filter-line">
            <div class="text bold">{{ goodProducts }}</div>
            <div class="text bold">найдено</div>

            <div @click="filterReset" class="close">
                <img src="/img/close.png">
                Очистить поиск
            </div>
        </div>
    </div>
</div>
</template>


<script>
// Картинки кнопок сортировки по платформе
import platformImgSteam from '~/assets/img/filter-steam.png'
import platformImgOrigin from '~/assets/img/filter-origin.png'
import platformImgMinecraft from '~/assets/img/filter-minecraft.png'
import platformImgBattlenet from '~/assets/img/filter-battlenet.png'
import platformImgUplay from '~/assets/img/filter-uplay.png'

export default {
    props: {
        // отсортированный список товаров, принимаем из компонента Products
        goodProducts: {
            type: Number,
            required: true
        }
    },
    data() {
        return {
            /**
             * Категории
             */
            // Кнопки сортировки по категориям
            catBtns: [
                { id: 1, title: 'Весь ассортимент', sort: '', styled: '' },
                { id: 2, title: 'Лицензионные ключи', sort: 'keys', styled: '' },
                { id: 3, title: 'Аккаунты', sort: 'accounts', styled: '' },
                { id: 4, title: 'Игровые наборы', sort: 'boxes', styled: 'prize' },
            ],
            // Активная кнопка сортировки категории
            activeBtnCat: 1,
            // Актуальный тип сортировки по категории
            categorySort: '',


            /**
             * Платформа
             */
            // Кнопки сортировки по платформе
            platformBtns: [
                { id: 1, sort: 'steam', img: platformImgSteam },
                { id: 2, sort: 'origin', img: platformImgOrigin },
                { id: 3, sort: 'minecraft', img: platformImgMinecraft },
                { id: 4, sort: 'battle.net', img: platformImgBattlenet },
                { id: 5, sort: 'uplay', img: platformImgUplay },
            ],
            // Активная кнопка сортировки платформе
            activeBtnPlatform: 0,
            // Актуальный тип сортировки по платформе
            platformSort: '',


            /**
             * Поиск
             */
            // Полное отображение поиска
            visibleSearch: false,
            // Вводимый текст в поле поиска
            searchInput: '',

            /**
             * Жанры
             */
            genres: [
                'Симулятор',
                'Экшн',
                'RPG',
                'Приключения',
                'Стратегии',
                'Инди',
            ],
            // Актуальный тип сортировки по жанру
            genreSort: '',
            // Отображение списка жанров
            visibleGenres: false,

            // объект с данными о сортировке
            dataSort: {
                search: '',
                category: '',
                platform: '',
                genre: '',
            }
        }
    },

    created() {
        this.$emit('sort', this.dataSort)
    },

    watch: {
        /**
         * Следим за изменением состояния каждой сортировки и отправляем в компонент выше (Products) все изменения.
         */
        searchInput() {
            this.$emit('sort', this.sortData)
        },
        categorySort() {
            this.$emit('sort', this.sortData)
        },
        platformSort() {
            this.$emit('sort', this.sortData)
        },
        genreSort() {
            this.$emit('sort', this.sortData)
        }
    },
    
    computed: {
        /**
         * @computed
         * Вычисляемое состояние объекта сортировки.
         * Вызывается из watch при каждом изменении любой сортировки.
         */
        sortData() {
            return {
                search: this.searchInput,
                category: this.categorySort,
                platform: this.platformSort,
                genre: this.genreSort
            }
        }
    },

    methods: {
        /**
         * @method
         * Принимает строку, возвращает ее же, но с заглавной буквы.
         */
        ucFirst(str) {
            if (!str) return str;
            return str[0].toUpperCase() + str.slice(1);
        },

        /**
         * @method
         * Вызывается при клике на кнопку категории товаров. Принимается тип сортировки и id кнопки, меняется активная кнопка и тип сортировки.
         * 
         * @string sort - Принимаемый параметр сортировки
         * @number id - Принимаемый параметр с номером кнопки, по которой был клик
         */
        btnCatSort(sort, id) {
            this.activeBtnCat = id
            this.categorySort = sort
        },

        /**
         * @method
         * Вызывается при клике на кнопку платформы. Принимается тип сортировки и id кнопки, меняется активная кнопка и тип сортировки.
         * 
         * @string sort - Принимаемый параметр сортировки
         * @number id - Принимаемый параметр с номером кнопки, по которой был клик
         */
        btnPlatformSort(sort, id) {
            if(this.activeBtnPlatform == id) {
                this.activeBtnPlatform = 0
                this.platformSort = ''
                return
            }

            this.activeBtnPlatform = id
            this.platformSort = sort
        },

        /**
         * @method
         * Вызывается при клике на кнопку поиска. Разворачивает или скрывает поле ввода текста.
         * 
         * @boolean this.visibleSearch - состояние видимости поиска
         */
        searchBtn() {
            this.visibleSearch = !this.visibleSearch
        },

        /**
         * @method
         * Вызывается при клике на кнопку выбора жанра. Разворачивает список всех жанров.
         * 
         * @boolean this.visibleGenres - состояние отображения всех жанров и применение стилей.
         */
        genreBtn() {
            this.visibleGenres = !this.visibleGenres
        },

        /**
         * @method
         * Вызывается при клике на какой-то из жанров. Принимается тип сортировки и меняется на принятый.
         * 
         * @string genre - Принимаемый параметр сортировки
         * @boolean visibleGenres - Отображение списка жанров
         */
        btnGenreSort(genre) {
            this.genreSort = genre.toLowerCase()
            this.visibleGenres = false
        },

        /**
         * @method
         * Сброс всех выбранных фильтров.
         */
        filterReset() {
            this.activeBtnPlatform = 0,
            this.platformSort = ''
            this.visibleSearch = false
            this.searchInput = ''
            this.genreSort = ''
            this.visibleGenres = false
        },
    }
}
</script>

<style lang="scss">
.filter {
    min-height: 165px;
    border-radius: 8px;
    box-shadow: 0 20px 51px rgba(0,0,0,.03);
    padding-bottom: 20px;
    background: #fff;

    .filter-btns {
        display: flex;
        height: 50px;
        width: 100%;
        justify-content: flex-start;
        flex-wrap: wrap;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
        overflow: hidden;

        .filter-btn {
            background: #eff3f6;
            height: 100%;
            display: flex;
            width: calc(100% / 4);
            flex-direction: column;
            justify-content: flex-start;
            align-items: center;
            cursor: pointer;
            transition: all .5s cubic-bezier(0.595, 0.03, 0, 0.88);

            &.active {
                background: #fff;

                .filter-btn-title {
                    color: #000;
                }
            }

            .filter-btn-title {
                display: flex;
                margin-right: 5px;
                font-size: 16px;
                color: #bfc4c8;
                font-weight: 400;
                line-height: 50px;

                &.prize::before {
                    content: '';
                    display: inline-block;
                    width: 22px;
                    height: 50px;
                    background: url("/img/box.png") center center no-repeat;
                        background-size: auto;
                    background-size: contain;
                    margin-right: 5px;
                    transition: all .2s cubic-bezier(0.595, 0.03, 0, 0.88);
                }

                &:hover::before {
                    height: 45px;
                }
            }
        }
    }
    
    .filter-wrapper {
        padding: 0 100px;
        margin-top: 20px;

        .filter-line {
            display: flex;
            justify-content: left;

            .text {
                line-height: 40px;
                margin-right: 5px;

                &.bold {
                    color: #000;
                    font-weight: 800;
                }
            }

            .close {
                margin-left: 10px;
                cursor: pointer;
                line-height: 40px;
                margin-right: 5px;
                display: flex;
                align-items: center;
                transition: all .3s cubic-bezier(0.595, 0.03, 0, 0.88);

                &:hover {
                    img {
                        opacity: .8;
                    }
                }

                img {
                    margin-right: 5px;
                    width: 14px;
                    height: 14px;
                }
            }

            &:last-child {
                margin-top: 20px;
            }

            .filter-platforms {
                display: flex;
                justify-content: left;
                margin-right: 40px;

                .title {
                    line-height: 40px;
                    margin-right: 5px;
                    color: #000;
                }

                .filter-platform {
                    width: 40px;
                    height: 40px;
                    border-radius: 8px;
                    background: #eff3f6;
                    margin-left: 5px;
                    position: relative;
                    cursor: pointer;

                    &.active {
                        img {
                            filter: grayscale(0);
                            opacity: 1;
                        }
                    }

                    &:hover {
                        img {
                            filter: grayscale(0);
                            opacity: 1;
                        }
                    }

                    img {
                        max-width: 20px;
                        max-height: 20px;
                        position: absolute;
                        top: 0;
                        left: 0;
                        right: 0;
                        bottom: 0;
                        margin: auto;
                        filter: grayscale(1);
                        opacity: .3;
                        transition: all .3s cubic-bezier(0.595, 0.03, 0, 0.88);
                    }
                }
            }

            .filter-line-second {
                display: flex;
                justify-content: left;

                form {
                    position: relative;
                    border-radius: 10px;
                    overflow: hidden;
                    min-width: 40px;
                    height: 41px;

                    .search-btn {
                        display: block;
                        width: 38px;
                        height: 41px;
                        position: absolute;
                        top: 50%;
                        right: 0;
                        margin-top: -21px;
                        z-index: 100;
                        background: url("/img/search.png") no-repeat center center #eff3f6;
                        cursor: pointer;
                    }

                    input {
                        width: 30px;
                        height: 41px;
                        border-radius: 8px;
                        background: #eff3f6;
                        border: none;
                        padding-left: 10px;
                        color: #afafaf;
                        position: relative;
                        box-sizing: border-box;
                        transition: all .3s cubic-bezier(0.595, 0.03, 0, 0.88);
                        font-size: 16px;

                        &:focus {
                            outline: none;
                            border: 0;
                        }

                        &.full {
                            width: 210px;
                        }
                    }
                }
                
                .category-wrapper {
                    margin-left: 5px;
                    position: relative;
                    min-width: 140px;

                    .category {
                        width: 162px;
                        box-sizing: border-box;
                        height: 40px;
                        background: #eff3f6;
                        -webkit-border-radius: 5px;
                        -moz-border-radius: 5px;
                        border-radius: 5px;
                        overflow: hidden;
                        cursor: pointer;
                        line-height: 40px;
                        padding-left: 14px;
                        padding-right: 35px;
                        position: relative;
                        z-index: 100;
                        box-shadow: 0 20px 51px rgba(0,0,0,.03);
                        transition: all .3s cubic-bezier(0.595, 0.03, 0, 0.88);

                        &.active {
                            background: #fff;
                        }

                        .title {
                            line-height: 40px;
                            margin-right: 5px;
                            font-size: 16px;
                            color: #bfc4c8;
                            font-weight: 400;
                        }

                        img {
                            position: absolute;
                            top: 50%;
                            margin-top: -4px;
                            right: 10px;
                        }
                    }

                    .category-list {
                        position: absolute;
                        background: #fff;
                        width: 100%;
                        opacity: 0;
                        visibility: hidden;
                        margin-top: -40px;
                        top: 40px;
                        left: 0;
                        border-bottom-left-radius: 8px;
                        border-bottom-right-radius: 8px;
                        -webkit-box-shadow: 0 20px 51px rgba(0,0,0,.03);
                        box-shadow: 0 20px 51px rgba(0,0,0,.03);
                        transition: all .3s cubic-bezier(0.595, 0.03, 0, 0.88);
                        z-index: 2;

                        &.active {
                            visibility: visible;
                            opacity: 1;
                            margin-top: 0;
                        }

                        ul {

                            li {
                                font-size: 16px;
                                color: #bfc4c8;
                                font-weight: 400;
                                cursor: pointer;
                                transition: all .3s cubic-bezier(0.595, 0.03, 0, 0.88);
                                padding-left: 14px;
                                margin-right: 5px;
                                line-height: 40px;

                                &:hover {
                                    color: #93989c;
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
</style>