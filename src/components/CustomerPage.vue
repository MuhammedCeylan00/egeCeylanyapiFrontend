<template>
  <div class="customer-list">
    <div><router-link to="/">Geri dön</router-link></div>
    <h2>Müşteri Kayıtları</h2>
    <input type="text" v-model="searchQuery" placeholder="Arama...">
    <ul>
      <li v-for="(customer) in customersFiltered" :key="customer.id">
        <div>
          <p><span>İsim soyisim:</span> {{ customer.namesurname }}</p>
          <p><span>Telefon:</span> {{ customer.phone }}</p>
          <p><span>Adres</span> {{ customer.adress }}</p>
          <p><span>Malzeme</span> {{ customer.material }}</p>
          <p><span>Fiyat:</span> {{ customer.price }}</p>
          <p><span>Alınan ödeme: </span> {{ customer.moneypaid }}</p>
        </div>
        <button @click="deleteCustomer(customer.id)">Sil</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      customers: [],
      searchQuery: ''
    }
  },
  computed: {
    customersFiltered() {
      console.log(this.customers);
      if (this.customers.length === 0) {
        return [];
      } else if (this.searchQuery === "") {
        return this.customers;
      } else {
        return this.customers.filter((el) =>
          el.namesurname.toLowerCase().includes(this.searchQuery.toLowerCase().trim())
        );
      }
    }
  },
  mounted() {
    axios.get("http://localhost:3000/customers")
      .then(response => this.customers = response.data.reverse());
  },
  methods: {
    deleteCustomer(id) {
      console.log("id: ",id);
      axios.delete(`http://localhost:3000/deletecustomer/${id}`)
        .then(response => {
          console.log(response.data)
          // do something with the response
        })
        .catch(error => {
          console.log(error)
        })

        location.reload();
    }
  }
}
</script>

<style scoped>
.customer-list {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.customer-list h2 {
  text-align: center;
}

.customer-list input[type="text"] {
  display: block;
  margin-bottom: 10px;
  padding: 5px 10px;
  width: 96%;
  font-size: 16px;
}

.customer-list ul {
  list-style: none;
  padding: 0;
}

.customer-list li {
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.customer-list li div {
  flex-grow: 1;
  margin-right: 10px;
}

.customer-list button {
  background-color: red;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 10px;
}

span {
  color: blue;
  margin-right: 10px;
}
</style>
