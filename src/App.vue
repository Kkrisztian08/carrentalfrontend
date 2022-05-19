<template>
  <div id="app" class="container">
    <nav>
      <ul class="nav">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="#newcar">Új autó felvétele</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="https://petrik.hu">Petrik honlap</a> 
        </li>
      </ul>
    </nav>
    <header><h1>Petrik Autókölcsönző</h1></header>
    <main class="row">
      <CarItem class="col-12 col-md-6 col-xl-4"
      v-for="car in cars"
      v-bind:key="car.id"
      :car="car"/>
    </main>
    <CarForm id="newcar" @newcar="Reload"/>
    <footer>Készitette: Kovács Krisztián</footer>
  </div>
</template>

<script>
import CarItem from './components/CarItem.vue'
import CarForm from './components/CarForm.vue'

export default {
  name: 'App',
  components: {
    CarItem,
    CarForm
  },
  data(){
    return{
      cars:[]
    }
  },
  methods:{
    async Reload(){
      let Response=await fetch("http://127.0.0.1:8000/api/cars")
      let data= await Response.json()
      console.log(data)
      this.cars=data.data
    }
  },
  async mounted(){
    this.Reload()
  }
}
</script>

<style>

</style>
