<template>
  <div id="user-info">
    <!-- <a href="#" class="clear-fix">
      <slot name="user-icon">
        <svg class="privateImage-svg left">
          <use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#avatar-default"></use>
        </svg>
        <img src="" alt="" class="icon-img">
      </slot>
      <div class="login-info left">
        <slot name="user-nickname">
          <div>登录/注册</div>
        </slot>
        <div class="phone">
          <span>
            <svg data-v-735ff1be="" fill="#fff" class="icon-mobile"><use data-v-735ff1be="" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#mobile"></use></svg>
          </span>
          <slot name="user-phone">手机号：17772922979</slot>
        </div>
      </div>
      <svg data-v-735ff1be="" fill="#fff" class="arrow-svg right"><use data-v-735ff1be="" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#arrow-right"></use></svg>
    </a> -->
   <div>
     <img src="../../../assets/img/tabbar/user.jpg" alt="">
     <a href="">昵称: coderzzw</a>
     <p>账号：17772922979</p>
     <p>登录/退出</p>
   </div>
   
  </div>
</template>

<script>
	export default {
		name: "UserInfo"
	}
</script>

<style scoped>
  img {
    margin-top: 15px;
    width: 40px;
    height: 40px;
  }
  a {
    margin-left: 20px;
    margin-bottom: 15px
  }
  img, a {
    display: inline-block;
  }
  p {
    margin-top: 10px;
  }
 /*  #user-info {
    background-color: var(--color-tint);
    padding: 15px;
    margin-top: -5px;
  }

  #user-info .privateImage-svg {
    width: 60px;
    height: 60px;
    background-color: #fff;
    border-radius: 30px;
  }

  .left {
    float: left;
  }

  #user-info .arrow-svg {
    width: 11px;
    height: 22px;
    margin-top: 18px;
  }

  #user-info .login-info {
    color: #fff;
    margin: 10px 0 0 10px;
  }

  #user-info .login-info .phone {
    position: relative;

    font-size: 13px;
    margin-top: 5px;
    margin-left: 15px;
    font-weight: 300;
  }

  #user-info .login-info .phone .icon-mobile {
    position: absolute;
    width: 12px;
    height: 18px;
    left: -15px;
    top: 0px;
  } */
</style>
