<template>
    <d2-container type="card">
        <template slot="header">
            <el-tag>基本信息</el-tag>
        </template>
        <div class="user-profile">
            <div class="user-profile-left">
                <el-form ref="form" :model="userForm" :rules="rules" label-position="right" label-width="100px"
                         size="medium">

                    <el-form-item label="昵称" prop="username" style="width:200px">
                        <el-input v-model="userForm.username"></el-input>
                    </el-form-item>
                    <el-form-item label="性别" prop="gender">
                        <el-radio-group v-model="userForm.resource">
                            <el-radio label="男"></el-radio>
                            <el-radio label="女"></el-radio>
                        </el-radio-group>
                    </el-form-item>
                    <el-form-item label="出生日期" prop="birthday" style="width:500px">
                        <el-col :span="11">
                            <el-form-item prop="date1">
                                <el-date-picker
                                        v-model="userForm.birthDate"
                                        type="date"
                                        placeholder="选择日期"
                                        style="width: 100%;"/>
                            </el-form-item>
                        </el-col>
                    </el-form-item>
                    <el-form-item label="常用邮箱" prop="email" style="width:300px">
                        <el-input v-model="userForm.email" placeholder="name@example.com"></el-input>
                    </el-form-item>
                    <el-form-item label="联系电话" prop="phone" style="width:300px">
                        <el-input v-model="userForm.phone"></el-input>
                    </el-form-item>
                    <el-form-item label="住址">
                        <area-cascader type='all' placeholder="请选择" :level="1" :data="pcaa"
                                       v-model="selected"></area-cascader>
                    </el-form-item>
                    <el-form-item prop="address">
                        <el-input placeholder="具体地址" v-model="userForm.address" style="width:500px"></el-input>
                    </el-form-item>
                </el-form>
                <el-button type="primary" @click="updateProfile">修改信息</el-button>
            </div>
            <div class="user-profile-right">
                <el-upload
                        class="avatar-uploader"
                        action="123"
                        :show-file-list="false"
                        :on-success="handleAvatarSuccess"
                        :before-upload = "beforeAvatarUpload" >
                <img v-if="imageUrl" :src="imageUrl" class="avatar">
                <i v-else class="el-icon-plus avatar-uploader-icon"></i>
                </el-upload>


            </div>
        </div>
        <template slot="footer">footer</template>
    </d2-container>
</template>

<script>
    import {AreaSelect} from "vue-area-linkage";
    import AreaData from "area-data";
    import {pca, pcaa} from "area-data";
    import {mapGetters} from 'vuex'

    export default {
        name: 'profile',
        component: {
            AreaSelect: AreaSelect
        },
        data() {
            return {
                userForm: {
                    username: 'xiaying',
                    gender:null,
                    email: "xiaying@xy.com",
                    phone: 123456789,
                    address: null,
                    birthDate:'',
                },
                pca: pca,
                pcaa: pcaa,
                // placeholder: [" ", " ", " "],
                selected: ['广东省', '深圳市', '南山区'],

                rules: {},

                imageUrl: ''
            }
        },
        methods: {
            ...mapGetters('d2admin/user', [
                'getUserInfo'
            ]),
          handleAvatarSuccess(res, file) {
            this.imageUrl = URL.createObjectURL(file.raw);
          },
          beforeAvatarUpload(file) {
            const isJPG = file.type === 'image/jpeg';
            const isLt2M = file.size / 1024 / 1024 < 2;

            if (!isJPG) {
              this.$message.error('上传头像图片只能是 JPG 格式!');
            }
            if (!isLt2M) {
              this.$message.error('上传头像图片大小不能超过 2MB!');
            }
            return isJPG && isLt2M;
          },
            //当上传图片后，调用onchange方法，获取图片本地路径
          // onchange(file, fileList){
          //   var _this = this;
          //   var event = event || window.event;
          //   var file = event.target.files[0];
          //   var reader = new FileReader()
          //   //转base64
          //   reader.onload = function(e){
          //     _this.imageUrl = e.target.result // 将图片路径赋值给src
          //   }
          //   reader.readAsDataURL(file);
          // },
          updateProfile(){
              const
          }
        },
        created: function () {
            this.userForm.username = this.getUserInfo().name
            this.userForm.phone = this.getUserInfo().other.phone
            this.userForm.email = this.getUserInfo().other.email
        }
    }
</script>
<style lang="scss" scope>
    .user-profile {
        width: 100%;
        height:370px;
        margin-left: 10px;
        background: white;


    .user-profile-left {
        width: 50%;
        float: left;
        margin-right: 20px;
    }

    .user-profile-right {
        width: 40%;
        float: right;
        height: 100px;
    .avatar-uploader .el-upload {
        border: 1px dashed #d9d9d9;
        border-radius: 6px;
        cursor: pointer;
        position: relative;
        overflow: hidden;
    }

    .avatar-uploader .el-upload:hover {
        border-color: #409EFF;
    }

    .avatar-uploader-icon {
        font-size: 28px;
        color: #8c939d;
        width: 178px;
        height: 178px;
        line-height: 178px;
        text-align: center;
    }

    .avatar {
        width: 178px;
        height: 178px;
        display: block;
    }



    }

    }

    /*.avatar-uploader .el-upload {*/
        /*border: 1px dashed #d9d9d9;*/
        /*border-radius: 6px;*/
        /*cursor: pointer;*/
        /*position: relative;*/
        /*overflow: hidden;*/
    /*}*/

    /*.avatar-uploader .el-upload:hover {*/
        /*border-color: #409EFF;*/
    /*}*/

    /*.avatar-uploader-icon {*/
        /*font-size: 28px;*/
        /*color: #8c939d;*/
        /*width: 178px;*/
        /*height: 178px;*/
        /*line-height: 178px;*/
        /*text-align: center;*/
    /*}*/

    /*.avatar {*/
        /*width: 178px;*/
        /*height: 178px;*/
        /*display: block;*/
    /*}*/





</style>
