<script>
import db from "../firebase.js"

export default {
  data() {
    return {
      data: [],
    }
  },
  mounted: function () {
    db.collection("test")
      .get()
      .then((querySnapshot) => {
        querySnapshot.forEach((doc) => {
          console.log(`${doc.id} => ${doc.data().name}`)
          this.data.push(doc.data().name)
        })
      })
  },
}
</script>
<template>
  <div>
    <h1>Firestore Test</h1>
    <li v-for="(item, index) in data" :key="index">
      {{ item }}
    </li>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
