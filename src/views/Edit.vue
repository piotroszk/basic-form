<template>
  <div class="edit">
    <h1>Edit user</h1>
    <button class="btn btn-info my-5" @click="fillForm">Fill the form with data</button>
    <Form @onSubmit="editUser" :disabled="disabled" :form-data="formData" :form-config="config" />
  </div>
</template>

<script>
import config from '../../public/config/formConfig.json'
import Form from "@/components/Form";

export default {
  name: "Edit",
  components: { Form },
  data() {
    return {
      config,
      disabled: true,
      formData: {},
      user: {}
    }
  },
  methods: {
    editUser(user) {
      this.user = user
      localStorage.setItem('user', JSON.stringify(this.user));
      alert('User edited!')
    },
    fillForm() {
      this.formData = (Object.assign({}, this.user))
      this.disabled = false
    },
    retrieveUser() {
      const retrievedUser = localStorage.getItem('user');
      this.user = JSON.parse(retrievedUser)
    }
  },
  mounted() {
    this.retrieveUser()
  }
}
</script>
