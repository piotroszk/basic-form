<template>
  <form class="w-25 mx-auto needs-validation" novalidate>
    <div class="form-group" v-for="(field, i) in formConfig" :key="i">
      <label :for="i" class="text-capitalize">{{ field.name }}</label>
      <input :type="field.type" v-model="form[field.name]" v-bind="field.validators" class="form-control" :id="i" :placeholder="field.placeholder">
      <div class="invalid-feedback">
        This field is required.
      </div>
    </div>
    <button class="btn btn-success mt-3" @click="onSubmit" :disabled="disabled">Submit</button>
  </form>
</template>

<script>
export default {
  name: "Form",
  props: {
    disabled: Boolean,
    formData: {
      type: Object,
      required: false
    },
    formConfig: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      form: {},
      valid: false
    }
  },
  methods: {
    onSubmit() {
      this.validateForm()
      if (this.valid) {
        this.$emit('onSubmit', this.form)
      }
    },
    validateForm() {
      const forms = document.querySelectorAll('.needs-validation')
      this.valid = true
      forms.forEach(form => {
        if (!form.checkValidity()) {
          this.valid = false
        }
      })
      Array.prototype.slice.call(forms)
          .forEach(function (form) {
            form.addEventListener('submit', function (event) {

              if (!form.checkValidity()) {
                event.preventDefault()
                event.stopPropagation()
              }

              form.classList.add('was-validated')
            }, false)
          })
    }
  },
  watch: {
    formData: function(val) {
      this.form = val
    }
  },
  mounted() {
    this.formConfig.forEach(field => {
      this.form[field.name] = null
    })
  }
}
</script>
<style lang="scss">
  .btn:disabled {
    cursor: not-allowed;
  }
</style>

