<template>
  <div class="register-container">
    <input v-model="name" placeholder="username" class="input-username">
    <input v-model="password" type="password" placeholder="password" class="input-password">
    <div @click="submit" class="button-submit">登录</div>
  </div>
</template>

<script>
  import md5 from 'md5.js'
  import axios from 'axios'

  export default {
    name: "Register",
    data(){
      return{
        name: '',
        password: ''
      }
    },
    methods: {
      submit(){
        axios({
          method: 'post',
          url: '/api/auth/login',
          data: {
            name: this.name,
            password: new md5().update(this.password).digest('hex')
          }
        }).then((data)=>{
          if (data.data.data){
            alert('login success')
            this.$router.push({path: '/main'})
          }else{
            alert(data.data.message)
          }
        }).catch(error=>{
          alert(error)
        })
      }
    }
  }
</script>

<style scoped>
  .register-container{
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    margin: auto;
    height: 10rem;
    width: 80%;
  }
  .input-username{
    display: flex;
    width: 95%;
    height: 2rem;
    border-radius: 5px;
  }
  .input-password{
    display: flex;
    width: 95%;
    height: 2rem;
    border-radius: 5px;
  }
  .button-submit{
    display: flex;
    justify-content: center;
    align-items: center;
    color: #222222;
    width: 95%;
    background-color: #4effbe;
    height: 2rem;
    border-radius: 5px;
  }
</style>
