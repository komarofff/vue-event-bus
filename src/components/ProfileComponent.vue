<template>
  <div id="profile">
    <h2>Profile</h2>
    <div>
      <p>Name: {{name}}</p>
      <p>Email: {{ email }}</p>
      <p>Goal - {{goal}}</p>
    </div>
  </div>
  <button @click="sendToApp">send emit to App</button>
  <button @click="sendBus">send bus to App</button>
</template>

<script>

export default {
  name: "ProfileComponent",
  emits:['getDataFromComponent'],
  data() {
    return {
      name: '',
      email: '',
      goal:''
    }
  },
  methods:{
    sendToApp(){
      this.$emit('getDataFromComponent','I`m data from component')
    },
    sendBus(){
      this.emitter.emit('busFromComponent','data from bus ')
    }
  },
  created() {
    this.emitter.on('form-submitted', ({ name, email}) => {
      this.name = name;
      this.email = email
    })
    this.emitter.on('goal-sender',(goal)=>{
      this.goal = goal
    })
  },
  beforeDestroy() {
    this.emitter.off('form-submitted');
  },

}
</script>

<style scoped>

</style>