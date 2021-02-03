<template>
  <div class="header">
    <div class="header-wrap">
      <div class="gnav-holder">
        <button class="btn gnav">
          <span class="ham ham-top"></span>
          <span class="ham ham-middle"></span>
          <span class="ham ham-bottom"></span>
        </button>
      </div>
      <div class="logo-holder">
        <a class="btn" href="#TOP">
          <span class="img-holder">
            <img src="~/assets/img/logo.svg" alt="ロゴ">
          </span>
        </a>
      </div>
      <div class="icons-holder">
        <span class="icon icon-cart btn">
          <font-awesome-icon icon="shopping-cart"/>
        </span>
        <span class="icon icon-cart btn">
          <font-awesome-icon icon="shopping-cart"/>
        </span>
        <span class="icon icon-cart btn">
          <font-awesome-icon icon="shopping-cart"/>
        </span>
        <span class="icon icon-cart btn">
          <font-awesome-icon icon="shopping-cart"/>
        </span>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .header {
    width: 100%;
    height: 54px;
    position: fixed;
    top: 0;
    left: 0;
    background: #fff;
    border-bottom: 1px solid #e0e0e0;
    z-index: 2;
    background-color: rgb(250, 250, 250);
  }
  .header-wrap {
    width: 90%;
    margin: 0 auto;
    display: flex;
    align-items: center;
  }
  .gnav-holder {
    width: 33%;
    display: flex;
    flex-direction: column;
    .gnav {
      position: relative;
      background-color: #fff;
      border: 1px solid #e0e0e0;
      width: 45px;
      height: 45px;
      .ham {
        width: 20px;
        height: 2px;
        background-color: #666;
        display: block;
        margin: 0 auto;
        &.ham-top {
          position: absolute;
          top: 15px;
          left: 12px;
        }
        &.ham-middle {
          position: absolute;
          top: 20px;
          left: 12px;
        }
        &.ham-bottom {
          position: absolute;
          top: 25px;
          left: 12px;
        }
      }
    }
  }
  .logo-holder {
    width: 33%;
    display: flex;
    flex-direction: column;
    align-items: center;
    .img-holder {
      display: block;
      width: 42px;
    }
  }
  .icons-holder {
    width: 33%;
    display: flex;
    justify-content: flex-end;
    .icon {
      width: 52px;
      padding: 10px 15px;
      color: #666;
    }
  }
</style>
