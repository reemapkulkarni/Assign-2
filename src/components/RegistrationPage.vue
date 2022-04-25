<template>
<div class="form">
  <div class="vue-tempalte">
    <div class="hero">
    <form @submit.prevent="validateBeforeSubmit" >
      <p></p>
      <br />
      <br />

      <h1>Register</h1>

      <div class="form-group">
        <label>First Name <span class="text-danger">*</span></label>
        <input
          type="text"
          v-validate="'required'"
          :class="{ 'input form-control': true }"
          name="firstname"
          pattern="[A-Za-z]*"
          v-model="firstName"
          placeholder="Enter firstname"
          class="form-control form-control-lg"
          required="required"
        />
        <!-- <span class="text-danger" v-if="errors.has('firstname')"><small>{{ errors.first('firstname') }}</small></span> -->

      </div>
      <div class="form-group">
        <label>Last Name<span class="text-danger">*</span></label>
        <input
          type="text"
          v-validate="'required'"
          :class="{ 'input form-control': true }"
          pattern="[A-Za-z]*"
          v-model="lastName"
          placeholder="Enter lastname"
          class="form-control form-control-lg"
          required="required"
        />
        <!-- <span class="text-danger" v-if="errors.has('lastname')"><small>{{ errors.first('lastname') }}</small></span> -->
      </div>
       <!-- <div class="form-group">
>                <label class>Gender<span class="text-danger">*</span></label>
>                  <select v-model="gender" @click="onChange"  v-validate="'required'"  :class="{ 'input form-control': true }" placeholder="select gender"  class="form-control form-control-lg">
>                    <option>Please Select One</option>
>                    <option value="">Male</option>
>                    <option value="">Female</option>
>                     <option v-if="item in filters" :value="item">{{item}}</option>
>                  </select>
>                <span class="text-danger" v-if="errors.has('gender')"><small>{{ errors.first('gender') }}</small></span>
>      </div> -->

       <!-- <div class="form-group">
>      <label for="gender">Gender:</label>
>      <select v-model="gender" name="gender" v-validate="'required'" :class="{'form-control': true, 'error': errors.has('gender')}">
>        <option>Female</option>
>        <option>Male</option>
>      </select>
>      <span v-show="errors.has('gender')" class="text-danger">{{ errors.first('gender') }}</span>
>    </div> -->
    <!-- <div>
>      <label for="gender">Gender</label>
>      <select name="gender" v-model="gender">
>    <option disabled selected>Please Choose</option>
>      {{gender}}
>  </select>
>      <span v-if="'gender' in validations && validations.gender">Green means go</span>
>      <span v-if="'gender' in validations && !validations.gender">Please select a gender</span>
>    </div> -->
   <!-- <div class="form-group" :class="{error: validation.hasError('gender')}">
>      <div class="label">* Gender</div>
>      <div class="content">
>        <label>
>          <input type="radio" class="form-control" name="gender" @click= value="male" v-model="gender" />
>          Male
>        </label>
>        <label>
>          <input type="radio" class="form-control" name="gender" value="female" v-model="gender" />
>          Female
>        </label>
>      </div>
>      <div class="message">{{ validation.firstError('gender') }}</div>
>    </div> -->

      <div class="form-group">
        <label>Email Id<span class="text-danger">*</span></label>
        <input
          type="email"
          v-validate="'required'"
          :class="{ 'input form-control': true }"
          v-model="email"
          placeholder="Enter email"
          class="form-control form-control-lg"
        />
        <!-- <span class="text-danger" v-if="errors.has('email')"><small>{{ errors.first('email') }}</small></span> -->
      </div>

      <div class="form-group">
        <label>Mobile<span class="text-danger">*</span></label>
        <input type="text" v-validate="'required'"
        :class="{'input-form-control':true}"
        v-model="mobile"
        placeholder="Enter Mobile number"
        class="form-control form-control-lg"
        />
        <!-- <span class="text-danger" v-if="errors.has('mobile')"><small>{{errors.first('mobile') }}</small></span> -->
      </div>

      <div class="form-group">
        <label>Username<span class="text-danger">*</span></label>
        <input type="text" v-validate="'required'"
        :class="{'input-form-control':true}"
        v-model="username"
        placeholder="Enter Username"
        class="form-control form-control-lg"
        />
        <!-- <span class="text-danger" v-if="errors.has('username')"><small>{{errors.first('username') }}</small></span> -->
      </div>

      <div class="form-group">
        <label>Password<span class="text-danger">*</span></label>
        <input
          type="password"
          v-validate="'required'"
          :class="{ 'input form-control': true }"
          v-model="password"
          placeholder="Enter password"
          class="form-control form-control-lg"
          pattern="(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,}"
          required="required"
        />
         <!-- <span class="text-danger" v-if="errors.has('password')"><small>{{ errors.first('password') }}</small></span> -->
      </div>
      <p></p>
      <button
        type="submit"
        class="btn btn-primary"
        v-on:click="register()"
      >
        Register
      </button>

      <p class="forgot-password text-right">
        Already registered
        <router-link :to="{ name: 'login' }">login?</router-link>
      </p>
    </form>
  </div>
  </div>
</div>
</template>

<script>
import axios from 'axios'
import VeeValidate from 'vee-validate'
import Vue from 'vue'
Vue.use(VeeValidate)

export default {
  name: 'RegistrationPage',
  data () {
    return {
      error: [],
      firstName: '',
      lastName: '',
      email: '',
      password: ''
    }
  },

  computed: {
    isComplete () {
      return this.firstName && this.lastName && this.email && this.password
    }
  },
  methods: {
    validateBeforeSubmit () {
      this.$validator.validateAll().then((result) => {
        if (result) {
          alert('Form Submitted!')
        }
      })
    },
    // onChange(e) {
    //           console.log(e.target.value);
    //       },

    register () {
      const url = 'http://localhost:4887/o/setStudentData'
      axios
        .post(url, {
          firstname: this.firstName,
          lastname: this.lastName,
          // gender: this.gender,
          email: this.email,
          password: this.password
        })
        .then((response) => {
          console.log(response.data)
          this.value = response.data
          if (response.data === true) {
            alert('Registration Successful')
            this.$router.push({ name: 'login' })
          } else {
            alert('Please enter data')
          }
        })
        .catch(function (err) {
          console.error(err)
        })
      console.log(this.firstName)
    }
  }
  //  gender(newValue) {
  //   this.validations.gender = this.genders.includes(newValue);
  // }
}
</script>
