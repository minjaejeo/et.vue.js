<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <button @click="getFruites">getFruites</button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },
  methods: {
    getApple() {
      return new Promise((resolve) => {
        setTimeout(() => resolve("apple"), 1000);
      })
    },
    getBanana() {
      return new Promise((resolve) => {
          setTimeout(() => resolve("banana"), 1000);
      })
    },
    // async getFruites() {
    //   console.time();
    //   let a = await this.getApple();
    //   let b = await this.getBanana();
    //   console.log(a, b);
    //   console.timeEnd();
    // }
    // async getFruites() {
    //   console.time();
    //   let getApplePromise = this.getApple();
    //   let getBananaPromise = this.getBanana();
    //   let a = await getApplePromise;
    //   let b = await getBananaPromise;
    //   console.log(a, b);
    //   console.timeEnd();
    // }
    async getFruites() {
      console.time();
      let [ a, b ] = await Promise.all([ this.getApple(), this.getBanana() ]);
      console.log(a, b);
      console.timeEnd();
    }
  }
}
</script>
