<template>
  <div class="row">
        <div class="col-12">
        <card title="Users">
          <div class="table-responsive">
            <base-table :data="tableData"
                        :columns="tableColumns"
                        thead-classes="text-primary">
            </base-table>
          </div>
        </card>
      </div>

      <div class="col-12">
        <card class="card-plain">
          <div class="table-full-width table-responsive">
            <base-table title="Cultivos" :data="cropTableData"
                         :columns="cropTableColumns">

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
    return {
        tableData:[],
        tableColumns:["ID","Email","Date"],
        cropTableData:[],
        cropTableColumns:["ID","Name","Description","Hydrogen","Temperature","Water"]
    }
  },
  beforeMount(){
    Axios.get("https://optipapa-c3caa-default-rtdb.firebaseio.com/users.json").then((value)=>{
        let data = value.data;
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

          this.tableData.push(user);
          if(currentObject.cultivos){
            this.cropTableData.push(...currentObject.cultivos)
          }
        }
      }).catch((error)=>{
        console.log(error);
      });
  }
};
</script>
<style>
</style>
