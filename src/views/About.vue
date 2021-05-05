<template>
  <v-container>
    <v-row>
      <v-col>
        <v-text-field placeholder=" " dense v-model="name" label="Name" outlined></v-text-field>
        <v-btn @click="add">Add</v-btn>
        <v-data-table
          :headers="headers"
          :items="data"
          :items-per-page="5"
          class="elevation-1"
      >
      <template v-slot:item="allData">
        <tr>
          <td>{{allData.item.id}}</td>
          <td>{{allData.item.name}}</td>
          <td>{{allData.item.items}}</td>
          <td align="center">
            <v-btn small text @click="deleteData(allData.item.id)">Delete</v-btn>
          </td>
        </tr>
      </template>
        </v-data-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
const baseUrl = "http://18.139.50.74:8080"

export default {
  name: 'LoginPage',
  components: {
  },
  data(){
    return{
      data : [],      
      headers: [
          {
            text: "ID",
            width: "150px",
          },
          {
            text: "Name",
            width: "150px",
          },
          {
            text: "Items",
            width: "150px",
          },
          {
            text: "Actions",
            width: "150px",
          },
      ],
      name: '',
    }
  },
  mounted(){
    this.loadData()
  },
  methods: {
    loadData(){
      let token = 'Bearer'+ ' ' +localStorage.getItem('token')
      axios.get(`${baseUrl}/checklist`, {
        headers: {
          'Authorization': token,
        }
      }).then(res => {
        console.log("RESPONSE NYA",res.data.data)
        this.data = res.data.data
      })
    },
    deleteData(id){
      let token = 'Bearer'+ ' ' +localStorage.getItem('token')
      axios.delete(`${baseUrl}/checklist/${id}`,{
        headers: {
          'Authorization': token,
        }
      }).then(res => {
        console.log("sukses", res.data)
        this.loadData()
      })
    },
    add(){
      let token = 'Bearer'+ ' ' +localStorage.getItem('token')
      axios.post(`${baseUrl}/checklist`,{ name : this.name}, {
         headers: {
          'Authorization': token,
        }
      }).then(()=> {
          this.name = ''
          this.loadData()
      }) 
      
    }
  }
}
</script>
