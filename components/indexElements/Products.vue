<template>
    <main>
        <mainFilter :goodProducts="goodProducts" @sort="setData" />

        <productsList @goodProducts="setProducts" :sort="sort" />
    </main>
</template>

<script>
import mainFilter from '@/components/indexElements/MainFilter'
import productsList from '@/components/indexElements/ProductsList'

export default {
    components: { mainFilter, productsList },

    data() {
        return {
            // props с данными о сортировки, получаем из компонента MainFilter
            sort: {},
            // принимаем $emit из компонента ProductsList и присваиваем сюда отсортированный товар
            goodProducts: 0,
        }
    },

    methods: {
        /**
         * @method
         * Вызывается из слушателя события, который вызывает $emit из компонента ProductsList в момент сортировки товара.
         * Присваиваем актуальный массив товаров в data goodProducts.
         * 
         * @Array data - принимаемый массив товаров.
         * @Array goodProducts - массив в data, куда записываем полученные данные.
         */
        setProducts(data) {
            this.goodProducts = data
        },

        /**
         * @method
         * Принимаем объект сортировки из компонента mainFilter и присваиваем его в Data.
         * Вызывает в момент работы $emit 
         */
        setData(sort) {
            this.sort = sort
        }
    }
}
</script>

<style lang="scss">
main {
    margin-top: 35px;
}
</style>