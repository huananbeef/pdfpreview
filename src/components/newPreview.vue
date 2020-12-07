<template>
    <div>
        预览的PDF内容丫
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped>
    .contract-modal {
        position: absolute;
        right: 15%;
        width: 1000px;
        height: 500px;
        overflow: scroll;
        background: rgba(139, 148, 171, 0.7);
        padding: 20px 0 0;
        z-index: 900;
    }
    .contract-modal .contract-detail {
        margin: 0 auto;
        max-width: 96%;
        height: auto;
    }
    .contract-btns{
        height: 50px;
        background-color:  #fff;
        text-align: center;
        padding-bottom:44px;
        padding-top:10px;
    }
    #mycanvas {
        min-height: 50vh;
        background: #fff;
    }
    canvas{
        margin: 0 auto;
        display: block;
        border-bottom:2px solid #aaa;
    }
    .close-btn{
        position: absolute;
        right: 15%;
        width: 26px;
        height: 26px;
        z-index: 999;
        background-color: #666;
        border-radius: 50%;
        cursor: pointer;
    }
</style>
