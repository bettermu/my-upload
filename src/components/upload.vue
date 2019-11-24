<template>
<div class="uplaod-wrap">
    <div class="select-wrap">
        <input @change="fileChange($event)" :multiple="multiple" id="upload" type="file" hidden />
        <label for="upload"></label>
    </div>
    <div class="file-list-wrap">
        <span v-show="!files.length">尚未选择任何文件哦</span>
        <div class="list-item" v-for="(item,index) in files" :key="index">
            <div class="delete-mask" @click="deleteFile(item)"></div>
            <img :src="item.url" alt />
            <div class="item-name">{{item.file.name.split('.')[0]}}</div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    props: {
        multiple: {
            default: false
        },
        limit:{
            default:5
        }
    },

    data() {
        return {
            uid: 0, //file uid
            files: [], //文件数组
            imgSuffixArr: ["jpg", "jpeg", "png", "gif"],
            suffixObj: {
                xlsx: require("../assets/img/excel.png"),
                pdf: require("../assets/img/pdf.png"),
                doc: require("../assets/img/word.png")
            }
        };
    },

    methods: {
        //文件选择触发事件
        fileChange(e) {
            if(this.files.length >= this.limit){
                return
            }
            let that = this;
            //e.target.files[0]为选择的文件对象

            //类数组转换成数组
            let files = Array.prototype.slice.call(e.target.files)

            //上传数量限制
            files = files.length > this.limit ? files.slice(0,this.limit) : files ;

            for (let i = 0; i < files.length; i++) {
                let file = files[i];
                //new 一个 FileReader对象
                let reader = new FileReader();

                reader.readAsDataURL(file);
                reader.onload = function (result) {
                    that.files.push({
                        uid: ++that.uid,
                        file: file,
                        url: that.imgUrlByFileType(file, result) //require('../assets/img/pdf.png') //////
                    });
                };
            }
        },

        //删除文件触发事件
        deleteFile(item) {
            let index = this.findFileById(item.uid);
            this.files.splice(index, 1);
        },

        //找出对应uid的文件
        findFileById(id) {
            for (let i = 0; i < this.files.length; i++) {
                if (this.files[i].uid === id) {
                    return i;
                }
            }
        },

        //判断文件类型,返回对应缩略图
        imgUrlByFileType(file, result) {
            let suffix = file.name.split(".")[1];

            return this.imgSuffixArr.includes(suffix) ?
                result.target.result :
                this.suffixObj[suffix];
        }
    }
};
</script>

<style lang="less" scoped>
.select-wrap {
    label {
        display: block;
        height: 100px;
        width: 100px;
        background: url("../assets/img/add-file-default-icon.png") center no-repeat;
        cursor: pointer;

        &:hover {
            background: url("../assets/img/add-file-hover-icon.png") center no-repeat;
        }
    }
}

.file-list-wrap {
    .list-item {
        float: left;
        position: relative;
        margin-right: 10px;

        &:hover {
            .delete-mask {
                opacity: 1;
            }
        }

        .delete-mask {
            cursor: pointer;
            opacity: 0;
            position: absolute;
            top: 0;
            right: 0;
            height: 30px;
            width: 30px;
            background: url("../assets/img/delete.png") center rgba(0, 0, 0, 0.6) no-repeat;
            background-size: 16px 16px;
            transition: all 0.3s;
        }

        .item-name {
            max-width: 100px;
            text-align: center;
        }

        img {
            height: 80px;
        }
    }
}
</style>
