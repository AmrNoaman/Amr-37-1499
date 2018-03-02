<template>
  <div>
    <!-- <div class="row">
      <div class="col-md-12">
        <div class="card">

        </div>
      </div>
    </div> -->
    <div>
      <input type="text" v-model= "name" > Name <br>
      <input type="text" v-model= "price"> Price <br>
      <input type="text" v-model= "deleteP"> Delete Product <br>
      <input type="text" v-model= "updatePname"> Update Name <br>
      <input type="text" v-model= "updatePprice"> Update Price <br>
      <input type="text" v-model= "updatePid"> ID of product to be updated <br>
      <button v-on:click="AddToApi"> add product</button>
      <button v-on:click="DeleteP"> delete product</button>
      <button v-on:click="UpdateP"> update product</button>
    </div>

    <div>
    <table id="firstTable" style="width:100%">
    <thead>
      <tr>
        <th>CreatedAt</th>
        <th>ID</th>
        <th>Name</th>
        <th>Price</th>
        <th>SellerName</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in rows.data">
        <td>{{row.createdAt}}</td>
        <td>{{row._id}}</td>
        <td>{{row.name}}</td>
        <td>{{row.price}}</td>
        <td>{{row.sellerID}}</td>
        <!-- <button v-on:click="DeleteP"> delete product</button> -->
      </tr>
    </tbody>
    </table>
  </div>
</div>

</template>

<script>

import axios from 'axios'
import PaperTable from 'components/UIComponents/PaperTable.vue'
const tableColumns = ['Id', 'Name', 'Price', 'CreatedAt', 'UpdatedAt', 'SellerName', '']
const tableData = [{
  id: 1,
  name: 'Dakota Rice',
  price: '$36.738',
  createdat: '15/2/2018',
  updatedat: '16/2/2018',
  sellername: 'Mo'
},
{
  id: 2,
  name: 'Minerva Hooper',
  price: '$36.738',
  createdat: '15/2/2018',
  updatedat: '16/2/2018',
  sellername: 'Mo'
}]
export default {
  components: {
    PaperTable
  },
  data () {
    return {
      table1: {
        title: 'Stripped Table',
        subTitle: 'Here is a subtitle for this table',
        columns: [...tableColumns],
        data: [...tableData]
      },
      table2: {
        title: 'Table on Plain Background',
        subTitle: 'Here is a subtitle for this table',
        columns: [...tableColumns],
        data: [...tableData]
      },
      rows: [],
      name: '',
      price: '',
      deleteid: ''
    }
  },
  created () {
    this.getProd()
  },
  methods: {
    AddToApi () {
      axios.post('http://localhost:3000/api/product/createProduct', {
        name: this.name,
        price: this.price
      }).then((response) => {
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    getProd () {
      axios.get('http://localhost:3000/api/product/getProducts')
      .then((response) => {
        this.rows = response.data
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    DeleteP () {
      axios.delete('http://localhost:3000/api/product/deleteProduct/' + this.deleteP)
      .then((response) => {
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    },
    UpdateP () {
      axios.patch('http://localhost:3000/api/product/updateProduct/' + this.updatePid, {
        name: this.updatePname,
        price: this.updatePprice
      })
      .then((response) => {
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
    }
  }
}

</script>
<style>

</style>
