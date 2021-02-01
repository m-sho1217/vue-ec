<template>
  <div id="ITEM_DETAIL">
    <Header></Header>
    <div class="wrap">
      <div class="title">
        <h1>商品詳細</h1>
      </div>
      <div class="container">
        <div class="two-col">
          <div class="col-left">
            <span class="img-holder">
              <img :src="item.image_url" alt="">
            </span>
          </div>
          <div class="col-right">
            <p class="name">{{ item.name }}</p>
            <p class="price">
              {{ item.price }}円<span class="tax"> 税込</span>
            </p>
             <button class="btn uk-button uk-button-secondary uk-button-large">カートに入れる</button>
          </div>
        </div>
      </div>
    </div>
    <Footer></Footer>
  </div>

</template>

<script>
import firebase from '@/plugins/firebase'
const db = firebase.firestore()
/* TODO
doc.data()を格納する
*/

export default {
  data() {
    return {
      item: {}
    }
  },
  created() {
    const _addItem = this.addItem
    var docRef = db.collection("items").doc(this.$route.params.id);
    docRef.get().then(function(doc) {
        if (doc.exists) {
            _addItem(doc.data());
            console.log("Document data:", doc.data());
        } else {
            // doc.data() will be undefined in this case
            console.log("No such document!");
        }
    }).catch(function(error) {
        console.log("Error getting document:", error);
    });
  },
  methods: {
    addItem(item) {
      this.item = item
    }
  }
}
</script>



