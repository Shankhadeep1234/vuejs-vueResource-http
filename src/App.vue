<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1>Http</h1>
        <div class="form-group">
          <label for="">Username</label>
          <input class="form-control" type="text" v-model="user.userName" />
        </div>
        <div class="form-group">
          <label for="">Mail</label>
          <input class="form-control" type="text" v-model="user.email" />
        </div>
        <button class="btn btn-primary" @click="submit">Submit</button>
        <hr />
        <button class="btn btn-primary" @click="fetchData">Get Data</button>
        <br />
        <ul class="list-group">
          <br />
          <li
            class="list-group-item"
            v-for="(user, index) in users"
            :key="index"
          >
            {{ user.userName }} - {{ user.email }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        userName: '',
        email: '',
      },
      users: [],
    };
  },
  methods: {
    submit() {
      this.$http
        .post('', this.user)
        .then((response) => {
          console.log(response);
        })
        .catch((err) => {
          console.log(err);
        });

      this.user.userName = '';
      this.user.email = '';
    },
    fetchData() {
      this.$http
        .get('https://vuejs-http-a11f4.firebaseio.com/data.json')
        .then((response) => {
          return response.json();
        })
        .then((data) => {
          const resultArray = [];
          for (let key in data) {
            resultArray.push(data[key]);
          }
          this.users = resultArray;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style></style>
