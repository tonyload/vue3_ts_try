<template>
    <h1>{{result}}</h1>
</template>
<script lang="ts">
import {defineComponent} from 'vue'
export default defineComponent({
    setup(){
        return new Promise((resolve,rejuect)=>{
            setTimeout(() => {
                return resolve({result:'JSpang'})
            }, 1000);

        })
    }
})
</script>