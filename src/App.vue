<template>

  <div class='black-bg' v-if="modal_status == 'OPENED'">
      <div class='white-bg'>
        <span class='modal-close' @click='closeModal()'>닫기</span>
        <img :src="selectedProduct().image" class="room-img">
        <h4>{{selectedProduct().title}}</h4>
        <p>{{selectedProduct().content}}</p>
        <p>{{selectedProduct().price}} 원</p>
        <p> 신고 수 : {{selectedProduct().reportCnt}} </p>
      </div>
  </div>

  <img alt="Vue logo" src="./assets/logo.png">

  <div class='menu'>
      <a v-for="(menu, idx) in menus" :key='idx'> {{ menu }}</a>
  </div>

  <div class="component" v-for="(product, idx) in products" :key='idx'>
      <img :src="product.image" class="room-img">
      <h4 :style='baseColor' @click="openModal(product)">{{product.title}}</h4>
      <p>{{product.content}}</p>
      <p>{{product.price}} 원</p>
      <button v-on:click="report(product)">허위매물신고</button> <span>신고 수: {{product.reportCnt}}</span>
  </div>
</template>

<script>
import products from './product'

export default {
  name: 'App',
  created() {
    console.warn(process.env)
  },
  data(){
      return { 
          baseColor: 'color: blue',
          menus: ["Home", "Products", "About"],
          modal_status: 'CLOSED',
          products: products
      }
  },
  methods: {
    report(product) {
      console.warn('product -> ', product)
      product.reportCnt++
    },
    openModal(product) {
      this.modal_status = 'OPENED'
      product.selected = true
    },
    selectedProduct() {
      return this.products.filter( product => product.selected )[0]
    },
    closeModal() {
      this.products.forEach ( product => product.selected = false )
      this.modal_status = 'CLOSED'
    }
  },
  components: {
    
  }
}
</script>

<style>
body { margin: 0; }
div { box-sizing: border-box; }
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

.room-img {
  width: 100%;
  margin-top: 20px;
}

.modal-close {
  float: right;
  color: black;
  font-size: 12px;
  margin-right: 1%;
}

.modal-close:hover {
  text-decoration: underline;
  cursor: pointer;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0,0,0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 80%;
  margin: 0 auto;
  background: white;
  border-radius: 8px;
  padding: 20px;
}
.component span, button {margin-right: 10px;}
</style>
