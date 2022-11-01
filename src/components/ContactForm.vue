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
    
    <select v-model="form.category">
      <option v-for="option in categoryOptions" :key="option.categoryId" :value="form.category">
        {{ option.name }}
      </option>
    </select>

    <!-- Subcategory -->
    <select v-model="form.subcategory">
      <option v-for="option in subcategoryOptions" :key="option.subCategoryId" :value="form.subcategory">
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
import useVuelidate from '@vuelidate/core'
import { required, email } from '@vuelidate/validators'
// import categoryList from './categoryList'

export default {
  name: 'ContactForm',
  props: {
  //   categoryList: [
  // {
  // categoryId: 0,
  // name: "All"
  // },
  // {
  // categoryId: 1,
  // name: "Books",
  // subCategories: [
  //   {
  //   subCategoryId: 1,
  //   name: "Hardcover"
  //   },
  //   {
  //   subCategoryId: 2,
  //   name: "Paperback"
  //   },
  //   {
  //   subCategoryId: 3,
  //   name: "Electronic"
  //   }
  // ]
  // },
  // {
  // categoryId: 2,
  // name: "Movies",
  // subCategories: [
  //   {
  //   subCategoryId: 4,
  //   name: "DVD"
  //   },
  //   {
  //   subCategoryId: 5,
  //   name: "BluRay"
  //   },
  //   {
  //   subCategoryId: 6,
  //   name: "Download"
  //   }
  // ]
  // },
  // {
  // categoryId: 3,
  // name: "Games",
  // subCategories: [
  //   {
  //   subCategoryId: 7,
  //   name: "XBox"
  //   },
  //   {
  //   subCategoryId: 8,
  //   name: "PC"
  //   }
  // ]
  // },
  // {
  // categoryId: 4,
  // name: "Music"
  // }
  //     ],
  },
  setup () {
    return { v$: useVuelidate() }
  },

  data() {
    return {
      categoryList: null,
      categoryOptions: [
          {
            categoryId: 0,
            name: "All"
          }
        ],
      subcategoryOptions: [
        {
          subCategoryId: 1,
          name: "Hardcover"
          },
          {
          subCategoryId: 2,
          name: "Paperback"
          },
          {
          subCategoryId: 3,
          name: "Electronic"
        }
      ],
      form: {
        name: '',
        email: '',
        phone: '',
        category: 'Category',
        subcategory: 'Subcategory',
        message: '',
        checkedOptions: []
      }
    }
  },
  mounted () {
    axios
      .get('https://run.mocky.io/v3/0b8fbded-6ce4-4cb2-bf2f-d2c39207506b')
      .then(response => (this.categoryList = response))
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
}
</script>

<style scoped>

</style>