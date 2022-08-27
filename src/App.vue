<template>
  <div class="container">
<ProfileComponent @getDataFromComponent="showDataFromComponent"></ProfileComponent>
    <p>data= {{data}} </p>
    <p>Busdata= {{busData}} </p>
    <div id="edit__profile">
      <h2>Enter your details below:</h2>
      <form @submit.prevent="handleSubmit">
        <div class="form-field">
          <label>Name:</label>
          <input type="text" v-model="user.name" />
        </div>
        <div class="form-field">
          <label>Email:</label>
          <input type="text" v-model="user.email" />
        </div>
        <button>Submit</button>
      </form>
    </div>
  </div>
  <button @click="sendGoal" > send goal to component</button>
</template>

<script>
import ProfileComponent from "@/components/ProfileComponent";

export default {
  name: 'App',
  data(){
    return{
      user: {
        name: '',
        email: ''
      },
      data: '',
      busData:''
    }
  },
  created() {
    this.emitter.on('busFromComponent',(el)=>{
      this.busData = el
    })
  },
  methods: {
    showDataFromComponent(val){
      this.data = val
    },
    handleSubmit() {
      //this.$eventBus.$emit('form-submitted', this.user)
      this.emitter.emit('form-submitted', this.user)
      this.user = {}
    },
    sendGoal(){
      this.emitter.emit('goal-sender','To be a senior developer ')
    }
  },
  components: {
   ProfileComponent
  }
}
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
