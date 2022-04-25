<template>
  <div class="container-fluid">
    <form class="form-group" @submit.prevent>
      <h2 style="text-align: center; font-weight: bold; font-size: 40px">
        Update Profile
      </h2>

      <div class="row">
        <div class="col-md-12">
          <button
            type="submit"
            class="btn btn-primary"
            v-on:click="loaddata()"
          >
            Load Data
          </button>
        </div>
        <div class="col-md-12">
          <label></label>
          <input
            type="text"
            class="form-control"
            placeholder="Enter User_id to update profile"
            v-model.number="user_id"
          />
        </div>

        <div class="col-md-6">
          <label for="fname"></label>
          <input
            type="text"
            class="form-control"
            placeholder="Enter First name"
            v-model="fname"
          />
        </div>

        <div class="col-md-6">
          <label for="lname"></label>
          <input
            type="text"
            class="form-control"
            placeholder="Enter last name"
            v-model="lname"
          />
        </div>

        <div class="col-md-6">
          <label for="email"></label>
          <input
            type="email"
            class="form-control"
            placeholder="Enter Email"
            v-model="email"
          />
        </div>

        <div class="col-md-6">
          <label for="mobile"></label>
          <input
            type="text"
            class="form-control"
            placeholder="Enter mobile no."
            v-model="mobile"
          />
        </div>

        <div class="col-md-6">
          <label for="username"></label>
          <input
            type="text"
            class="form-control"
            placeholder="Enter username"
            v-model="username"
          />
        </div>

        <div class="col-md-6">
          <label for="password"></label>
          <input
            type="password"
            class="form-control"
            placeholder="Enter password"
            v-model="password"
          />
        </div>
      </div>
      <div class="col-md-12" style="text-align: center; margin-top: 20px">
        <button type="submit" class="btn btn-primary" v-on:click="update()">Update</button>
      </div>
    </form>
    <div>
      <table class="table">
        <thead>
          <tr>
            <th scope="col">User_ID</th>
            <th scope="col">FirstName</th>
            <th scope="col">LastName</th>
            <th scope="col">Email</th>
            <th scope="col">Mobile</th>
            <th scope="col">Username</th>
            <th scope="col">Passord</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="post in values" :key="post.user_id">
            <td>{{ post.user_id }}</td>
            <td>{{ post.fname }}</td>
            <td>{{ post.lname }}</td>
            <td>{{ post.email }}</td>
            <td>{{ post.mobile }}</td>
            <td>{{ post.username }}</td>
            <td>{{ post.password }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'ProfilePage',
  data () {
    return {
      user_id: [],
      fname: '',
      lname: '',
      email: '',
      mobile: '',
      username: '',
      password: '',
      values: []
    }
  },
  methods: {
    getdata () {
      console.warn('values=', this.user_id)
    },
    hello () {
      console.log('id', this.user_id)
      console.log('user_id', typeof this.user_id)
    },

    update () {
      const url = 'http://localhost:4887/o/updateStudentData'
      axios
        .post(url, {
          fname: this.fname,
          lname: this.lname,
          email: this.email,
          mobile: this.mobile,
          username: this.username,
          password: this.password,
          user_id: this.user_id
        })
        .then((response) => {
          console.log(response.data)
          this.value = response.data
        })
        .catch(function (err) {
          console.error(err)
        })
    },
    loaddata () {
      axios
        .post('http://localhost:4887/o/getStudentData', {})
        .then((response) => {
          this.values = response.data
          console.log('response data:', response.data)
        })
        .catch(function (err) {
          console.error(err)
          // reject (new Error('failed'))
        })
    }
  }

}
</script>
