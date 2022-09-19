<template>
  <div>
    <div>
      <ItemListCheckout
        v-for="(item, i) in listItem"
        :key="item.id + item.order_qty + i"
        :data-item="item"
        :sales-type="salesType"
        :index="i"
        :qty="item.qty"
      />
    </div>
    <div class="flex items-center justify-center h-full">
      <h6>No article selected</h6>
    </div>
  </div>
</template>

<script>
import ItemListCheckout from '@/components/point-of-sales/ItemListCheckout.vue'
export default {
  name: 'ListCheckout',
  components: { ItemListCheckout },
      props: {
        listItem: { type: Array, require: true, default: Array },
    },
}
</script>

<style lang="css" scoped></style>
