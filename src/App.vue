<template>
  <div id="app">
    <el-alert id='tip' :title="tip_msg" type="error" show-icon v-if="isTip"></el-alert>
    <div class="login_logo">

    </div>
    <div class="login">
        <div class="box1">
        		<div class = "login-massage">
        			乐活&nbsp;·&nbsp;乐智能&nbsp;·&nbsp;乐健康
        		</div>
    	    <div class="form_box">
    	        <div class="login_form">
    	        		<p > 欢迎登陆Santa Fe平台</p>
    	        		<form autocomplete="off" >
    	            <div class="input_fill user_input">
    	                <!--<label>用户名</label><br />-->
    	                <input type="text" placeholder="请输入用户名" name="text" autocomplete="off" v-on:focus="nameFoucs" v-on:blur="nameBlur" v-bind:class="{'active':namefoucs}" v-model="content_name">
    	                <span class="user_icon" v-bind:class="{'active':namefoucs}"></span>
    	            </div>
    	            <div class="input_fill password_input">
    	                <!--<label>密码</label><br />-->
    	                <input type="password" placeholder="请输入密码" name="password" autocomplete="off"  v-on:focus="passwordFoucs" v-on:blur="passwordBlur" v-bind:class="{'active':passwordfoucs}" v-model="content_pwd"/>
    	                <span class="password_icon" v-bind:class="{'active':passwordfoucs}"></span>
    	            </div>
    	            </form>
    	            <div>
    	                <input type="button" v-on:mousedown='loginBtnDidClicked' v-on:mouseup='loginBtnDidMouseup' :class="didClicked ? 'sign_up_clicked' : 'sign_up'" value="登录" />
    	            </div>
    	        </div>
    	        <div class="login_mask"></div>
    	    </div>
    	    <div class="QR_code">
    	    		<img src="./../static/img/QR_code.png"/>
    	    		<p> 扫描添加</p>
    	    		<p>意见反馈界面</p>
    	    </div>
        </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Santa Fe个人健康信息及护理决策AI系统',
      didClicked:false,
      namefoucs:false,
      passwordfoucs:false,
      content_name:"",
      content_pwd:"",
      isTip:false,
      tip_msg:""
    }
  },
  props: {

  },
  methods: {
    loginBtnDidClicked:function() {
      console.log('name:'+this.content_name+'\n'+'password:'+this.content_pwd);
      this.didClicked = true
    },
    loginBtnDidMouseup:function() {
      console.log('mouseup');
      this.didClicked = false
    },
    //获得焦点
    nameFoucs:function() {
      console.log('foucs');
      this.namefoucs = true;
    },
    //失去焦点
    nameBlur:function() {
      this.namefoucs = false;
      if (!this.checkPhone(this.content_name)) {
        this.isTip = true;
        this.tip_msg = '手机号码有误，请重新填写';
      }
      else {
        this.isTip = false;
      }
    },
    passwordFoucs:function() {
      this.passwordfoucs = true;
    },
    passwordBlur:function() {
      this.passwordfoucs = false;
    },
    checkPhone:function(content){
      // var phone = document.getElementById('phone').value;
      if(!(/^1[34578]\d{9}$/.test(content))) {
        return false;
      }
      else {
        return true;
      }
}
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #fff;
  margin:0 auto;


}
h1, h2 {
  font-weight: normal;
}

.sign_up {
  width:100%;
  height:40px;
  background:#0082dd;
  color:#fff;
  font-size:16px;
  border-radius:4px;
  cursor: pointer;
}

.sign_up_clicked {
  width:100%;
  height:40px;
  color:#fff;
  font-size:16px;
  border-radius:4px;
  cursor: pointer;
  background: gray;
}

.login .form_box .name {
  width:250px;height:38px;border:1px solid #ddd;background: #fff;border-radius:4px;padding-left:50px;line-height:38px;
  border-color: #0082dd;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

#tip {
  text-align: center;
}

</style>
