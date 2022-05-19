<template>
  <form>
    <div v-if="vanHiba" class="alert alert-danger" role="alert">{{ this.message }}</div>
  <div>
    <label for="carlicenseplatenumber" class="form-label">Rendszám tábla</label>
    <input v-model="car.license_plate_number" type="text" class="form-control" id="carlicenseplatenumber" >
  </div>
  <div>
    <label for="carbrand" class="form-label">Márka</label>
    <input v-model="car.brand" type="text" class="form-control" id="carbrand" >
  </div>
  <div>
    <label for="carmodel" class="form-label">Model</label>
    <input v-model="car.model" type="text" class="form-control" id="carmodel" >
  </div>
  <div>
    <label for="cardailycost" class="form-label">Napidíj</label>
    <input v-model="car.daily_cost" type="number" class="form-control" id="cardailycost" >
  </div>
  
  <button @click="newCar" class="btn btn-primary">Új autó</button>
</form>
</template>

<script>
export default {
    name: 'CarForm',
    data(){
        return{
            vanHiba:false,
            message:'',
            car:{
                license_plate_number:'',
                brand:'',
                model:'',
                daily_cost:'',
            }
        }
    },
    methods:{
        async newCar(){
            let Response =await fetch("http://127.0.0.1:8000/api/cars", {
                method: "POST",
                headers:{
                    'Content-Type':'application/json',
                    'Accept':'application/json'
                },
                body:JSON.stringify(this.car)
            })
            let body=await Response.json()
            if (Response.status==201) {
                this.vanHiba=false
                this.car={
                    license_plate_number:'',
                    brand:'',
                    model:'',
                    daily_cost:'',
                }
                this.$emit("newcar")
                return
            }
            this.vanHiba=true
            this.message=body.message
        }
    }
}
</script>

<style>

</style>