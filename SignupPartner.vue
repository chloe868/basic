<template>
  <div class="row holder">
    <div class="col-md-6 col-lg-4 mx-auto signup-container">
      <div class="signup-wrapper">
        <div class="signup-header" style="margin-top: 50px;">
          <img src="../../../assets/img/logo.png" v-on:click="redirect('/')">
        </div>
        <span style="width:100%;float:left;text-align:center;font-size:20px;margin-bottom:20px;">
          Register as partner to <b class="text-primary">{{common.APP_NAME}}</b>
        </span>
        <div class="signup-holder">
          <div class="login-message-holder login-spacer text-center" v-if="errorMessage !== null">
            <span class="text-danger text-center"><b>Oops!</b> {{errorMessage}}</span>
          </div>
          <div class="login-message-holder login-spacer text-center" v-if="errorMessage2 !== null">
            <span class="text-danger text-center"><b>Oops!</b> {{errorMessage2}}</span>
          </div>
          <div class="login-message-holder login-spacer text-center" v-if="errorMessage3 !== null">
            <span class="text-danger text-center"><b>Oops!</b> {{errorMessage3}}</span>
          </div>
          <div class="login-message-holder login-spacer text-center" v-if="errorMessage4 !== null">
            <span class="text-danger text-center"><b>Oops!</b> {{errorMessage4}}</span>
          </div>
          <div class="login-message-holder login-spacer text-center" v-if="errorMessage5 !== null">
            <span class="text-danger text-center"><b>Oops!</b> {{errorMessage5}}</span>
          </div>
          <div class="login-message-holder login-spacer text-center" v-if="errorMessage6 !== null">
            <span class="text-danger text-center"><b>Oops!</b> {{errorMessage6}}</span>
          </div>
          <div class="login-message-holder login-spacer text-center" v-if="errorMessage7 !== null">
            <span class="text-danger text-center"><b>Oops!</b> {{errorMessage7}}</span>
          </div>
          <div class="login-message-holder login-spacer text-center" v-if="successMessage !== null">
            <span class="text-success text-center"><b>Wow!</b> {{successMessage}}</span>
          </div>
          <div>
            <div class="input-group login-spacer">
              <span class="input-group-addon" id="addon-1"><i class="fa fa-user"></i></span>
              <input v-on:keyup="validate('username')" type="text" class="form-control form-control-login" placeholder="Username" aria-describedby="addon-1" v-model="username">
            </div>
            <div class="input-group login-spacer">
              <span class="input-group-addon" id="addon-1"><i class="fa fa-envelope"></i></span>
              <input v-on:keyup="validate('email')" type="text" class="form-control form-control-login" placeholder="Email" aria-describedby="addon-1" v-model="email">
            </div>
            <div class="input-group">
              <span class="input-group-addon" id="addon-2"><i class="fa fa-key"></i></span>
                <input v-on:keyup="validate('password')" style="border-right-style: none;" class="form-control form-control-login" :type="visibility" placeholder="Password" aria-describedby="addon-2" v-model="password">
                <span style="background: white;" class="input-group-addon">
                  <i v-if="visibility == 'password'" @click="showPassword('password')" class="fa fa-eye" aria-hidden="true"></i>
                  <i v-if="visibility == 'text'" @click="hidePassword('password')" class="fa fa-eye-slash" aria-hidden="true"></i>
                </span>
            </div>
            <div class="input-group login-spacer">
              <span class="input-group-addon" id="addon-2"><i class="fa fa-key"></i></span>
                <input v-on:keyup="validate('cpassword')" style="border-right-style: none;" class="form-control form-control-login" :type="visibilityC" placeholder="Confirm Password" aria-describedby="addon-2" v-model="cpassword">
                <span style="background: white;" class="input-group-addon">
                  <i v-if="visibilityC == 'password'" @click="showPassword('cpassword')" class="fa fa-eye" aria-hidden="true"></i>
                  <i v-if="visibilityC == 'text'" @click="hidePassword('cpassword')" class="fa fa-eye-slash" aria-hidden="true"></i>
                </span>
            </div>
            <button class="btn btn-primary btn-block login-spacer" v-on:click="signUp()">Signup</button>
            <button class="btn btn-danger btn-block login-spacer" v-on:click="redirect('/login')">Back to Login</button>  
          </div>
        </div>
      </div>
    </div>

  </div>
</template>
<style scoped>


.signup-container, .holder{
  margin-top: 25px;
}

.signup-header{
  height: 100px;
  color: #006600;
  width: 100%;
  float: left;
  text-align: center;
}
.signup-header img{
  height: 100px !important;
  width: auto !important;
}

.signup-header img:hover{
  cursor: pointer;
}

.header-title{
  width: 90%;
  margin:  25px 5% 0 5%;
  font-size: 24px;
  font-weight: 700px;
}

.signup-holder{
  width: 80%;
  margin: 0 10% 0 10%;
  float: left;
}

.input-holder{
  width: 90%;
  margin:  0 5% 0 5%;
}

.form-control{
  height: 45px !important;
}
.btn{
  height: 50px !important;
}
.input-group-addon{
  width: 15% !important;
  text-align: center !important;
  padding: 0px !important;
  display: block !important;
  line-height: 43px !important;
}

.input-group{
  margin-top: 5px;
  margin-bottom: 5px;
}
.site-title{
  margin-top: 25px;
  width: 100%;
  float: left;
}
.site-title img{
  width: 50px;
  width: 50px;
  float: left;
  margin-right: 10px;
}
.site-title .app-name{
  float: left;
}

.account-type{
  width: 120px !important;
}
/*-------------- Extra Small Screen for Mobile Phones --------------*/
@media (max-width: 991px){
  .custom-holder{
    box-shadow: 0 0 0 0 #fff !important;
    margin-top: 50px !important;
  }
}
</style>
<script>
import ROUTER from 'src/router'
import AUTH from 'src/services/auth'
import CONFIG from 'src/config.js'
import COMMON from 'src/common.js'
export default {
  mounted(){
    // this.getSchools()
  },
  data(){
    return {
      username: '',
      email: '',
      password: '',
      cpassword: '',
      type: 'PARTNER',
      errorMessage: null,
      errorMessage2: null,
      errorMessage3: null,
      errorMessage4: null,
      errorMessage5: null,
      errorMessage6: null,
      errorMessage7: null,
      successMessage: null,
      user: AUTH.user,
      tokenData: AUTH.tokenData,
      flag: false,
      schools: null,
      schoolIndex: null,
      common: COMMON,
      visibility: 'password',
      visibilityC: 'password'
    }
  },
  methods: {
    strong(){
      this.successMessage = 'Strong password.'
    },
    showPassword(pass) {
      if(pass === 'password'){
        this.visibility = 'text'
      } else {
        this.visibilityC = 'text'
      }
    },
    hidePassword(pass) {
      if(pass === 'cpassword'){
        this.visibilityC = 'password'
      } else {
        this.visibility = 'password'
      }
    },
    signUp(){
      this.validate()
      let parameter = {
        username: this.username,
        email: this.email,
        password: this.password,
        config: CONFIG,
        account_type: this.type,
        referral_code: null,
        status: 'ADMIN'
      }
      if(this.errorMessage === null && this.errorMessage2 === null && this.errorMessage3 === null && this.errorMessage4 === null && this.errorMessage5 === null && this.errorMessage6 === null && this.errorMessage7 === null){
        $('#loading').css({'display': 'block'})
        this.APIRequest('accounts/create', parameter).then(response => {
          $('#loading').css({'display': 'none'})
          if(response.error !== null){
            if(response.error.status === 100){
              let message = response.error.message
              if(typeof message.username !== undefined && typeof message.username !== 'undefined'){
                this.errorMessage = message.username[0]
              }else if(typeof message.email !== undefined && typeof message.email !== 'undefined'){
                this.errorMessage = message.email[0]
              }
            }else if(response.data !== null){
              if(response.data > 0){
                this.login()
              }
            }
          }
        })
      }
    },
    redirect(parameter){
      ROUTER.push(parameter)
    },
    validate(input){
      this.successMessage = null
      let reqWhiteSpace = /\s/
      if(input === 'username') {
        this.errorMessage = null
        if(reqWhiteSpace.test(this.username)){
          this.errorMessage = 'Username should not contain a space.'
        } else if(this.username.length < 6){
          this.errorMessage2 = 'Username must be atleast 6 characters.'
        } else {
          this.errorMessage = null
          this.errorMessage2 = null
        }
      } else if(input === 'email') {
        this.errorMessage3 = null
        if(AUTH.validateEmail(this.email) === false){
          this.errorMessage3 = 'You have entered an invalid email address.'
        } else {
          this.errorMessage3 = null
        }
      } else if(input === 'password') {
        this.errorMessage4 = null
        if(this.password.length < COMMON.passwordLimit){
          this.errorMessage4 = 'Password must be atleast ' + COMMON.passwordLimit + ' characters.'
        }else if(/^.*(?=.{8,})((?=.*[!@#$%^&*()\-_=+{};:,<.>]){1})(?=.*\d)((?=.*[a-z]){1})((?=.*[A-Z]){1}).*$/.test(this.password)){
          this.strong()
          this.errorMessage4 = null
          this.errorMessage5 = null
        } else {
          this.errorMessage5 = 'Password must be alphanumeric characters. It should contain 1 number, 1 special character and 1 capital letter.'
        }
      } else if(input === 'cpassword') {
        this.errorMessage6 = null
        this.successMessage = null
        if(this.password.localeCompare(this.cpassword) !== 0){
          this.errorMessage6 = 'Password did not match.'
        } else {
          this.errorMessage6 = null
        }
      } else if(this.username.length >= 6 && this.email !== null && this.password !== null && this.password.length >= 6 && this.password.localeCompare(this.cpassword) === 0 && this.type !== null && AUTH.validateEmail(this.email) === true){
        this.errorMessage = null
      }else{
        this.errorMessage7 = 'Please fill in all required fields.'
        this.errorMessage7 = null
      }
    },
    login(){
      AUTH.authenticate(this.username, this.password, (response) => {
        ROUTER.push('dashboard')
      }, (response, status) => {
        this.errorMessage = (status === 401) ? 'Your username and password did not match.' : 'Cannot log in? Contact us through email: support@idfactories.com'
      })
    }
  }
}
</script>
