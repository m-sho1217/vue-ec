<template>
  <div class="wrap">
    <Header></Header>
    <div class="title">
      <h1>商品詳細</h1>
    </div>
    {{item}}
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
      item: null
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

<style lang="scss" scoped>

</style>

