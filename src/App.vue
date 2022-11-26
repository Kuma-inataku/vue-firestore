<script>
import db from "./firebase.js"

export default {
 name: "App",
 data() {
  return {
    data: [],
    ids: [],
    storeData: {
      name: "",
      doc: ""
    },
    updateData: {
      name: "",
      doc: ""
    },
    updateId: ""
  }
 },
  mounted: function () {
    console.log(this.data)
    db.collection("talk")
      .get()
      .then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          // console.log(doc.data());
          this.ids.push(doc.id);
          this.data.push(doc.data().name);
          this.data.push(doc.data().doc);
        })
      });
      console.log(this.ids)
  },
  methods: {
    inputtedStoreName(event) {
      this.storeData.name = event.target.value;
    },
    inputtedStoreDoc(event) {
      this.storeData.doc = event.target.value;
    },
    inputtedUpdateName(event) {
      this.updateData.name = event.target.value;
    },
    inputtedUpdateDoc(event) {
      this.updateData.doc = event.target.value;
    },
    changeId(event) {
      this.updateId = event.target.value;
    },
    store() {
      console.log("store");
      db.collection("talk").add({
          name:this.storeData.name,
          doc:this.storeData.doc
      })
      .then((docRef) => {
          console.log("Document written with ID: ", docRef.id);
      })
      .catch((error) => {
          console.error("Error adding document: ", error);
      });
    },
    update() {
      console.log("update");
      if (!this.updateId) {
        alert("idがnull")
        return;
      }
      db.collection("talk").doc(this.updateId).set({
        name:this.updateData.name,
        doc:this.updateData.doc
      });
    },

  }
}
</script>

<template>
  <h1>Firestore</h1>
  <h2>データ一覧</h2>
  <ul>
    <li v-for="(item, index) in data" :key="index">
      {{ item }}
    </li>
  </ul>
  <div>
    <h2>新規登録</h2>
    <form action="">
      <div>
        名前<input type="text" name="name" @input="inputtedStoreName">
      </div>
      <div>
        Doc<input type="text" name="doc" @input="inputtedStoreDoc">
      </div>
      <div>
        登録<input type="button" @click="store()" value="登録">
      </div>
    </form>
  </div>
  <div>
    <h2>更新（最初のIDのデータ）</h2>
    <form action="">
      <select name="id" @change="changeId">
        <option v-for="(id, key) in ids" :key="key" :value="id" name="id">{{id}}</option>
      </select>
      <div>
        名前<input type="text" name="name" @input="inputtedUpdateName">
      </div>
      <div>
        Doc<input type="text" name="doc" @input="inputtedUpdateDoc">
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
