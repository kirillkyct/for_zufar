<template>
    <div>
        <h1>Все игры</h1>

        <div class="games-list">
            <ul>
                <li v-for="game in games" :key="game.id">
                    <p>{{ game.title }}</p>
                    <p>{{ game.price }}Р</p>
                    <nuxt-link :to="/goods/ + game.id"> Купить </nuxt-link>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            games: [
                { title: 'Кс ГО', price: 89, id: 1 },
                { title: 'Гта 5', price: 149, id: 2 },
                { title: 'Овервотч', price: 199, id: 3 },
            ]
        }
    }
}
</script>
<style lang="scss" scoped>
    .games-list {

        ul {
            display: flex;
            justify-content: space-between;
            margin: 0;
            padding: 0;
        }
    }
    li {
        width: 48%;
        margin: 5px 10px;
        min-height: 200px;
        background: #cacaca2d;
        display: block;
        box-sizing: border-box;
    }
</style>