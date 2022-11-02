<template>
  <form @submit.prevent="onSubmit">
    <!-- Full Name -->
    <div class="form-group" :class="{ error: v$.form.name.$errors.length }">
      <input class="form-control" placeholder="Full Name *" type="text" v-model="v$.form.name.$model">
      <div class="pre-icon os-icon os-icon-user-male-circle"></div>
          <!-- error message -->
      <div class="input-name" v-for="(error, index) of v$.form.name.$errors" :key="index">
        <div class="error-msg">{{ error.$message }}</div>
      </div>
    </div>

    <!-- E-mail -->
    <div class="form-group" :class="{ error: v$.form.email.$errors.length }">
      <input class="form-control" placeholder="E-mail *" type="email" v-model="v$.form.email.$model">
      <div class="pre-icon os-icon os-icon-user-male-circle"></div>
          <!-- error message -->
      <div class="input-errors" v-for="(error, index) of v$.form.email.$errors" :key="index">
        <div class="error-msg">{{ error.$message }}</div>
      </div>
    </div>

    <!-- Phone -->
    <div class="form-group" :class="{ error: v$.form.phone.$errors.length }">
      <input class="form-control" placeholder="Phone *" type="number" v-model="v$.form.phone.$model">
      <div class="pre-icon os-icon os-icon-user-male-circle"></div>
          <!-- error message -->
      <div class="input-errors" v-for="(error, index) of v$.form.phone.$errors" :key="index">
        <div class="error-msg">{{ error.$message }}</div>
      </div>
    </div>

    <!-- Category -->
    <select v-model="form.category" @change="onChangeCategory($event)">
      <option disabled value>Category</option>
      <option v-for="option in categoryOptions" :key="option.categoryId" :value="option.name">
        {{ option.name }}
      </option>
    </select>

    <!-- Subcategory -->
    <select v-model="form.subcategory">
      <option disabled value>Subcategory</option>
      <option v-for="option in subcategoryOptions" :key="option.subCategoryId" :value="option?.name ? option.name : 'Subcategory'">
        {{ option.name }}
      </option>
    </select>

    <!-- Message -->
    <textarea
      v-model="form.message"
      placeholder="Message"
      maxlength="100"
      cols="150"
      rows="5">
    </textarea>
    <div class="message-counter">{{ form.message.length }} /100</div>

    <!-- Checkboxes Options -->
    <div>Please select at least one of the following:</div>
    <input type="checkbox" id="option1" value="option1" v-model="form.checkedOptions">
    <label for="option1">Option 1</label>

    <input type="checkbox" id="option2" value="option2" v-model="form.checkedOptions">
    <label for="option2">Option 2</label>

    <!-- Submit Button -->
    <div class="buttons">
      <button :disabled="v$.form.$invalid" class="btn btn-primary">Submit</button>
    </div>

  </form>
</template>

<script>
import axios from 'axios'
import useVuelidate from '@vuelidate/core'
import { required, email } from '@vuelidate/validators'

export default {
  name: 'ContactForm',
  props: {
  },
  setup () {
    return { v$: useVuelidate() }
  },

  data () {
    return {
      categoryListResponse: null,
      categoryOptions: null,
      subcategoryOptions: null,
      form: {
        name: '',
        email: '',
        phone: '',
        category: '',
        subcategory: '',
        message: '',
        checkedOptions: []
      }
    }
  },
  mounted () {
    axios
      .get('https://run.mocky.io/v3/0b8fbded-6ce4-4cb2-bf2f-d2c39207506b')
      .then(response => (this.categoryListResponse = response) && (this.categoryOptions = response.data))
  },
  validations() {
    return {
      form: {
        name: { required },
        email: { required, email },
        phone: { required },
      },
    }
  },
  methods: {
    onChangeCategory(event) {
      let selectedCategory = this.categoryListResponse.data.filter(
        category => category.name === event.target.value
      )
      let selectedSubcategories = selectedCategory[0].subCategories
      this.subcategoryOptions = selectedSubcategories
    }
  }
}
</script>

<style scoped>

</style>