<template>
  <div class="container" id="app">
    <div class="row">
      <div class="col-6 offset-3">
        <div class="progress">
          <div class="progress-bar" :style="progress"></div>
        </div>
      </div>

      <form class="col-6 offset-3" action="/">
        <div class="form-group">
          <label for="name">Name: </label>
          <i class="fas fa-check bg-success"></i>
          <input type="text" class="form-control" id="name" v-model="info[0].value">
        </div>

        <div class="form-group">
          <label for="phone">Phone: </label>
          <i class="fas fa-check bg-success"></i>
          <input type="text" class="form-control" id="phone" v-model="info[1].value">
        </div>

        <div class="form-group">
          <label for="email">Email: </label>
          <i class="fas fa-check"></i>
          <input type="text" class="form-control" id="email" v-model="info[2].value">
        </div>

        <div class="form-group">
          <label for="sf1">Some Field 1: </label>
          <i class="fas fa-check bg-success"></i>
          <input type="text" class="form-control" id="sf1" v-model="info[3].value">
        </div>

        <div class="form-group">
          <label for="sf2">Some Field 2: </label>
          <i class="fas fa-check bg-success"></i>
          <input type="text" class="form-control" id="sf2" v-model="info[4].value">
        </div>

        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      info: [
        {
          name: 'Name',
          value: '',
          pattern: /^[a-zA-z]{2,30}$/
        },
        {
          name: 'Phone',
          value: '',
          pattern: /^[0-9]{7,14}$/
        },
        {
          name: 'Email',
          value: '',
          pattern: /.+/
        },
        {
          name: 'Some Field 1',
          value: '',
          pattern: /.+/
        },
        {
          name: 'Some field 2',
          value: '',
          pattern: /.+/
        }
      ]
    }
  }
}
</script>

<style scoped>
  label {
    margin-right: 5px;
  }

  .fas {
    padding: 3px;
    font-size: 8px;
    color: #fff;
    border-radius: 50%;
  }
</style>