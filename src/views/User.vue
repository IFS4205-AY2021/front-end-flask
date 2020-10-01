<template>
  <div class="home">
    <div class="columns">
      <div class="column is-3 is-offset-2">
        <NavBar>
        </NavBar>
        <h1 class="title">Tracer - User</h1>
      </div>
    </div>

    <hr>
    <div class="columns">
      <div class="column is-3 is-offset-2">
        <form v-on:submit.prevent="adduser">
          <h2 class="subtitle">Add User</h2>

          <div class="field">
            <label class="label">Name</label>
            <div class="control">
              <input class="input" type="text" v-model="name">
            </div>
          </div>

          <div class="field">
            <label class="label">Phone</label>
            <div class="control">
              <input class="input" type="text" v-model="phone">
            </div>
          </div>

          <div class="field">
            <label class="label">Age</label>
            <div class="control">
              <input class="input" type="text" v-model="age">
            </div>
          </div>

          <div class="field">
            <label class="label">address</label>
            <div class="control">
              <input class="input" type="text" v-model="address">
            </div>
          </div>

          <div class="field">
            <label class="label">Location</label>
            <div class="control">
              <input class="input" type="text" v-model="location">
            </div>
          </div>

          <div class="field">
            <label class="label">test_result</label>
            <div class="control">
              <div class="select">
                <select v-model="test_result">
                  <option value="True">Positive</option>
                  <option value="False">Negative</option>
                  <option value="None">Unknown</option>
                </select>
              </div>
            </div>
          </div>

          <div class="field">
            <label class="label">Encryption_keys</label>
            <div class="control">
              <input class="input" type="text" v-model="encryption_keys">
            </div>
          </div>


          <div class="field">
            <div class="control">
              <button class="button is-link">Add</button>
            </div>
          </div>
        </form>
      </div>

      <div class="column is-6">
        <h2 class="subtitle">Users</h2>

        <div class="todo">
          <div class="card" v-for="user in users" v-bind:key="user.id">
            <div class="card-content">{{ user.name }}</div>

            <!-- <footer class="card-footer">
              <a class="card-footer-item" @click="deleteUser(user.id)">Delete</a>
            </footer> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const API_URL = 'http://127.0.0.1:8000/'
import axios from 'axios'
import NavBar from '../components/Navbar'
import { mapState } from 'vuex'
import { getAPI } from '../axios-api'
import '../../node_modules/bulma'
export default {
  name: 'user',
  components: {
    NavBar
  },
  onIdle () {
    this.$store.dispatch('userLogout')
      .then(() => {
        this.$router.push({ name: 'login' })
      })
  },
  data () {
    return {
      users: [],
      name: '',
      phone: '',
      age: '',
      address: '',
      location: '',
      test_result: false,
      encryption_keys: ''
    }
  },
  computed: mapState(['APIData']),
  mounted () {
    this.getusers()
  },
  methods: {
    getusers() {
      axios({
        method: 'get',
        url: API_URL + 'api/user/',
        headers: {
            Authorization: `Bearer ${this.$store.state.accessToken}`
        }
      }).then(response => this.users = response.data)
      console.log(this.users)
    },
    adduser() {
      if (this.name) {
        axios({
          method: 'post',
          url: API_URL + 'api/user/',
          headers: {
            Authorization: `Bearer ${this.$store.state.accessToken}`
          },
          data: {
            name: this.name,
            phone: this.phone,
            age: this.age,
            address: this.address,
            location: this.location,
            test_result: this.test_result,
            encryption_keys: this.encryption_keys
          }
        }).then((response) => {
            let newuser = {
                'id': response.data.id,
                'name': response.data.name,
                'phone': response.data.phone,
                'age': response.data.age,
                'address': response.data.address,
                'location': response.data.location,
                'test_result': response.data.test_result,
                'encryption_keys': response.data.encryption_keys
            }
            this.users.push(newuser)
            this.name = '',
            this.phone = '',
            this.age = '',
            this.address = '',
            this.location = '',
            this.test_result = false,
            this.encryption_keys = ''
        }).catch((error) => {
          console.log(error)
        })
      }
    }
    // deleteUser(user_id) {
    //   const user = this.users.filter(user => user.id === user_id)[0]
    //   axios({
    //     method: 'put',
    //     url: API_URL + 'api/user/' + user_id + '/',
    //     headers: {
    //       'Content-Type': 'application/json',
    //     },
    //     data: {
    //       status: status,
    //       description: description
    //     },
    //     auth: {
    //       username: 'adm',
    //       password: 'adminuser'
    //     }
    //   }).then(() => {
    //     user.status = status
    //   })
    // }
  },
  created () {
    getAPI.get('api/user/', { headers: { Authorization: `Bearer ${this.$store.state.accessToken}` } })
      .then(response => {
        this.users = response.data
      })
      .catch(err => {
        console.log(err)
      })
  }
}
</script>

<style lang="scss">
.select, select {
  width: 100%;
}
.card {
  margin-bottom: 20px;
}
.done {
  opacity: 0.3;
}
</style>