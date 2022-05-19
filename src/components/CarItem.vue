<template>
  <div>
    <article class="card">
        <div class="card-body">
            <h1 class="card-title">{{ car.license_plate_number }}</h1>
            <p class="card-text">Márka: {{ car.brand }}</p>
            <p class="card-text">Modell: {{ car.model }}</p>
            <p class="card-text">Napidíj: {{ car.daily_cost }} Ft</p>
            <img :src=picture class="card-img-top" alt="Autó képe">
            <a @click="Rent" class="btn btn-primary">Kölcsönzés</a>
            <div v-if="vanHiba" class="alert alert-danger" role="alert">{{ this.message }}</div>
            <div v-if="sikeres" class="alert alert-success" role="alert">Sikeres kölcsönzés!</div>
        </div>
    </article><br/>
  </div>
</template>

<script>
export default {
    name: 'CarItem',
    props: [
        "car"
    ],
    data(){
        return{
            vanHiba:false,
            sikeres:false,
            message:''
        }
    },
    computed:{
        picture(){
            if(this.car.brand=="Ford" && this.car.model=="Focus"){
                return '/kepek/ford_focus.png'
            }else if(this.car.brand=="Ford" && this.car.model=="CX727"){
                return '/kepek/ford_cx727.png'
            }else if(this.car.brand=="Ford" && this.car.model=="Chile"){
                return '/kepek/ford_chile.png'
            }else if(this.car.brand=="Ford" && this.car.model=="Evos"){
                return '/kepek/ford_evos.png'
            }else if(this.car.brand=="Ford" && this.car.model=="Explorer"){
                return '/kepek/ford_explorer.png'
            }else if(this.car.brand=="Ford" && this.car.model=="Fiesta"){
                return '/kepek/ford_fiesta.png'
            }else if(this.car.brand=="Ford" && this.car.model=="Galaxy"){
                return '/kepek/ford_galaxy.png'
            }else if(this.car.brand=="Ford" && this.car.model=="Kuga"){
                return '/kepek/ford_kuga.png'
            }else if(this.car.brand=="Ford" && this.car.model=="Mondeo"){
                return '/kepek/ford_mondeo.png'
            }else if(this.car.brand=="Peugeot" && this.car.model=="208gt"){
                return '/kepek/peugeot_208gt.png'
            }else{
                return '/kepek/renault_clio.png'
            }
        }
    },
    methods:{
        async Rent(){
            let Response=await fetch(`http://127.0.0.1:8000/api/cars/${this.car.id}/rent`,{
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
                this.sikeres=true
                return
            }
            this.vanHiba=true
            this.sikeres=false
            this.message=body.message
        }
    }
}
</script>

<style>

</style>