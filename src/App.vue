<template>
  <div class="main">
   <div class="wrapper">
      <form @submit.prevent="submitForm" class="myform">
        <div  class="inputDiv">
          <label for="inputName">Name</label>
          <input :class="userValidate.name? 'isEror' : '' " v-model="user.name" type="text"  id="inputName">
        </div>
        <div class="inputDiv">
          <label for="inputSurname">Surname</label>
          <input :class="userValidate.surname? 'isEror' : '' " v-model="user.surname" type="text"  id="inputSurname">
        </div>
        <div class="inputDiv">
          <label for="inputEmail">email</label>
          <input :class="userValidate.email? 'isEror' : '' " v-model="user.email" type="email"  id="inputEmail">
        </div>
        <div class="inputDiv">
          <label for="country">country</label>
          <select v-model="user.country" class="selected">
            <option v-for="item in getContries" :key="item.id" :value="item.id">{{ item.name }}</option>
          </select>
        </div>
        <div class="inputDiv">
          <label for="inputAdrres">addres</label>
          <textarea v-model="user.address" id="inputAdrres" rows="5"></textarea>
        </div>
         <div class="inputDiv">
           <div>
             <h3>hobbies</h3>
            </div>
            <div class="checkbox">
            <div v-for="item in hobbies" :key="item.id">
             <label for="checkbox1">{{item.name}}</label>
             <input type="checkbox" id="checkbox1" name="hobbies" :value="item.id" v-model="user.hobbies">
            </div>
          </div>
        </div>
        <div class="inputtDiv">
          <div>
            <h3>gender</h3>
          </div>
          <div class="checkbox">
            <div v-for="item in gender" :key="item.id" >
              <label :for="item.id">{{ item.name }}</label>
              <input type="radio" :id="item.id" name="gender" :value="item.id" v-model="user.gender">
            </div>
          </div>
        </div>
          <div>
            <input type="file" hidden ref="myInputfile" @change="inputFile">
            <button  class="inputfileBtn" type="button" @click="$refs.myInputfile.click()">{{ file?.name ? 'change file' : 'select file' }}</button>
            <span v-if="file?.name">{{ file.name }}</span>
          </div>
        <IsAccept v-model="user.isAccept" />
        <button class="submitBtn" type="submit">submit</button>
      </form>
    </div>
    <div class="wrapper">
      <p>User INFO:  {{ user }}</p>
      <p>User country: {{ getCountrybyId(user.country) }}</p>
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      userValidate: {
        name: false,
        surname: false,
        email: false
      },
      user: {
        name: '',
        surname: '',
        email: '',
        country: 1,
        address: '',
        hobbies: [],
        gender: '',
        file: '',
        isAccept: true
      },
      file: {},
      countries: [{ id: 1, name: 'iran' }, { id: 2, name: 'leobnon' }],
      hobbies: [{ id: 1, name: 'football' }, { id: 2, name: 'volleyball' }],
      gender: [{ id: 1, name: 'male' }, { id: 2, name: 'female' }, { id: 3, name: 'other' }]
    }
  },
  components: {
  },
  methods: {
    validateData () {
      const obj = {
        name: this.user.name.trim() === '',
        surname: this.user.surname.trim() === '',
        email: this.user.email.trim() === ''
      }
      console.log(obj)
      return obj
    },
    inputFile (e) {
      console.log(e.target.files)

      this.file = { name: e.target.files[0].name }
      this.user.file = {
        name: e.target.files[0].name,
        size: e.target.files[0].size,
        type: e.target.files[0].type
      }
    },
    getCountrybyId (id) {
      return this.getContries.find((item) => item.id === id).name
    },
    submitForm () {
      console.log('form go')
      const validationResult = this.validateData()
      this.userValidate = validationResult
      if (Object.values(validationResult).includes(true)) {
        alert('form is invalid')
      } else {
        this.user = {
          name: '',
          surname: '',
          email: '',
          country: 1,
          address: '',
          hobbies: [],
          gender: '',
          file: ''
        }
        this.file = []
      }
    }
  },
  computed: {
    getContries () {
      return this.countries
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.isEror {
  border-color: red !important;
}
.main {
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 10px;

}
.wrapper {
  width: 50%;
  box-shadow:1px 3px 3px 1px;
  padding: 10px;
  border-radius: 5px;
  gap: 0px;
}
.inputDiv {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
.myform {
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.submitBtn{
  border-radius: 5px;
  padding: 3px;
  margin-top: 3px;
  background-color: aqua;
  color: black;
}
.submitBtn:hover{
  background-color: blue;
  color: aliceblue;
}
.selected{
  padding: 4px;
}
.checkbox{

  display: inline-flex;
}
.inputfileBtn {
  padding: 4px;
  border: none;
  border-radius: 5px;
  background-color: green;
}
.inputfileBtn:active{
  transform: scale(0.75);
}
</style>
