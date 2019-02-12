<template>
  <section class="hero is-fullheight">
    <div class="hero-body">
      <div class="container has-text-centered">
        <div class="column is-4 is-offset-4">
          <h3 class="title has-text-grey">LER Corp</h3>
          <p class="subtitle has-text-grey">When your fantasy become reality.</p>
          <div class="box">
            <figure class="avatar">
              <img src="https://placehold.it/128x128">
            </figure>
            <form method="post" @submit.prevent="savelogin">
              <div class="field">
                <div class="control">
                  <input class="input is-large" type="text" placeholder="Your Username" name="username" v-model="v_username" v-validate="'required'" autofocus="">
                </div>
                <p v-show="errors.has('username')" class="help is-danger">{{ errors.first('username') }}</p>
              </div>

              <div class="field">
                <div class="control">
                  <input class="input is-large" type="password" placeholder="Your Password" name="password" v-model="v_password" v-validate="'required'"> 
                </div>
                <p v-show="errors.has('password')" class="help is-danger">{{ errors.first('password') }}</p>
              </div>
              <div class="field">
                <label class="checkbox">
                  <input type="checkbox">
                  Remember me
                </label>
              </div>
              <button type="submit" class="button is-block is-info is-large is-fullwidth">Login</button>
            </form>
          </div>
          <p class="has-text-grey">
            <nuxt-link to="">Sign Up</nuxt-link>
            <nuxt-link to="">Forgot Password</nuxt-link>
            <nuxt-link to="">Need Help?</nuxt-link>
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
  import Vue from 'vue';
  import VeeValidate from 'vee-validate';
  Vue.use(VeeValidate);
  import swal from 'sweetalert';
  export default {
    components: {

    },
    created() {

    },
    data() {
      return {
        v_username: '',
        v_password: ''
      }
    },
    methods: {
      resetform() {
        this.v_username = '';
        this.v_password = '';
        this.$nextTick(() => this.$validator.reset())
      },
      savelogin() {
        this.storelogin();
      },
      storelogin() {
        this.$validator.validateAll().then(async valid => {
          if (valid) {
              if(this.v_username=='peler' && this.v_password=='admin') {
                swal(
                  'Hai '+this.v_username,
                  'Anda berhasil login.'
                )
                this.$router.push('/home');
              } else {
                swal(
                  'Maaf '+this.v_username,
                  'Username/password salah.'
                )
                //this.$refs.username.$el.focus()
                this.resetform();
              }
          }
          
        });
      }
    }

  }
</script>