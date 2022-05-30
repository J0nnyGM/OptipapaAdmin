<template>
    <div class="row">
      <div class="col-12">
        <card class="card-plain">
          <div class="table-full-width table-responsive">
            <base-table title="KPIS" :data="tableData"
                         :columns="tableColumns">

            </base-table>
          </div>
        </card>
      </div>
  </div>
</template>
<script>
import Axios from 'axios';
import { BaseTable } from "@/components";
export default {
  components:{
    BaseTable
  },
  data(){
    return{
      tableData:[
        {
          nombre:"Calificaciones de la aplicación por usuarios",
          valor:0,
          medida:"Puntuacion"
        },
        {
          nombre:"Cantidad de usuarios creados ",
          valor:0,
          medida:"Puntuacion"
        },
        {
          nombre:"Cantidad de cultivos registrados ",
          valor:0,
          medida:"Puntuacion"
        },
        {
          nombre:"Promedio de tiempo de los cultivos",
          valor:0,
          medida:"Puntuacion"
        },
        {
          nombre:"Cantidad de agua promedio por cultivo",
          valor:0,
          medida:"Puntuacion"
        },
      ],
      tableColumns:["Nombre","valor","Medida"],
    }
  },
  beforeMount(){
    Axios.get("https://optipapa-c3caa-default-rtdb.firebaseio.com/users.json").then((value)=>{
        let data = value.data;
        let tiempoPromedio = 0;     
        let aguaPromedio = 0;     
        let totalCultivos = 0;      
        for(var key of Object.keys(data)){
          let currentObject = data[key];
          let user = {
            id:"",
            email:"",
            date:"",
            rating:0
          }
          user.id = currentObject.id;
          user.email = currentObject.email;
          user.date = currentObject.date;
          user.rating = currentObject.rating;

          
          this.tableData[0].valor++;
          this.tableData[1].valor++;
          this.tableData[2].valor+=3; 

          currentObject.cultivos.forEach(element => {
            tiempoPromedio += element.time;
            aguaPromedio += element.water;

            totalCultivos++;
          });

        }

        
        
        this.tableData[3].valor = Math.floor(tiempoPromedio/=totalCultivos);
        this.tableData[4].valor = Math.floor(aguaPromedio/=totalCultivos);


        
      }).catch((error)=>{
        console.log(error);
      });
  }
};
</script>
<style>
</style>
