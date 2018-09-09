<template>
  <div class="container" id="app">
    <div class="row">
      <div class="col-6 offset-3">
        <div class="progress">
          <div class="progress-bar" :style="progressWidth"></div>
        </div>
      </div>

      <form class="col-6 offset-3" @submit.prevent="formSubmited = true" v-if="!formSubmited">
        <div class="form-group"
             v-for="(field, index) in info"
             :key="field.name"
        >
          <label :for="field.name">{{ field.name }}: </label>
          <span class="fa"
                v-if="controls[index].activated"
                :class="controls[index].error ?
                'fa-exclamation-circle text-danger' :
                'fa-check-circle text-success'"
          ></span>
          <input type="text"
                 class="form-control"
                 :id="field.name"
                 :value="field.value"
                 @input="onInput(index, $event.target.value)"
          >
        </div>

        <button type="submit"
                class="btn btn-primary"
                :disabled="done < info.length"
        >Submit
        </button>
      </form>

      <div v-else>
        <table class="table table-bordered">
          <tr v-for="(field, index) in info">
            <td>{{ field.name }}</td>
            <td>{{ field.value }}</td>
          </tr>
        </table>
      </div>
    </div>

    <div class="sample row">
      <form class="col-6 offset-3">
        <div class="content alert alert-info" @scroll="onScroll">
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
          <p>This text no one reads. This text no one reads. This text no one reads.</p>
        </div>

        <div v-if="scrolled">
          <div class="form-check">
            <label class="form-check-label">
              <input class="form-check-input" type="checkbox" v-model="flags.agree">
              Согласен
            </label>
          </div>
          <div class="form-check">
            <label class="form-check-label">
              <input class="form-check-input" type="checkbox" v-model="flags.spam">
              Хочу получать спам
            </label>
          </div>
          <div v-show="flags.spam">
            <div class="form-check">
              <label class="form-check-label">
                <input class="form-check-input" type="radio" value="phone" v-model="spam">
                Phone
              </label>
            </div>
            <div class="form-check">
              <label class="form-check-label">
                <input class="form-check-input" type="radio" value="email" v-model="spam">
                Email
              </label>
            </div>
          </div>
          <hr>
          <button class="btn btn-primary">
            Send Data
          </button>
        </div>
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
          },
          {
            name: 'Phone',
            value: '',
            pattern: /^[0-9]{7,14}$/,
          },
          {
            name: 'Email',
            value: '',
            pattern: /.+/,
          },
          {
            name: 'Some Field 1',
            value: '',
            pattern: /.+/,
          },
          {
            name: 'Some field 2',
            value: '',
            pattern: /.+/,
          }
        ],
        controls: [],
        formSubmited: false,
        scrolled: false,
        flags: {
          agree: false,
          spam: false
        },
        spam: 'phone'
      }
    },
    beforeMount() {
      for (let i = 0; i < this.info.length; i++) {
        this.controls.push({
          error: !this.info[i].pattern.test(this.info[i].value),
          activated: this.info[i].value !== ''
        });
      }
    },
    methods: {
      onInput(index, value) {
        let data = this.info[index];
        let control = this.controls[index];

        data.value = value;
        control.error = !data.pattern.test(value);
        control.activated = true
      },
      onScroll(e) {
        if (e.target.scrollHeight - e.target.clientHeight - e.target.scrollTop < 10) {
          this.scrolled = true;
          console.log(this.flags.spam);
        }
      }
    },
    computed: {
      done() {
        let done = 0;

        for (let i = 0; i < this.info.length; i++) {
          if (!this.controls[i].error) {
            done++;
          }
        }

        return done;
      },
      progressWidth() {
        return {
          width: (this.done / this.info.length * 100) + '%'
        }
      }
    }
  }
</script>

<style scoped>
  label {
    margin-right: 5px;
  }

  .content {
    height: 300px;
    overflow: auto;
  }
</style>