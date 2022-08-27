<template>
  <div id="profile">
    <h2>Profile</h2>
    <div>
      <p>Name: {{name}}</p>
      <p>Email: {{ email }}</p>
      <p>Goal - {{goal}}</p>
    </div>
  </div>
</template>

<script>

export default {
  name: "ProfileComponent",
  data() {
    return {
      name: '',
      email: '',
      goal:''
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