<template>
  <div class="wrapper" style="margin-top:39px;">
    <Sliders />
    <Products />
  </div>
</template>

<script>
import Sliders from '@/components/Sliders'
import Products from '@/components/indexElements/Products'

export default {
  components: { Sliders, Products }
}
</script>