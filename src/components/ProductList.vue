<template lang="pug">
  .food
    .food-list
      router-link.food-item(v-for="(product, index) in products",
        :key="index",
        :style="`background: url(${product.image}) no-repeat center / cover`",
        :to="`${category}/${product.id}`")
        .food-name
          | {{product.name}}
        .food-price
          input(type="button" class="add-to-card" value="Добавить в Заказ" @click="addItem(product)")

    navigation-component
</template>

<script>
import NavigationComponent from '../components/Navigation';

export default {
  name: 'ProductList',
  data () {
    return {
      menu: this.$root.$options.menu
    }
  },

  computed: {
    section() {
      return this.$route.params.sectionId
    },
    category() {
      return this.$route.params.categoryId
    },
    categories() {
      return this.menu.find(e => e.id === this.section).categories
    },
    products() {
      return this.categories.find(e => e.id === this.category).products
    },
    store() {
      return this.$store
    }
  },

  methods: {
    addItem: function(product) {
      event.preventDefault();
      this.store.commit({type: 'addProduct', product: product})
    }
  },

  components: {
    NavigationComponent
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss" rel="stylesheet/scss">

/* This stylesheet generated by Transfonter (https://transfonter.org) on February 27, 2017 7:39 PM */


.food {
  padding-top: 20px;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-between;

  &-list {
    display: flex;
    width: 80%;
    flex-flow: row wrap;
    justify-content: flex-start;
    align-items: flex-start;
    align-content: flex-start;
    overflow-y: auto;
    padding-right: 2%;
    max-height: calc(100vh - 120px);
  }

  &-item {
    text-decoration: none;
    margin-left: 3%;
    display: flex;
    flex-flow: column;
    justify-content: flex-start;
    width: 31.3%;
    min-height: 233.55px;
    position: relative;
    border-radius: 2px;
    box-shadow: 0 0 0 128px rgba(0, 0, 0, 0.2) inset, 0 1px 0 0 #d7d8db, 0 0 0 1px #e3e4e8;
    text-shadow: 1px 1px 2px rgba(0,0,0,0.5);
    padding: 10px 10px;

    &:nth-child(3n-2) {
      margin-left: 0;
    }

    &:nth-child(3n) {
      margin-right: 0;
    }

    &:nth-child(n+4) {
      margin-top: 3%;
    }
  }

    &-name {
      font-family: 'Roboto Slab', serif;
      font-weight: 400;
      text-align: left;
      color: white;
      font-size: 18px;
      line-height: 24px;
      letter-spacing: 0.2px;
    }

    &-weight {
      font-family: 'Roboto Slab', serif;
      color: white;
      font-size: 11px;
    }

    .add-to-card {
      font-family: 'Open Sans', sans-serif;
      font-size: 14px;
      position: absolute;
      bottom: 10px;
      left: 10px;
      padding: 10px;
      background-color: #4890b6;
      border: none;
      color: white;
      cursor: pointer;
      border-radius: 3px;
    }
}


</style>
