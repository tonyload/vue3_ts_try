<template>
    <img :src="result && result.imgUrl" />
</template>
<script>
import axios from "axios"
import {defineComponent} from "vue"
export default  defineComponent({
    async setup() {
        const rawData  = await axios.get("https://apiblog.jspang.com/default/getGirl")
        return {
            result:rawData.data
        }
    }
})
</script>