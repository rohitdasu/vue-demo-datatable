<template>
  <div id="app">
    <div class="container">
      <span class="h1">Demo App</span>
      <div class="row">
        <input type="text" class="mr-2" />
        <button class="btn btn-success">POST</button>
      </div>
      <div class="row mt-4">
        <button class="btn btn-warning">GET TABLE DATA</button>
      </div>
      <div class="mt-5">
        <b-table striped hover :items="items" :fields="fields"></b-table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "App",
  data() {
    return {
      apiUrl:
        "https://1g1wp4zu1k.execute-api.us-east-1.amazonaws.com/dev/testSQSSender",
        tableData:[],
        fields: [
          {
            key: 'engine',
            sortable: true
          },
          {
            key: 'url',
            sortable: true
          },
          {
            key: 'id',
            sortable: true
          },
          {
            key: 'se_page',
            sortable: false
          },
          {
            key: 'se_port',
            sortable: false
          },
          {
            key: 'site_name',
            sortable: false
          },
          {
            key: 'snippet',
            sortable: false
          },
          {
            key: 'se_index_on_page',
            label: 'Person age',
            sortable: true,
            // Variant applies to the whole column, including the header and footer
            // variant: 'danger'
          }
        ],
        items: [
          { isActive: false, age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
          { isActive: false, age: 21, first_name: 'Larsen', last_name: 'Shaw' },
          { isActive: false, age: 89, first_name: 'Geneva', last_name: 'Wilson' },
          { isActive: false, age: 38, first_name: 'Jami', last_name: 'Carney' }
        ]
    };
  },
  created() {
    this.getData();
  },
  methods: {
    getData() {
      axios.get(this.apiUrl).then((res) => {
        res.data.map((data) =>{
          this.tableData.push(data);
        });
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
