<template>
  <div id="profile">
    <h2>Profile</h2>
    <div>
      <p>Name: {{name}}</p>
      <p>Email: {{ email }}</p>
    </div>
  </div>
</template>

<script>

export default {
  name: "ProfileComponent",
  data() {
    return {
      name: '',
      email: ''
    }
  },
  created() {
    this.emitter.on('form-submitted', ({ name, email}) => {
      this.name = name;
      this.email = email
    })
  },
  beforeDestroy() {
    this.emitter.off('form-submitted');
  },
}
</script>

<style scoped>

</style>