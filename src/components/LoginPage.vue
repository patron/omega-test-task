<template>
  <div class="page-wrapper bg-blue p-t-210 p-b-100 font-manrope">
    <div class="wrapper wrapper--w680">
      <div v-if="!formSubmited" class="card card-4">
        <div class="card-body">
          <h2 class="title">Registration Form</h2>
          <form @submit.prevent="submitFunction">
            <div class="row row-space">
              <div class="col-2">
                <div class="form-group">
                  <input
                    type="text"
                    id="name"
                    v-model="loginform.name"
                    class="form-control"
                    @blur="$v.loginform.name.$touch()"
                    :class="{ error: $v.loginform.name.$error }"
                    required
                  />
                  <label class="form-control-placeholder" for="name"
                    >First Name</label
                  >
                </div>
              </div>
              <div class="col-2">
                <div class="form-group">
                  <input
                    type="text"
                    id="surname"
                    v-model="loginform.surname"
                    class="form-control"
                    @blur="$v.loginform.surname.$touch()"
                    :class="{ error: $v.loginform.surname.$error }"
                    required
                  />
                  <label class="form-control-placeholder" for="surname"
                    >Last Name</label
                  >
                </div>
              </div>
            </div>
            <div class="row row-space">
              <div class="col-4">
                <div class="form-group">
                  <input
                    type="text"
                    id="phone"
                    v-model="loginform.phone"
                    masked="true"
                    v-mask="'+## #### ######'"
                    class="form-control"
                    @blur="$v.loginform.phone.$touch()"
                    :class="{ error: $v.loginform.phone.$error }"
                    required
                  />
                  <label class="form-control-placeholder" for="phone"
                    >Phone</label
                  >
                </div>
              </div>
            </div>
            <div class="row row-space">
              <div class="col-4">
                <div class="form-group">
                  <input
                    type="text"
                    id="email"
                    v-model="loginform.email"
                    class="form-control"
                    @blur="$v.loginform.email.$touch()"
                    :class="{ error: $v.loginform.email.$error }"
                    required
                  />
                  <label class="form-control-placeholder" for="email"
                    >Email</label
                  >
                </div>
              </div>
            </div>
            <div class="p-t-8">
              <button class="btn btn--radius btn--blue" :disabled="$v.$invalid">
                Create Account
              </button>
            </div>
          </form>
        </div>
      </div>

      <transition name="fade">
        <div v-if="formSubmited" class="card card-4">
          <div class="card-body">
            <img
              alt="success"
              src="@/assets/success.svg"
              class="success-icon"
            />
            <span class="success-text">Thank you!</span>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Vuelidate from "vuelidate";
import { required, email, alpha, helpers } from "vuelidate/lib/validators";
import VueMask from "v-mask";

const phonenum = helpers.regex(
  "phonenum",
  /^\+44[-. ]?([0-9]{4})[-. ]?([0-9]{6})$/
);

Vue.use(Vuelidate);
Vue.use(VueMask);

export default {
  name: "LoginPage",
  data() {
    return {
      formSubmited: false,
      loginform: {
        name: "",
        surname: "",
        phone: "",
        email: ""
      }
    };
  },
  methods: {
    submitFunction() {
      this.formSubmited = !this.formSubmited;
      console.log("Submitted information:", this.loginform);
    }
  },
  validations: {
    loginform: {
      name: { required, alpha },
      surname: { required, alpha },
      phone: { required, phonenum },
      email: { required, email }
    }
  }
};
</script>

<style>
/* ==========================================================================
   #FONT
   ========================================================================== */

.font-manrope {
  font-family: "Manrope", "Arial", "Helvetica Neue", sans-serif;
}

/* ==========================================================================
   #GRID
   ========================================================================== */
.row {
  display: -webkit-box;
  display: -webkit-flex;
  display: -moz-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-flex-wrap: wrap;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
}

.row-space {
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  -moz-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
}

.col-2 {
  width: -webkit-calc((100% - 30px) / 2);
  width: -moz-calc((100% - 30px) / 2);
  width: calc((100% - 30px) / 2);
}

.col-4 {
  width: 100%;
}

@media (max-width: 767px) {
  .col-2 {
    width: 100%;
  }
  .col-4 {
    width: 100%;
  }
}

/* ==========================================================================
   #BOX-SIZING
   ========================================================================== */

html {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

* {
  padding: 0;
  margin: 0;
}

*,
*:before,
*:after {
  -webkit-box-sizing: inherit;
  -moz-box-sizing: inherit;
  box-sizing: inherit;
}

/* ==========================================================================
   #RESET
   ========================================================================== */
/**
 * A very simple reset that sits on top of Normalize.css.
 */
body,
h1,
h2,
h3,
h4,
h5,
h6,
blockquote,
p,
pre,
dl,
dd,
ol,
ul,
figure,
hr,
fieldset,
legend {
  margin: 0;
  padding: 0;
}

/**
 * Remove trailing margins from nested lists.
 */
li > ol,
li > ul {
  margin-bottom: 0;
}

/**
 * Remove default table spacing.
 */
table {
  border-collapse: collapse;
  border-spacing: 0;
}

/**
 * 1. Reset Chrome and Firefox behaviour which sets a `min-width: min-content;`
 *    on fieldsets.
 */
fieldset {
  min-width: 0;
  /* [1] */
  border: 0;
}

button {
  outline: none;
  background: none;
  border: none;
}

/* ==========================================================================
   #PAGE WRAPPER
   ========================================================================== */
.page-wrapper {
  min-height: 100vh;
}

body {
  font-family: "Manrope", "Arial", "Helvetica Neue", sans-serif;
  font-weight: 400;
  font-size: 14px;
}

h2 {
  font-size: 16px;
}

/* ==========================================================================
   #BACKGROUND
   ========================================================================== */
.bg-blue {
  background: #f1f5fa;
}

/* ==========================================================================
   #SPACING
   ========================================================================== */
.p-t-100 {
  padding-top: 100px;
}

.p-t-210 {
  padding-top: 210px;
}

.p-t-8 {
  padding-top: 8px;
}

.p-b-100 {
  padding-bottom: 100px;
}

/* ==========================================================================
   #WRAPPER
   ========================================================================== */
.wrapper {
  margin: 0 auto;
}

.wrapper--w960 {
  max-width: 960px;
}

.wrapper--w780 {
  max-width: 780px;
}

.wrapper--w680 {
  max-width: 680px;
}

/* ==========================================================================
   #BUTTON
   ========================================================================== */
.btn {
  display: block;
  font-weight: bold;
  font-size: 18px;
  line-height: 25px;
  padding: 13px 33px;
  cursor: pointer;
  font-size: 18px;
  color: #fff;
  font-family: "Manrope", "Arial", "Helvetica Neue", sans-serif;
  float: right;
}

.btn--radius {
  border-radius: 60px;
}

.btn--blue {
  background: #01a3ff;
}

.btn--blue:disabled {
  background: rgba(1, 163, 255, 0.25);
}

/* ==========================================================================
   #FORM
   ========================================================================== */
input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus,
textarea:-webkit-autofill,
textarea:-webkit-autofill:hover,
textarea:-webkit-autofill:focus,
select:-webkit-autofill,
select:-webkit-autofill:hover,
select:-webkit-autofill:focus {
  transition: background-color 5000s ease-in-out 0s;
}

input {
  outline: none;
  margin: 0;
  border: none;
  -webkit-box-shadow: none;
  -moz-box-shadow: none;
  box-shadow: none;
  width: 100%;
  font-size: 14px;
  font-family: inherit;
}

.form-group {
  position: relative !important;
  margin-bottom: 14px;
}

.form-control {
  line-height: 50px;
  background: #fafafa;
  box-shadow: 0px 1px 1px rgba(0, 66, 142, 0.25);
  border-radius: 10px;
  padding: 0 20px;
  font-weight: 500;
  font-size: 14px;
  color: #000;
  margin-top: 5px;
}

.form-control-placeholder {
  position: absolute;
  top: 15px;
  left: 15px;
  padding: 7px 0 0 13px;
  transition: all 200ms;
  font-size: 14px;
  color: #7188a3;
}

.form-control:focus + .form-control-placeholder,
.form-control:valid + .form-control-placeholder {
  font-size: 75%;
  transform: translate3d(0, -100%, 0);
  top: 21px;
  left: 8px;
}

.error {
  border: 1px solid #ff1a1a;
}

/* ==========================================================================
   #TITLE
   ========================================================================== */
.title {
  text-align: center;
  font-size: 16px;
  color: #333;
  font-weight: 500;
  margin-bottom: 28px;
}

/* ==========================================================================
   #CARD
   ========================================================================== */

.card-4 .card-body {
  padding: 57px 65px;
  padding-bottom: 65px;
}

@media (max-width: 767px) {
  .card-4 .card-body {
    padding: 50px 40px;
  }
}

.success-icon {
  display: block;
  margin: 0 auto;
}

.success-text {
  display: block;
  font-weight: bold;
  font-size: 18px;
  line-height: 25px;
  text-align: center;
  padding-top: 16px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
