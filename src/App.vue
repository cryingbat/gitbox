<template>
  <div>
    <div>
      <v-header :seller='seller'></v-header>
    </div>
    <div class="tab">
      <div class="tab-item">
        <router-link to='/goods'>商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to='/ratings'>评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to='/seller'>商家</router-link>
      </div>
    </div>
    <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
</template>

<script>
import header from './components/header/header'
import {urlParse} from "@/common/js/urlParse"
const ERR_OK = 0;
export default {
  data() {
    return {
      seller: {
        id:(() => {
          let queryParm = urlParse();
          console.log(queryParm)
          // return queryParm.id;
        })()
      }
    }
  },
  created() {
    this.$http.get('/api/seller').then(response => {
      if(response.body.errno == ERR_OK){
        this.seller = response.body.data;
        // this.seller = Object.asign({},this.seller,)
      }
    });
  },
  components: {
    'v-header' : header
  }
}
</script>

<style>
@import "./common/css/style.css"
body,html{line-height: 1;font-weight: 200;font-family: 'PingFang SC','STHeitiSC-Light','Helvetical-Light',arial,sans-serif}
  .tab{display: flex;width: 100;height: 40px;}
  .tab-item{flex: 1;text-align: center;line-height: 40px}
  .router-link-active{color: red}
</style>