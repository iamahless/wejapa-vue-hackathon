<template>
  <div class="o-page o-page--center">
    <div class="o-page__card">
      <div class="c-card c-card--center">
        <span class="c-icon c-icon--large u-mb-small">
          <svg width="40" height="40" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
            <g clip-path="url(#clip0)">
              <path fill-rule="evenodd" clip-rule="evenodd"
                d="M39.562 13.8603L30.1611 21.727L20.7603 12.8614L9.97692 21.9767L5.27649 17.4815L21.0368 3.99576L30.4376 12.9862L35.2763 8.99047L39.9768 13.4857L39.562 13.8603Z"
                fill="#FED430"></path>
              <path fill-rule="evenodd" clip-rule="evenodd"
                d="M21.1749 16.982L35.2762 30.4677L24.9076 39.3333L20.3454 34.9629L25.3224 30.7174L20.2072 25.7227L15.3685 21.1026L20.6219 16.6074L21.1749 16.982ZM17.4422 28.2201L4.86163 38.8338L0.0229492 34.2137L13.0183 23.1005L17.857 27.7206L17.4422 28.2201Z"
                fill="#1DBF69"></path>
              <path fill-rule="evenodd" clip-rule="evenodd"
                d="M30.4376 0C31.82 0 32.926 0.499471 33.7555 1.37354C34.585 2.12275 34.9997 3.12169 34.9997 4.37037C34.8615 5.49418 34.3085 6.49312 33.479 7.24233C32.6495 7.99153 31.4053 8.36614 30.1611 8.36614C28.9168 8.36614 27.6726 7.7418 26.9813 6.99259C26.1519 6.24339 25.5989 5.11958 25.7371 3.99577C25.7371 2.87196 26.2901 1.87302 27.1196 1.12381C28.0873 0.374603 29.1933 0 30.4376 0Z"
                fill="black"></path>
            </g>
            <defs>
              <clipPath id="clip0">
                <rect width="40" height="39.3333" fill="white"></rect>
              </clipPath>
            </defs>
          </svg>
        </span>

        <h4 class="u-mb-medium">Welcome Back :)</h4>
        <form @submit.prevent="loginUser">
          <div class="c-field">
            <label class="c-field__label">Email Address</label>
            <input class="c-input u-mb-small" type="email" placeholder="e.g. adam@sandler.com" required=""
              autocomplete="off" v-model="email" />
          </div>

          <div class="c-field">
            <label class="c-field__label">Password</label>
            <input class="c-input u-mb-small" type="password" placeholder="Numbers, Pharagraphs Only" required=""
              autocomplete="off" v-model="password" />
          </div>

          <button class="c-btn c-btn--fullwidth c-btn--info">
            <template v-if="isLoading">
                <Loader />
              </template>
              <template v-else>
                Log in
              </template>
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import Loader from '../assets/loader.svg'

  export default {
    name: 'Login',
    data() {
      return {
        email: '',
        password: '',
        isLoading: false
      };
    },
    components: {
      Loader,
    },
    methods: {
      loginUser() {
        const {
          email,
          password
        } = this;
        if (email === '' || password === '') {
          return this.$toastr.e('An email or password must be present');
        }
        this.isLoading = true

        this.$store.dispatch('loginUser', {
          email,
          password
        })
        .then((resp) => {
          this.isLoading = false
          console.log(resp)
          this.$router.push({ name:'Jobs' })
        })
        .catch((err) => {
          this.isLoading = false
          console.log(err)
          return this.$toastr.e('Invaild email or password provided');
          // return this.$toastr.e(err.message);
        });
      },
    },
  };
</script>