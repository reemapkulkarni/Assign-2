<template>

    <div class="container-fluid">

        <form  class="form-group" @submit.prevent>
      <h2 style="text-align: center; font-weight: bold; font-size: 45px">
        Login Form
      </h2>
      <div class="row">

          <div class="col-md-12">
              <label for="username">Username</label>
              <input type="text" class="form-control" placeholder="Enter Username" v-model="username"  />
          </div>

          <div class="col-md-12">
              <label for="password">Password</label>
              <input type="password" class="form-control" placeholder="Enter Password" v-model="password" />
          </div>

          <div class="col-md-12" style="text-align:center; margin-top:20px;">
          <button type="submit" class="btn btn-primary" v-on:click="profile()">Login</button>

          </div>
      </div>
        </form>
    </div>

</template>
<script>
import axios from 'axios'
export default {
  name: 'LoginPage',
  data () {
    return {
      error: [],
      username: null,
      password: null
    }
  },
  methods: {
    profile () {
      const url = 'http://localhost:4887/o/loginStudentData'

      axios
        .post(url, {
          username: this.username,
          password: this.password
        })
        .then((response) => {
          console.log(response.data)
          this.value = response.data
          if (response.data === true) {
            alert('Login Successful')
            console.log(response.data)
            this.$router.push({ name: 'profile' })
            console.log('if')
          } else {
            console.log('else')
            alert('Failed')
          }
        })
        .catch(function (err) {
          console.error(err)
        })
    }
  }
}
</script>
