<script>
import Firestore from "./components/Firestore.vue"
 
export default {
 name: "App",
 components: {
   Firestore,
 },
 methods: {
  store() {
    console.log("store")
  },
  update() {
    console.log("update")
  }
 }
}
</script>

<template>
  <h1>Firestore</h1>
  <div>
    <h2>データ一覧</h2>
    <Firestore />
  </div>
  <div>
    <h2>新規登録</h2>
    <form action="">
        <div>
            名前<input type="text" name="name">
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
