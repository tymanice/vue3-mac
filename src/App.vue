<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
 
  <form @submit.prevent="submitForm">
  <div class="grid">
    <div class="col-6 form-control" :class="{invalid: isError  === 'invalid'}">
    <label for="firstName">First Name</label>
    <InputText type="text" id="firstName" placeholder="First Name" v-model="firstName"/>
    <p v-if="isError === 'invalid'">Please enter valid First Name</p>
    </div>
    <div class="col-6">
    <h2>TEst</h2>
    <Checkbox v-model="checked" :binary="true" />
    </div>
  </div>
  <div class="grid">
    <div class="col-3 form-control" >
      <label for="date">Date</label>
      <Calendar v-model="date" />
    </div>
     <div class="col-3">
      <Dropdown v-model="selectedCity" :options="cities" optionLabel="name" placeholder="Select a City" />
    </div>
    <div class="col-3">
      <component-one @custom-change="handleCustomChange"></component-one>
    </div>
  </div>
  <div>
     <Button @click="submitForm"> Submit</Button>
  </div>
  </form>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
//import ref from 'vue'
import axios from 'axios';
import Button from 'primevue/button'
import InputText from 'primevue/inputtext'
import Checkbox from 'primevue/checkbox'
import Calendar from 'primevue/calendar'
import Dropdown from 'primevue/dropdown'
import ComponentOne from './components/ComponentOne'

// const formData = ref({
//   name: ''
// })
export default {
  data() {
    return {
      firstName: '',
      checked: false,
      date: new Date(),
      isError: '',
      selectedCity: null,
      agency: '',
      cities: [
        {name: 'New York', code: 'NY'},
        {name: 'Rome', code: 'RM'},
        {name: 'London', code: 'LDN'},
        {name: 'Istanbul', code: 'IST'},
        {name: 'Paris', code: 'PRS'}
      ]
    }
  },
  name: 'App',
  components: {
    //HelloWorld,
    Button,
    InputText,
    Checkbox,
    Calendar,
    Dropdown,
    ComponentOne
  },
  
  methods: {
    handleCustomChange(e){
      this.agency = e
    },
    submitForm() {

      this.validDateInput()
      this.sendData()

      console.log('name: ', this.firstName)
      console.log('checked: ', this.checked)
      console.log('date: ', this.date)
      console.log('error: ', this.isError)
      console.log('emit: ',  this.agency)
    },
    validDateInput(){
      if(this.firstName.trim() === ''){
        this.isError = 'invalid'
      } else {
        this.isError = ''
      }
    },
    sendData(){
      axios.post('https://vue-http-demo-47aea-default-rtdb.firebaseio.com/formData.json', {
      firstName: this.firstName,
     
    })
      .then(function (response) {
      console.log(response);
    })
      .catch(function (error) {
      console.log(error);
    });
    }
  }
}

// const submitForm = () => {
//   console.log('name: ', formData.name)
// }
</script>

<style>
input, label {
  display:block;
  box-sizing:border-box;
  width: 100%;
}

.form-control.invalid input {
  border-color: red;
}

.form-control.invalid label {
  color: red;
}

.form-control.invalid p {
  color: red;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

