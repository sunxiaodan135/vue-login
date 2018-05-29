<template>
    <div class="wrapper">
      <img src="../assets/logo.png">
      <h1>
        西北干旱安全技术保障监测系统
      </h1>
      <div class="login" v-show="showLogin">
        <Form ref="formInline" label-position="left" :model="formInline" :label-width="100":rules="ruleInline">
          <Form-item prop="user" label="用户名：">
            <Input v-model="formInline.user"></Input>
          </Form-item>
          <Form-item prop="password"  label="密  码：">

            <Input v-model="formInline.password" type="password"></Input>
          </Form-item>
          <Form-item>

            <i-button  size="large"type="success" @click.native="handleSubmit()" long>登录</i-button>
            <span v-on:click="ToRegister">没有账号？马上注册</span>
          </Form-item>

        </Form>
      </div>

      <div class="Register" v-show="showRegister">
        <Form ref="formInline" label-position="left" :model="formInline" :label-width="100":rules="ruleInline">
          <Form-item prop="user" label="用户名：">
            <Input v-model="formInline.user"></Input>
          </Form-item>
          <Form-item prop="password"  label="密  码：">

            <Input v-model="formInline.password" type="password"></Input>
          </Form-item>
          <Form-item prop="password"  label="重复密码：">

            <Input v-model="formInline.repassword" type="password"></Input>
          </Form-item>

          <Form-item>
            <i-button size="large" type="success"  @click.native="handleRegister()" long>注册</i-button>
            <span v-on:click="ToLogin">已有账号？马上登录</span>
          </Form-item>
        </Form>
      </div>
    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      formInline: {
        user: '',
        password: '',
        repassword:''
      },
      showLogin: true,
      showRegister: false,
      ruleInline: {
        user: [{
          required: true,
          message: '请填写用户名',
          trigger: 'blur'
        }],
        password: [{
      required: true,
      message: '请填写密码',
      trigger: 'blur'
    }],
        repassword: [{
      required: true,
      message: '请重复密码',
      trigger: 'blur'
    },
          {
          type: 'string',
          min: 6,
          message: '密码长度不能小于6位',
          trigger: 'blur'
        }]
      }
    }

  },
  methods: {
    handleSubmit() {
        if (this.formInline.user == '123456' && this.formInline.password == '1234567') {
          this.$Message.success('提交成功!');
          this.$router.push('/home');
        } else {
          this.$Message.error('请输入用户名密码!');
        }
      },
      handleReset(val) {
      console.log(val)
    },
    handleRegister(){

      if (this.formInline.user == '123456' && this.formInline.password == '1234567'&&this.formInline.repassword==this.formInline.password ) {
        this.$Message.success('提交成功!');
        this.ToLogin();
      } else if(this.formInline.user == '123456' && this.formInline.password !=this.formInline.repassword){
        this.$Message.error('请再次确认密码一致!');
      }else{
        this.$Message.error('请输入用户名或密码!');
      }
    },
    ToRegister(){
      this.showRegister = true
      this.showLogin = false
    },
    ToLogin(){
      this.showRegister = false
      this.showLogin = true
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .wrapper {
    margin: 0 auto;
    width: 400px;
    height: 520px;
    padding-top: 10px;
    padding-bottom: 10px;
    box-shadow: 5px 5px 10px 10px #888888;
    /*background: -webkit-gradient(linear, 0 0, 0 bottom, from(#ff0000), to(rgba(0, 0, 255, 0.5)));*/
    /*background: #fff;*/
    /*url(http://78rbeb.com1.z0.glb.clouddn.com/wp-content/uploads/2014/03/free-blurred-web-backgrounds-04.jpg);*/
  }
  .wrapper > h1{
    text-align: center;
    vertical-align: middle;
    margin-bottom: 20px;
    color: #000;
  }
  .login {
    margin: 0 auto;
    padding: 200px auto;
    width: 70%;
    height: 100%;
  }
  .Register {
    margin: 0 auto;
    padding: 200px auto;
    width: 70%;
    height: 100%;
  }
  span{cursor:pointer;}
</style>
