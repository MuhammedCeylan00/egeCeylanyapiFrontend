<template>
  <div class="hello">
    <h2 style="display: flex; justify-content: center; align-items: center;">Ceylan parke</h2>
    <router-link to="/musteriler">
      <button class="customer">Müşteri kayıtları</button>
    </router-link>
    <form @submit.prevent="addCustomer">
      <div>
        <label for="name">İsim Soyisim</label>
        <input type="text" id="name" v-model="customer.namesurname">
      </div>
      <div>
        <label for="phone">Telefon</label>
        <input type="text" id="phone" v-model="customer.phone">
      </div>
      <div>
        <label for="address">Adres</label>
        <textarea id="address" v-model="customer.adress"></textarea>
      </div>
      <div>
        <label for="material">Malzeme</label>
        <textarea type="text" id="material" v-model="customer.material"></textarea>
      </div>
      <div>
        <label for="price">Fiyat</label>
        <input type="number" id="price" v-model="customer.price">
      </div>
      <div>
        <label for="paid">Alınan Ödeme</label>
        <input type="number" id="paid" v-model="customer.moneypaid">
      </div>
      <button class="button" type="submit">Müşteri Ekle</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      customer: {
        namesurname: '',
        phone: '',
        adress: '',
        material: '',
        price: 0,
        moneypaid: 0,
      }
    }
  },
  methods: {
    async addCustomer() {
      await axios.post("http://localhost:3000/savecustomers", this.customer, {
      })
        .then(response => {
          console.log(response);
        })
        .catch(err => {
          console.error(err);
        });
      await axios.post("http://localhost:3000/sendmail", this.customer, {
      })
        .then(response => {
          console.log(response);
        })
        .catch(err => {
          console.error(err);
        });

        this.customer = {
        namesurname: '',
        phone: '',
        adress: '',
        material: '',
        price: 0,
        moneypaid: 0,
      };
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.hello form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-width: 500px;
  margin: auto;
  padding: 20px;
  background-color: #f9f9f9;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

.hello form div {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.hello form label {
  font-size: 1.1rem;
  font-weight: bold;
}

.hello form input[type="text"],
.hello form textarea,
.hello form input[type="number"] {
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 3px;
  font-size: 1rem;
}

.hello form input[type="submit"] {
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 1.2rem;
  cursor: pointer;
}

.button {
  height: 30px;
  cursor: pointer;
  background-color: rgb(46, 224, 46);
  border-radius: 10px;
  border: 1px solid rgb(46, 224, 46);
  color: white;
  font-weight: bold;
}

.button:hover {
  background-color: rgb(255, 255, 255);
  color: rgb(46, 224, 46);
  border: 1px solid rgb(46, 224, 46);
  transition: 0.5s ease-in-out;
}

.customer {
  margin-left: 80%;
  width: 100px;
  height: 50px;
  border-radius: 10px;
  border: 1px solid gray;
  cursor: pointer;
}
</style>

