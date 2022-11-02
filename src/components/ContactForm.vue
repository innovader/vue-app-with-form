<template>
  <h2>Contact Us</h2>

  <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>

  <form @submit.prevent="onSubmit">

    <!-- Full Name -->
    <div class="form-group" :class="{ error: v$.form.name.$errors.length }">
      <input
        class="form-control"
        placeholder="Full Name *"
        type="text"
        v-model="v$.form.name.$model"
      >
      <!-- error message -->
      <div class="input-name" v-for="(error, index) of v$.form.name.$errors" :key="index">
        <div class="error-msg">{{ error.$message }}</div>
      </div>
    </div>

    <!-- E-mail -->
    <div class="form-group" :class="{ error: v$.form.email.$errors.length }">
      <input
        class="form-control"
        placeholder="E-mail *"
        type="email"
        v-model="v$.form.email.$model"
      >
      <!-- error message -->
      <div
        class="input-errors"
        v-for="(error, index) of v$.form.email.$errors"
        :key="index"
        >
        <div class="error-msg">{{ error.$message }}</div>
      </div>
    </div>

    <!-- Phone -->
    <div class="form-group" :class="{ error: v$.form.phone.$errors.length }">
      <input
        class="form-control"
        placeholder="Phone *"
        type="number"
        v-model="v$.form.phone.$model"
      >
      <div class="pre-icon os-icon os-icon-user-male-circle"></div>
      <!-- error message -->
      <div
        class="input-errors"
        v-for="(error, index) of v$.form.phone.$errors"
        :key="index"
      >
        <div class="error-msg">{{ error.$message }}</div>
      </div>
    </div>

    <!-- Category -->
    <select v-model="form.category" @change="onChangeCategory($event)">
      <option disabled value>Category</option>
      <option
        v-for="option in categoryOptions"
        :key="option.categoryId"
        :value="option.name"
      >
        {{ option.name }}
      </option>
    </select>

    <!-- Subcategory -->
    <select v-model="form.subcategory">
      <option disabled value>Subcategory</option>
      <option
        v-for="option in subcategoryOptions"
        :key="option.subCategoryId"
        :value="option?.name ? option.name : 'Subcategory'"
      >
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
    <label v-for="checkbox in checkboxOptions" :key="checkbox.id">
      <input
        type="checkbox"
        :value="checkbox.id"
        :checked="checkbox.isChecked"
        v-model="form.checkedCheckboxes"
      >
      <span v-text="checkbox.name"></span>
    </label>

    <!-- Submit Button -->
    <div class="buttons">
      <button :disabled="v$.form.$invalid">Submit</button>
    </div>

  </form>

</template>

<script>
import axios from 'axios'
import useVuelidate from '@vuelidate/core'
import { required, email, alpha, numeric, } from '@vuelidate/validators'

export default {
  name: 'ContactForm',

  setup () {
    return { v$: useVuelidate() }
  },

  data () {
    return {
      categoryListResponse: null,
      categoryOptions: null,
      subcategoryOptions: null,
      checkboxOptions: [],
      form: {
        name: '',
        email: '',
        phone: '',
        category: '',
        subcategory: '',
        message: '',
        checkedCheckboxes: []
      }
    }
  },

  mounted () {
    // populate checkboxOptions on load.
    this.checkboxOptions =[
      { id: 'option1', name: 'Option 1', isChecked: false },
      { id: 'option2', name: 'Option 2', isChecked: false },
    ],
    // get data on load and store it in categoryListResponse, as well as populate categories(aka categoryOptions).
    axios
      .get('https://run.mocky.io/v3/0b8fbded-6ce4-4cb2-bf2f-d2c39207506b')
      .then(response => (this.categoryListResponse = response) && (this.categoryOptions = response.data))
  },

  validations() {
    //custom validator to check that at least one checkbox is selected.
    const atLeastOneCheckboxIsSelected = this.form.checkedCheckboxes.length > 0
    return {
      form: {
        name: { required, alpha }, // alpha means only letters.
        email: { required, email },
        phone: { required, numeric }, //numeric means only numbers.
        checkedCheckboxes: { required, atLeastOneCheckboxIsSelected}
      },
    }
  },

  methods: {
    onChangeCategory(event) {
      this.form.subcategory = '' // to remove prior subcategory selection, when selecting a new category.

      // populate subcategories(aka subcategoryOptions), depending on the category selected.
      let selectedCategory = this.categoryListResponse.data.filter(
        category => category.name === event.target.value
      )
      let selectedSubcategories = selectedCategory[0].subCategories
      this.subcategoryOptions = selectedSubcategories
    },
  }
}
</script>

<style scoped>

</style>