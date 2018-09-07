<template>
  <div class="container" id="app">
    <div class="row">
      <div class="col-6 offset-3">
        <div class="progress">
          <div class="progress-bar" :style="progressWidth"></div>
        </div>
      </div>

      <form class="col-6 offset-3" action="/">
        <div class="form-group"
             v-for="(field) in info"
             :key="field.name"
        >
          <label :for="field.name">{{ field.name }}: </label>
          <i class="fas fa-check"></i>
          <input type="text"
                 class="form-control"
                 :id="field.name"
                 v-model="field.value"
                 @input="isValid(field.value, field.pattern, field.progress)"
          >
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
            pattern: /^[a-zA-z]{2,30}$/,
            progress: false,
          },
          {
            name: 'Phone',
            value: '',
            pattern: /^[0-9]{7,14}$/,
            progress: false,
          },
          {
            name: 'Email',
            value: '',
            pattern: /.+/,
            progress: false,
          },
          {
            name: 'Some Field 1',
            value: '',
            pattern: /.+/,
            progress: false,
          },
          {
            name: 'Some field 2',
            value: '',
            pattern: /.+/,
            progress: false,
          }
        ],

        successClass: ['fa-check', 'bg-success'],
        errorClass: ['fa-times', 'bg-danger'],
        defaultClass: 'hidden',
        progress: 0,
      }
    },
    methods: {
      isValid(value, pattern, progress) {
        if (value.match(pattern) && !progress) {
          progress = true;
          this.progress += 20;
        } else {
          progress = false;
          this.progress -= 20;
        }
      }
    },
    computed: {
      progressWidth() {
        return {
          width: this.progress + '%'
        };
      },
      // className() {
      //   if () {
      //     return this.successClass
      //   } else if () {
      //     return this.errorClass
      //   } else {
      //     return this.defaultClass
      //   }
      // }
    },
    watch: {

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