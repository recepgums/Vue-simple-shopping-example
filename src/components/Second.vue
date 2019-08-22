<template lang="pug">
    <div>
    
    <div class="rightt" align="right">
        <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal"> Sepet    </button>
    </div>
        <!-- Modal -->
        <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" style="width:250px" role="document">
            <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Sepetim</h5>
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <div class="modal-body" style="width:250px" v-for="(item,key) in orders" :key="item">
            <span class="right"  @click="tekli_silme(key)">x</span>
                <div style="width:%100" >
                    <img  v-bind:src="info.data[item-1].image" :alt="name" class="card-img-top image-size">
                </div>
                <h4 class="card-title widthh"  >{{ info.data[item-1].name }}</h4>
                <h4 class="card-text price ">{{ info.data[item-1].price }}  {{ info.data[item-1].currency }}</h4>
            </div>
            <div class="modal-footer">
            <span style="text-align:left" v-if="1"><b>Tutar: {{this.total}}</b></span>
                <button type="button" class="btn btn-danger" @click="sepeti_bosalt">Sepeti Boşalt</button>
                <button type="button" class="btn btn-success"  @click="uyari">Satın Al</button>
            </div>
            </div>
        </div>
        </div>
    </div>
</template>


<script>
import {EventBus} from './event-bus.js';
import axios from 'axios'
export default {

    name:'Second',
    methods:{
         sepeti_bosalt(){
             for (var i = this.orders.length; i > 0; i--) {
                this.orders.pop();
            }
         },
         tekli_silme(id){
            this.orders.pop([id]);
         },
         uyari()
         {
             alert('Olmadı güzel kardeşim');
         }
     },

    mounted() { 
        axios
            .get('https://nonchalant-fang.glitch.me/listing')
            .then(response => (this.info = response));

        EventBus.$on('i-got-clicked', newOrder => {
        
        this.orders=newOrder;
        });
        EventBus.$on('i-got-clicked2', tutar => {
        this.total=tutar;
        });
        
         
        
     },
     data(){
         return {
             orders:[],
             info:null,
             total:0,
         }
     },
     
};
</script>

<style >
.rightt{
    position: relative;
    margin-right:200px;
}
.image-size{
   position: relative;
  height: 120px;
  width: 10px;
}
.right
   {
      float: right;

      width: 20px;

      background-color:#990000;
      color:white
   }
</style>