<template>
  <div class="about">
    <h1>{{nowTime}}</h1>
    <button @click="getNowTime">start</button>
    <h1>Red Romance wash house</h1>
    <p>请选择一位美女为您服务</p>

    <modal></modal>
    <div v-if="loading">loading... </div>
    <img v-if="loaded" :src="result.imgUrl" />


    <div>---------Suspense--------------</div>
    <Suspense>
      <template #fallback>
          loading
      </template>
      <template #default>
          <AsyncShow/>
      </template>
    </Suspense>

 <div>---------Suspense real--------------</div>
 <Suspense>
      <template #fallback>
          loading
      </template>
      <template #default>
          <GirlShow/>
      </template>
    </Suspense>
  </div>
</template>
<script>
import { ref,onErrorCaptured} from 'vue';
import {nowTime,getNowTime} from "../hooks/useNowTime"
import useUrlAxios from '../hooks/userUrlAxios'
import modal  from '../components/Modal'
import AsyncShow from '../components/AsycShow'
import GirlShow from '../components/GirlShow'
export default {
  components:{modal,AsyncShow,GirlShow},
  setup(){
      const url ="https://apiblog.jspang.com/default/getGirl"
      const {result,loading,loaded,error} = useUrlAxios(url)



      //异步函数捕获异常
      onErrorCaptured((error)=>{
        console.log("error====>",error)
        return true
      })


    return{
      nowTime,
      getNowTime,
      result,
      loading,
      loaded
    }
  }
  
}
</script>