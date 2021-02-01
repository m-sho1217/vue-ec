<template>
  <div id="HOME" class="wrap">
    <Header></Header>
    <div class="uk-inline">
      <div class="search">
        <form @submit="searchItems">
          <div class="float-right uk-margin" uk-margin>
              <div uk-form-custom="target: true">
                <input v-model="search" class="uk-search-input" type="search" placeholder="">
              </div>
              <button class="uk-button uk-button-default">Submit</button>
          </div>
        </form>
      </div>
      <p>{{ search }}</p>
    </div>
    <div class="title">
      <h1>商品一覧</h1>
    </div>
    <div class="container uk-child-width-1-2@s uk-grid-match" uk-grid>
      <div v-for="item_id in Object.keys(items)" :key="item_id">
        <div class="item-container btn uk-card uk-card-default uk-card-hover uk-card-body" v-if="items[item_id].name.includes(search)">
          <nuxt-link :to="'/detail/'+ item_id">
            <img :src="items[item_id].image_url" alt="商品画像">
            <p class="name">{{ items[item_id].name }}</p>
            <p class="price">¥ {{ items[item_id].price }}</p>
          </nuxt-link>
        </div>
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
        items: {},
        search: ""
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
      },
      searchItems(e) {
        const _addItems = this.addItems
        const _clearItems = this.clearItems
        console.log(this.search)
        e.preventDefault();
        db.collection('items').where("name", "==", this.search).get().then(function(querySnapshot) {
          // _clearItems()
          console.log(querySnapshot);
          querySnapshot.forEach(function(doc) {
            _addItems(doc.id, doc.data());
            console.log(doc.id, " => ", doc.data());
          });
        });
      },
      clearItems() {
        this.items = {}
      }
    }
  }
</script>

<style lang="scss" scoped>
</style>
