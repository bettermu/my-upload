<template>
    <div class="uplaod-wrap">
        <div class="select-wrap">
            <input id="upload" type="file" hidden>
            <label for="upload"></label>
        </div>
        <div class="file-list-wrap">
            这里是文件上传列表
        </div>
        
    </div>
</template>

<script>
export default {
    
}
</script>

<style lang="less" scoped>

.select-wrap {
    label {
        display:block;
        height:100px;
        width:100px;
        background:url('../assets/img/add-file-default-icon.png') center no-repeat;
        &:hover {
            background:url('../assets/img/add-file-hover-icon.png') center no-repeat;
        }
    }
}
    
</style>