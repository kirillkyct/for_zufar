<template>
    <div class="wrapper content" style="min-heigth: 353px;">
        <div class="products">
            <product v-for="item in goodProducts" :key="item.id" :item="item" />
        </div>

        <div v-if="!goodProducts.length" class="error">
            Ничего не найдено
        </div>

        <div v-if="goodProducts.length" class="all-products-btn">Показать еще</div>
    </div>
</template>

<script>
import product from '~/components/indexElements/Product'

export default {
    components: { product },

    computed: {
        /**
         * @computed
         * Вычисляемый список актуальноых товаров.
         * Пробегается циклом по всем товаром и отбирает на соответствие заданным пользователем фильтрам.
         * 
         * @Array products - товары для отображения на странице.
         * @Boolean status - статус соответствия фильтрам конкретного товара.
         * @Object sort - параметры сортировки.
         * 
         * @emit goodsProducts - отправка количества подходящих товаров.
         * @Number products.length - количество подходящих товаров.
         * 
         */
        goodProducts() {
            let products = [];
            this.products.find(el => {
                // есть фильтр по платформе
                let status = true
                if(this.sort.platform && el.platform !== this.sort.platform) status = false
                if(this.sort.genre && el.genre !== this.sort.genre) status = false
                if(this.sort.category && el.type !== this.sort.category) status = false

                if(status) products.push(el)
            })
            
            this.$emit('goodProducts', products.length)
            return products;
        }
    },
    
    props: {
        sort: {
            type: Object,
            required: true
        }
    },

     asyncData({ $axios }) {
        // const ip = await $axios.$get('/dz/products.json')
        // // return { ip }
        // console.log(ip)
        console.log($axios)
    },


    data() {
        return {
            products: []
        }
    }
}
</script>

<style lang="scss">
    .products {
        display: flex;
        justify-content: flex-start;
        flex-wrap: wrap;
        width: 100%;
        box-sizing: border-box;
        transition: all .3s cubic-bezier(0.595, 0.03, 0, 0.88);
        opacity: 1;
    }
    .all-products-btn {
        width: 100%;
        text-align: center;
        margin: 30px 8px 0;
        background: #eff3f6;
        color: #bfc4c8;
        font-size: 16px;
        font-weight: 400;
        padding: 22px;
        box-sizing: border-box;
        cursor: pointer;
        border-radius: 8px;
    }
</style>