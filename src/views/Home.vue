<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>Red Romance wash house</h1>
    <p>请选择一位美女为您服务</p>
    <div>

      <button v-for="(item,index) in girls" v-bind:key="index"
        @click="selectGirlFun(index)"
      > 
         {{index}}: {{item}}
      </button>
      <p>你选择了哪个美女为你服务：{{selectGirl}}</p>

      <button @click="overAction">点餐完毕</button>
      <p>{{overText}}</p>
    </div>
  
  </div>
</template>

<script lang="ts">

/**
 * ref() --将数据变成模板中可以使用的数据
 * reactive--将数据变成模板中可以使用的数据，可以让程序看起来更规范 
 * 
 */


/**
 * 生命周期
 * 钩子函数-伴随生命周期
 * setup()--组件创建之前，在v2中代替beforeCreated和created
 * 尽量使用setUp中的生命周期钩子函数
 * onActivated()   被包含在<keep-alive></keep-alive>中的组件，会多出两个生命周期函数，被激活时候执行
 * onDeactived() 比如 a组件切换到 B组件，a组件消失时候执行
 * onErrorCapture() --当捕获一个来自子组件的异常时候激活的钩子函数
 * 
 * 
 */


 /**
  * onRenderTracked onRenderTrigger --特有生命周期钩子函数，状态跟踪
  * onRenderTracked--跟踪虽有数据信息变化后的
  */
import { defineComponent ,ref,reactive, toRefs,onBeforeMount, onBeforeUnmount, onMounted, onBeforeUpdate, onUpdated, onUnmounted,onRenderTracked,onRenderTriggered, watch} from 'vue';
interface DataProp{
  girls:string[],
  selectGirl:string,
  selectGirlFun:(index:number)=>void
  // overText:string
  // overAction:()=>void
}
export default({
  name: 'Home',
  setup(){
    console.log("1setup function did------------开始创建组件就会执行setup")
    const data:DataProp =reactive({
      girls:['大脚',"刘莹",'小红'],
      selectGirl:"",
      selectGirlFun:(index:number)=>{
        data.selectGirl =data.girls[index]
      },
      // overAction(){
      //     data.overText = data.selectGirl + "|点餐完毕"
      // },
      // overText:""
    })
    const refData = toRefs(data)

    const overText = ref("红浪漫")
    const overAction = ()=>{
      overText.value = "点餐完成|"+overText.value
    }
    //监听函数的使用
    watch([overText,()=>data.selectGirl],(newV,oldV)=>{
      console.log( typeof newV[0])
      document.title = newV[0].toString()
    })


    // const girls =  ref(['大脚',"刘莹",'小红'])
    // const selectGirl = ref("")
    // const selectGirlFun = (index:number)=>{
    //   selectGirl.value =girls.value[index]
    // }



    // onBeforeMount(()=>{
    //   console.log("2组件挂载到页面执行之前---------------onBeforeMount")
    // })
    // onMounted(()=>{
    //    console.log("3组件挂载到页面执行之后---------------onMounted")
    // })
    // onBeforeUpdate(()=>{
    //    console.log("4组件更新的时候执行之前---------------onBeforeUpdate")
    // })
    // onUpdated(()=>{
    //    console.log("5组件更新的时候执行之后---------------onUpdated")
    // })
    // onBeforeUnmount(()=>{
    //   console.log("在组件卸载之前执行-----------------onBeforeUnmount")
    // })
    // onUnmounted(()=>{
    //    console.log("在组件卸载之后执行-----------------onMounted")
    // })
    // onRenderTracked((event)=>{//跟踪所有data
    //   // console.log("onRenderTracked",event)
    // })
    // onRenderTriggered((event)=>{//跟踪变化的data
    //   console.log("onRenderTriggered",event)
    // })







    return{
      ...refData,
      overText,
      overAction
    }
  },
  // beforeCreated(){
  //   console.log("1.1组件挂载到页面之前**************beforeCreated")
  // },
  // beforeMount(){
  //    console.log("2.1组件挂载到页面之前**************beforeMount")
  // },
  // mounted(){
  //   console.log("3.1组件挂载到页面之前**************mounted")
  // },
  // beforeUpate(){
  //    console.log("4.1组件更新之前**************beforeUpate")
  // },
  // updated(){
  //     console.log("5.1组件更新之后**************updated")
  // }


});
</script>


