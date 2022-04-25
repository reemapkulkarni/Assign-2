<template>

        <div class ="container-fluid">
            <form class="form-group">
                <h2 style="font-weight: bold; font-size: 45px">
                    Register
                </h2>

                <div class="row">
                <div class="col-md-6">
                <label for="fname"><strong>FirstName :</strong></label>
                <input
                type="text"
                class="form-control"
                placeholder="Enter First Name"
                v-model="fname"
                />
                  <!-- <span>{{v.errors[0]}}</span> -->
                </div>

            <div class="col-md-6">
                <label for="lname"><strong>LastName : </strong></label>
                <input
                type="text"
                class="form-control"
                placeholder="Enter Last Name"
                v-model="lname"
                />
            </div>

            <div class="col-md-6">
            <label for="email"><strong> Email : </strong></label>
            <input
              type="text"
              class="form-control"
              placeholder="Enter Email"
              v-model="email"
            />
            </div>

            <div class="col-md-6">
            <label for="mobile"><strong>Mobile No. : </strong></label>
            <input
              type="text"
              class="form-control"
              placeholder="Enter Mobile No."
              v-model="mobile"
            />
            </div>

            <div class="col-md-6">
            <label for="username"><strong> Username: </strong></label>
            <input
              type="text"
              class="form-control"
              placeholder="Enter Username"
              v-model="username"
            />
            </div>

            <div class="col-md-6">
            <label for="password"><strong>Password : </strong></label>
            <input
              type="password"
              class="form-control"
              placeholder="Enter Password"
              v-model="password"
            />
            </div>

            <div class="col-md-12" style="text-align: center; margin-top: 20px">
            <button
              type="submit"
              class="btn btn-primary"
              v-on:click="submit()">Submit
            </button>
          </div>

        <div class="col-md-12" style="text-align: center">
            Already have an account?<br /><router-link to="/LoginPage"
              >Login here</router-link>
        </div>

        </div>
        </form>
        </div>

</template>

<script>
import axios from 'axios'
// import VeeValidate from 'vee-validate'
// import Vue from 'vue'
// Vue.use(VeeValidate)

export default {
  name: 'RegistrationPage',
  data () {
    return {
      error: [],
      fname: '',
      lname: '',
      email: '',
      mobile: '',
      username: '',
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

    submit () {
      const url = 'http://localhost:4887/o/setStudentData'
      axios
        .post(url, {
          fname: this.fname,
          lname: this.lname,
          // gender: this.gender,
          email: this.email,
          mobile: this.mobile,
          username: this.username,
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
      console.log(this.fname)
    }
  }
  //  gender(newValue) {
  //   this.validations.gender = this.genders.includes(newValue);
  // }
}
</script>
