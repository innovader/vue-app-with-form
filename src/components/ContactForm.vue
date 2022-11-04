<template>
  <div class="contact-form-container" :class="showMobile ? 'contact-form-container-mobile' : ''">
    
    <div class="upper-text">
      <div :class="showMobile ? 'heading-mobile' : 'heading'">Contact Us</div>
      <p :class="showMobile ? 'description-mobile' : 'description'">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
    </div>

    <form class="form-only" @submit.prevent="onSubmit">
      <!-- Full Name -->
      <div class="form-group" :class="{ error: v$.form.name.$errors.length }">
        <input
        :class="showMobile ? 'input-mobile' : 'input-desktop'"
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
          :class="showMobile ? 'input-mobile' : 'input-desktop'"
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
          :class="showMobile ? 'input-mobile' : 'input-desktop'"
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
      <div :class="showMobile ? 'selections-container-mobile' : 'selections-container'">
        <select :class="showMobile ? 'select-mobile': ''" v-model="form.category" @change="onChangeCategory($event)">
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
        <select :class="showMobile ? 'select-mobile': ''" v-model="form.subcategory">
          <option disabled value>Subcategory</option>
          <option
            v-for="option in subcategoryOptions"
            :key="option.subCategoryId"
            :value="option?.name ? option.name : 'Subcategory'"
          >
            {{ option.name }}
          </option>
        </select>
      </div>

      <!-- Message -->
      <div class="textarea-container">
        <textarea
          v-model="form.message"
          placeholder="Message"
          maxlength="100">
        </textarea>
        <div class="message-counter">{{ form.message.length }} /100</div>
      </div>

      <!-- Checkboxes Options -->
      <div class="checkboxes-container">
        <div class="checkboxes-warning">Please select at least one of the following:</div>
        <label class="checkboxes-label" v-for="checkbox in checkboxOptions" :key="checkbox.id">
          <input
            class="checkboxes-input"
            type="checkbox"
            :value="checkbox.id"
            :checked="checkbox.isChecked"
            v-model="form.checkedCheckboxes"
          >
          <span v-text="checkbox.name"></span>
        </label>
      </div>

      <!-- Submit Button -->
      <div class="submit-button">
        <button :disabled="v$.form.$invalid" :class="showMobile ? 'button-mobile' : ''">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
import useVuelidate from '@vuelidate/core'
import { required, email, alpha, numeric, } from '@vuelidate/validators'

export default {
  name: 'ContactForm',

  props: {
    showMobile: Boolean,
  },

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
      .then((response) => {
        (this.categoryListResponse = response) && (this.categoryOptions = response.data)
      })
      .catch((error) => {
        console.log(error)
      })
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
.contact-form-container {
  background-color: #F8F8F8;
  padding: 104px 154px;
}

.contact-form-container-mobile {
  padding: 36px 24px;
}

.heading {
  font-size: 32px;
  font-weight: 800;
}

.heading-mobile {
  font-size: 28px;
  font-weight: 800;
}

.description {
  font-size: 18px;
}

.description-mobile {
  font-size: 16px;
}

p {
  margin-top: 32px;
  margin-bottom: 48px;
}

.textarea-container {
  margin-bottom: 40px;
}

.message-counter {
  display: flex;
  justify-content: flex-end;
  font-size: 12px;
}

textarea {
  width: calc(100% - 46px);
  padding-left: 40px;
  height: 112px;
  border-radius: 28px;
  font-size: 16px;
  color: #000000;
  border: 1px solid #000000;
}

.input-desktop {
  width: calc(100% - 48px);
  padding-left: 40px;
  height: 56px;
  margin-bottom: 40px;
  border-radius: 28px;
  font-size: 16px;
}

.input-mobile {
  width: calc(100% - 36px);
  padding-left: 28px;
  height: 40px;
  margin-bottom: 36px;
  border-radius: 28px;
  font-size: 14px;
}

.selections-container {
  display: flex;
  justify-content: space-between;
  margin-bottom: 40px;
}

.selections-container-mobile {
  display: flex;
  flex-direction: column;
}

select {
  width: calc(50% - 20px);
  height: 56px;
  border-radius: 28px;
  font-size: 16px;
  padding-left: 40px;
  border: 1px solid #000000;
}

.select-mobile {
  width: calc(100%);
  height: 40px;
  border-radius: 28px;
  font-size: 14px;
  padding-left: 28px;
  border: 1px solid #000000;
  margin-bottom: 36px;
}

.checkboxes-container {
  margin-bottom: 50px;
}

.checkboxes-warning {
  margin-bottom: 21px;
  font-size: 16px;
}

.checkboxes-label {
  margin-right: 37px;
}

.checkboxes-input {
  width: 24px;
  height: 24px;
}

.submit-button {
  display: flex;
  justify-content: center;
}

button {
  background-color: #4B00FF;
  color: #FFFFFF;
  width: 328px;
  height: 56px;
  box-shadow: 0px 3px 6px #00000066;
  border-radius: 42px;
  opacity: 1;
  font-size: 18px;
  font-weight: 800;
}

.button-mobile {
  width: 312px;
  height: 48px;
  box-shadow: 0px 3px 6px #00000066;
  border-radius: 42px;
  opacity: 1;
  font-size: 18px;
  font-weight: 800;
}

::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: #000000;
  opacity: 1; /* Firefox */
}

:-ms-input-placeholder { /* Internet Explorer 10-11 */
  color: #000000;
}

::-ms-input-placeholder { /* Microsoft Edge */
  color: #000000;
}


textarea::-webkit-input-placeholder {
  color: #000000;
  padding-top: 19px;
  font-family: 'Montserrat', sans-serif;
}

textarea:-moz-placeholder { /* Firefox 18- */
  color: #000000;
  padding-top: 19px;
  font-family: 'Montserrat', sans-serif;
}

textarea::-moz-placeholder {  /* Firefox 19+ */
  color: #000000;
  padding-top: 19px;
  font-family: 'Montserrat', sans-serif;
}

textarea:-ms-input-placeholder {
  color: #000000;
  padding-top: 19px;
  font-family: 'Montserrat', sans-serif;
}

textarea::placeholder {
  color: #000000;
  padding-top: 19px;
  font-family: 'Montserrat', sans-serif;
}
</style>