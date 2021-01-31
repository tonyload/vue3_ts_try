<template>
<!-- teleport 挂在到指定ID下的dom下 -->
    <teleport to="#modal"> 
        <div id="center">
            <h2>jspang.com</h2>
        </div>
    </teleport>    
</template>

<script lang="ts">
export default {

}
</script>
<style  >
#center{
    width:200px;
    height:200px;
    border:1px solid #000000;
    background:#ffffff;
    position: fixed;
    left:50%;
    top:50%;
    margin-left:-100px;
    margin-top:-100px;
}
</style>