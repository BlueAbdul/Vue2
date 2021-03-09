<template>
  <b-container id="app">
   <b-card class="shadow-lg">
     <b-row>
       <b-col>
       <h1>Liste des serveurs</h1>
       <br><br>
       <h4>Nombre de serveurs : {{totalServe}} </h4>
       </b-col>
     </b-row>
    <br><br>

    <b-row>
       <b-table stacked="lg" :items="serverList"  >
          
          <template #cell(actions)="row">

            <b-button variant="light" size="md" @click="onAddPrestation()">
              <i class="fa-fw fas fa-plus-circle m-2 text-primary" />
            </b-button>

            <b-button :disabled="serverList < 2" variant="light" size="md" @click="onRemovePrestation(row.index)">
              <i class="fa-fw fas fa-trash m-2 text-danger" />
            </b-button>

          </template>

          <template #cell(name)="row">
            <b-input v-model="row.item.name" />
          </template>
          <template label="Head Variant" #cell(capacity)="row">
            <b-input type="number" v-model.number="row.item.capacity" />
          </template>
          <template #cell(bandwidth)="row">
            <b-input v-model.number="row.item.bandwidth" min="1" />
          </template>
          <template #cell(online)="row">
            <i v-if='row.item.online' class="fas fa-globe-asia" style="color:limegreen;"></i>
            <i v-if='!row.item.online' class="fas fa-globe-asia" style="color:red;"></i>
          </template>
        </b-table>
    </b-row>

    <b-row>
      <b-col>
        Capacité totale : {{totalCapacity}} Tflops
      </b-col>
      <b-col>
        Bande passante totale : {{totalBandwith}} Go/s
      </b-col>
    </b-row>

   </b-card>

  </b-container>
</template>

<script>


export default {
  name: 'App',
  data(){
      return {
        fields: ['Nom serveur', 'Capacité (TFlop/s)', 'Bande passante', 'En ligne'],
        serverList: [
        {
          name: 'Mars',
          capacity : 768,
          bandwidth : 75,
          online : true
        },{
          name: 'Hades',
          capacity : 6780,
          bandwidth : 350,
          online : true
        },
        {
          name: 'Jupiter',
          capacity : 3076,
          bandwidth : 150,
          online : true
        },
        {
          name: 'Athena',
          capacity : 2048,
          bandwidth : 125,
          online : true
        },
        {
          name: 'Hephaistos',
          capacity : 512,
          bandwidth : 65,
          online : false
        },
        {
          name: 'Zeus',
          capacity : 7680,
          bandwidth : 450,
          online : true
        },
        {
          name: 'Gaïa',
          capacity : 12720,
          bandwidth : 1024,
          online : true
        }
        ,
        {
          name: 'Hercules',
          capacity : 256,
          bandwidth : 20,
          online : false
        }
        ]
      }
      },
      computed: {
        totalServe(){
          return this.serverList.length
        },

        totalCapacity(){
          let res = 0

          this.serverList.forEach((e)=>{
            res += e.capacity
          })

          return res
        },
        totalBandwith(){
          let res = 0

          this.serverList.forEach((e)=>{
            res += e.bandwidth
          })

          return res
        }
    }
}
</script>

<style>

@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.2/css/all.min.css');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
