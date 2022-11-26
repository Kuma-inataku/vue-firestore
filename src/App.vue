<script>
import db from "./firebase.js"

export default {
 name: "App",
 data() {
  return {
    data: [],
    storeName: ""
  }
 },
  mounted: function () {
    console.log(this.data)
    db.collection("talk")
      .get()
      .then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          this.data.push(doc.data().name);
        })
      });
  },
  methods: {
    inputtedStoreData(event) {
      this.storeName = event.target.value;
      console.log(this.storeName)
    },
    store() {
      console.log("store");
      db.collection("talk").add({
          name:this.storeName
      })
      .then((docRef) => {
          console.log("Document written with ID: ", docRef.id);
      })
      .catch((error) => {
          console.error("Error adding document: ", error);
      });
    },
    update() {
      console.log("update")
      // db.collection("talk").doc("D9hGpkxVwuUEYWBQFL4O").set({name:this.storeName});
    },
  }
}
</script>

<template>
  <h1>Firestore</h1>
  <h2>データ一覧</h2>
    <!-- 一覧機能をここに移植 -->
    <!-- <Firestore /> -->
  <div>
    <li v-for="(item, index) in data" :key="index">
      {{ item }}
    </li>
  </div>
  <div>
    <h2>新規登録</h2>
    <form action="">
        <div>
          名前<input type="text" name="name" @input="inputtedStoreData">
        </div>
        <div>
          登録<input type="button" @click="store()" value="登録">
        </div>
    </form>
  </div>
  <div>
    <h2>更新（最初のIDのデータ）</h2>
    <form action="">
        <div>
            名前<input type="text" name="name">
        </div>
        <div>
            更新<input type="button" @click="update()" value="登録">
        </div>
    </form>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
