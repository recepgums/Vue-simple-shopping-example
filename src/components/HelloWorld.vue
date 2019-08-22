<template>
  <div class="hello">
    
    <!--- SORTİNG STUFF --->


    <div class="container">
      <div class="row ">
        <div class="card col-sm "   id="ana-kart" v-for="item in info.data" :key="item" >
            <img v-bind:src="item.image" :alt="name" class="card-img-top">
            <div class="card-body " >
              <h4 class="card-title widthh"  >{{ item.name }}</h4>
              <div class="card-text price ">{{ item.price }}  {{ item.currency }}</div>
              <div class="row justify-content-end bottomm">
                <button class="btn btn-primary " @click="addToCart(item.id,item.price)">Sepete Ekle</button>
              </div>
            </div>
        </div>
      </div>
    </div>
</div>
</template>

<script>
import axios from 'axios'
import {EventBus} from './event-bus.js';

export default {
  name: 'HelloWorld',
  methods: {
    addToCart(order_id,fiyat) {
      this.count+=1;
      this.orders.push(order_id);
      this.tutar+=parseFloat(fiyat);
      EventBus.$emit('i-got-clicked', this.orders);
      EventBus.$emit('i-got-clicked2', this.tutar);
    },
    sepet(){
      if(this.sepet_acma_kapama%2==0){
        this.veri=true;
        this.sepet_acma_kapama+=1;
      }else{
        this.veri=false;
      this.sepet_acma_kapama+=1;}
    },
    post(){
      alert("post değişkenlerini bulamadım")
    }
  },
  data(){
    return{
      veri:false,
      info:null,
      orders:[],
      tutar:0,
    }
  },
    mounted: function(){
    axios
            .get('https://nonchalant-fang.glitch.me/listing')
            .then(response => (this.info = response));
  },
  watch:{
    
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#ana-kart{
  position: relative;
  background-color: #999999;
  margin-left:20px;
  margin-top:40px;
  height: 320px;
  
}
.widthh{
  font-size: 20px
}
.price{
  color:rgb(33, 99, 153);
  top: 10;
}
.bottomm{
   position: absolute;
    bottom: 0;
}
</style>
