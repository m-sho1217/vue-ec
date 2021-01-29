<template>
  <div id="HOME" class="wrap">
    <Header></Header>
    <div class="title">
      <h1>商品一覧</h1>
    </div>
    <div class="container uk-child-width-1-2@s uk-grid-match" uk-grid>
      <div class="item-container btn uk-card uk-card-default uk-card-hover uk-card-body" v-for="item_id in Object.keys(items)" :key="item_id">
        <nuxt-link :to="'/detail/'+ item_id">
          <img :src="items[item_id].image_url" alt="商品画像">
          <p class="name">{{ items[item_id].name }}</p>
          <p class="price">¥ {{ items[item_id].price }}</p>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import firebase from '@/plugins/firebase'
  const db = firebase.firestore()
  const docRef = db.collection("items")

  export default {
    data() {
      return {
        items: {}
      }
    },
    created() {
      const _addItems = this.addItems
      db.collection("items").get().then(function(querySnapshot) {
        console.log(querySnapshot);
        querySnapshot.forEach(function(doc) {
          // itemsオブジェクトに
          _addItems(doc.id, doc.data());
          console.log(doc.id, " => ", doc.data());
        });
      });
    },
    methods: {
      addItems(id, item) {
        Vue.set(this.items, id, item);
        console.log(this.items);
      }
    }
  }
</script>

<style lang="scss" scoped>
</style>
