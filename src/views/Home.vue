<template>
  <div class="home" id="home">
    <HeadComponent />
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->

    <!-- <HelloWorld :msg = msg /> -->
    
    <!-- container S -->
    <div class="page_container">

    </div>
    <!-- container E -->

    <!-- footer组件 S -->
    <FooterComponent ref="footer" :obj = selectPage />
    <!-- footer组件 E -->

    
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import FooterComponent from '@/components/Footer-component.vue'
import HeadComponent from '@/components/Head-component.vue'
import store from '@/store.js'

import {getCaeList} from '../service/api'

export default {
  name: 'home',
  components: {
    HelloWorld,
    FooterComponent,
    HeadComponent
  },
  data(){
    return {
        userInfo:store.state.userInfo,
        selectPage:'one'
    }
  },
  mounted(){
    document.getElementById('home').style.minHeight = window.innerHeight + 'px';
    this.$refs.footer.footerItem[0].isActive = true;
    
    this.init();
    

  },
  methods:{
    //获取占卜列表
    init(){
        let params = { hasHot:true }
        let userInfo = {
          name:'xiaocai',
          age:18
        }
      
        getCaeList(params).then(res => {
          console.log(res)
        });

         //提交用户信息动作
        store.dispatch('commitUserInfo',userInfo)

        //清除store中的信息
        // store.dispatch('commitClearInfo',null)
        // console.log(store)
      }
  }
}
</script>



<style lang="less" scoped>
.home {
  width: 100%;
  background: #f9f3ed !important;
  overflow: hidden;
  .page_container {
    width: 7rem;
    height: 7.4rem;
    margin: 0.68rem auto 0;
  }
}
</style>

