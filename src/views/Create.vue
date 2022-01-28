<template>
  <div class="create">
    <h1>Create user</h1>
    <Form @onSubmit="createUser" :form-config="config" />
  </div>
</template>

<script>
import config from '../../public/config/formConfig.json'
import Form from "@/components/Form";
export default {
  name: "Create",
  components: { Form },
  data() {
    return {
      config,
      user: {}
    }
  },
  methods: {
    createUser(user) {
      this.user = user
      localStorage.setItem('user', JSON.stringify(this.user));
      alert('User created!')
      this.$router.push({ name: 'Edit' })
    }
  }
}
</script>
