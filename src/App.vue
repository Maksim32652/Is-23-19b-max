<script setup>
import { ref,computed} from "vue";


const products = ref([
{
  id: 1,
  name: 'Iphone',
  date:'20.12.2024',
  count:100,
  price: 2000,
},
{
  id: 2,
  name: 'Oppo',
  date:'20.12.2024',
  count:110,
  price: 1300,
},
{
  id: 3,
  name: 'Xiomi',
  date:'20.12.2024',
  count:90,
  price: 990,
},
{
  id:4 ,
  name: 'Apple',
  date:'20.12.2024',
  count:200,
  price: 2550,
},
]);


const name =  ref('');
const date = ref('');
const count = ref(1);
const price = ref(0);

const addProduct = () => {
  if (name.value && date.value && count.value && price.value) {
    products.value.push(
      {
        id: Date.now(),
        name: name.value,
       date: date.value,
        count: count.value,
        price: price.value,
      }
    );
  }
}

const removeProduct = (id) => {
  products.value = products.value.filter((product) => product.id != id)
}

const totalSum = computed(() =>{
  return products.value.reduce((sum, product) => sum + (product.price * product.count), 0)
})
</script>

<template>
 <div class="contener">
 <div class="row">
  <div class="col">
    <h1 class="text-center mt-4">Учет товаров</h1>
    <form action="">
      <div class="mb-3">
      <label for="name" class="form-label">Название</label>
      <input type="text" v-model="name" class="form-control" id="name" >
      <div class="mb-3">
  <label for="date" class="form-label">Дата добавления</label>
  <input type="date" v-model="date" class="form-control" id="date" >
</div>
<div class="mb-3">
  <label for="count" class="form-label">Количество</label>
  <input type="number" v-model="count"class="form-control" id="number" >
</div>
<div class="mb-3">
  <label for="price" class="form-label">Цена</label>
  <input type="number" v-model="price"class="form-control" id="number">
</div>

</div>
<div class="mb-3 text-center">
  <button @click="addProduct" type="button" class="btn btn-outline-info">Добавить</button>
</div>
    </form>
  </div>
 </div>


 <div class="row row-cols-1 row-cols-md-3 g-4">
  <div class="col" v-for="product in products" :key="product.id">
    <div class="card h-100">
      
      <div class="card-body">
        <h5 class="card-title">{{product.name}}</h5>
        <p class="card-text">{{ product.date }}</p>
        <p class="card-text">{{ product.price }}</p>
        <p class="card-text">{{ product.count }} </p>
      </div>
      <div class="card-footer text-end">
        <button @click="removeProduct(product.id)" class="btn btn-outline-danger">Удалить</button>
      </div>
    </div>
  </div>
</div>
<div class="col">
  <h3 class="text-end">Общая сумма:${{ totalSum }}</h3>
</div>
 </div>

 
</template>

