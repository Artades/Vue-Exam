<template>
  <div class="purchases">
      <div class="purchases-body">
<h1>Purchases</h1>
<br>
<div  class="purchases-form">
    <input type="text" v-model.trim="title"  placeholder="Enter the product title">
<input type="number" v-model.trim="price"  placeholder="Enter the product price">
<button @click="createPurchase">+</button>
</div>
<br>

<br>
<h2>Total amount of purchases: <b>{{this.total}}</b> $</h2>
<br>



<div class="purchases-column" v-for="(item, idx) in purchases" :key="idx"  >
    <div class="item">
      <div class="item-upper">
<div>
 <h2 :style="{'text-decoration': item.isBought ? 'line-through' : ''}" >{{item.title}}</h2>
    <h3>{{item.price}} $</h3>
        </div>
        
        <div class="item-action">
<span class="complete"  @click="item.isBought = ! item.isBought" :style="{'background': item.isBought ? 'rgb(56, 192, 133)' : 'white'}"></span>
        <span class="delete"  @click="deletePurchase(item)">X</span>
        
       
        </div>
      </div>
      <div class="item-lower">
        <div class="chart">
        <div class="line" :style="{'width': Math.round(item.price / this.total *100) + '%' }"></div>
        </div>
        |
        <span v-html="Math.round(item.price / this.total *100) + '%' "></span>
      </div>
        
    </div>
    
</div>
 <button @click="clearPurchases">
    Buy
  </button>




      </div>
  </div>
</template>


<script>

export default {

data(){
    return{
total: null,
purchases: [],     
title: '',
price: null,
isBought: null,
}
 },
 methods: {
   
   clearPurchases(){
     alert(`Kaspi.kz: Вы совершили покупку на сумму: ${this.total} $`)
     this.purchases = []; 
     localStorage.removeItem("purchase") ;
      this.saveTotal();
   },
  
    createPurchase() {
      if (!this.title || !this.price) {
        alert('Fill the fields!!');
        return;
      }
      if (!this.purchases.length) {
        this.savePurchase();
        this.saveTotal();
      }
      this.purchases.push({
        title: this.title,
        price: this.price,
        isBought: this.isBought,
        idx: Date.now(),
        
      });
      this.saveTotal();
      this.savePurchase();
      this.title = "";
      this.price = null;
      this.total = this.total;

            let sum = 0;
this.purchases.forEach(i => {
  const res = i.price;
 let summ = sum+=res
this.total = summ;
////

})
    },
   
    deletePurchase(purchase) {
      this.purchases = this.purchases.filter((i) => i.idx !== purchase.idx);
        let sum = 0;
this.purchases.forEach(i => {
  const res = i.price;
 let summ = sum+=res
this.total = summ;
})

      this.savePurchase();
      this.saveTotal();
    },
    savePurchase() {
      const data = JSON.stringify(this.purchases);
      localStorage.setItem("purchase", data);
      
    },
    saveTotal(){
       localStorage.setItem('total', this.total)
    },

  
    
  },
   mounted() {
    if (localStorage.getItem("purchase")) {
      try {
        this.purchases = JSON.parse(localStorage.getItem("purchase"));
        this.total = localStorage.getItem("total");
      } catch (e) {
        localStorage.removeItem("purchase");
      }
    };
  
        
       let sum = 0;
this.purchases.forEach(i => {
  const res = i.price;
 let summ = sum+=res
this.total = summ;



})
     }
   }

</script>

<style>
.purchases{
    width:100%;
    
    border-radius: 12px;
   box-shadow: 0 0 9px rgba(19, 22, 31, 0.4) ;
  background: #fff;
}
.purchases-body{
    width: 100%;
    padding: 25px 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
.purchases-form{
    display: flex;
}
.purchases-form input{
    width: 100%;
    padding: 10px;
    border-radius: 12px;
   box-shadow: 0 0 9px rgba(19, 22, 31, 0.4) ;
  background: #fff;
  outline: none;
  border: 0;
  margin:  0 10px ;
}
.purchases-form input:focus{
   box-shadow: 0 0 9px rgba(16, 87, 53, 0.4) ;
}
button{
      width: 50px;
    padding: 10px;
    border-radius: 12px;
   box-shadow: 0 0 9px rgba(19, 22, 31, 0.4) ;
  background: rgb(66, 215, 160);
  outline: none;
  border: 0;
  margin:  0 10px ;
  color: white;
  font-weight: bold;
}
.purchases-column{
    width: 100%;
    display: flex;
    align-items: center;
    flex-direction: column;
}

.item{
    width: 500px;
     border-radius: 12px;
   box-shadow: 0 0 9px rgba(19, 22, 31, 0.4) ;
  background: #fff;
   margin: 10px 0;
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: column;
}
.item-upper{
  padding: 0 40px;
  width: 100%;
  display: flex;
  justify-content: space-between;
}

        .item-lower{
          width: 400px;
          display: flex;
          align-items: center;
          padding: 10px;
          border: 1px solid rgb(145, 150, 164);
          border-radius: 12px;
          justify-content: space-between;
        }
        .chart{
          width: 90%;
          
        }
        .line{
          width: 1%;
          height: 6px;
          background-color:rgb(66, 215, 160);
          border-radius: 12px; 
        }
.item-action{
  display: flex;
  align-items: center;
}
.complete{
  width: 20px;
  height: 20px;
  border: 1px solid rgb(61, 65, 68);
  border-radius: 50%;
  margin:  0 2px;
}
.delete{
   width: 20px;
  height: 20px;
  border: 1px solid rgb(210, 110, 110);
  border-radius: 50%;
  color: rgb(214, 81, 81);
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
    margin:  0 2px;
}

</style>