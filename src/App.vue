<template>
  <div class="container" id="app">
    <div class="row">
      <div class="col-6 offset-3">
        <div class="progress">
          <div class="progress-bar" :style="progressWidth"></div>
        </div>
      </div>

      <form class="col-6 offset-3" action="/">
        <div class="form-group" v-for="(field) in info">
          <label :for="field.name">{{ field.name }}: </label>
          <i class="fas fa-check bg-success"></i>
          <input type="text" class="form-control" :id="field.name" v-model="isValid">
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
      ],
      progress: 0,
    }
  },
  methods: {

  },
  computed: {
    progressWidth() {
      return {
        width: this.progress + '%'
      };
    }
  },
  watch: {
    isValid(value, regExp) {
      if (value.match(regExp)) {
        this.progress =+ 20;
      }
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