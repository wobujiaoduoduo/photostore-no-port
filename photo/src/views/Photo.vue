<template>
    <div>
         <!-- 展示相关 -->
    <div class="container">
      <div class="photoHeader">
        <div class="imgContainer">
          <img class="photoName" src=""/>
        </div>
        <div class="btnContainer">
          <span class="photoTitle">相册名称</span>
          <button class="mybtn" @click="showView" >上传照片</button>
        </div>
      </div>
S
      <div class="photoContainer">
        <div v-for="item in photos" :key="item.id" >
        <div class="photoItem" >
             <img :src= "item.imgUrl">
          <span>
            {{item.id}}
          </span>
        </div>
            
        </div>
        <!-- <div class="photoItem">
          <img src="img/Home.png" />
          <span>
            home
          </span>
        </div> -->

      </div>
    </div>
    <!-- 上传相关 -->
    <!-- vue3更新了 -->

    <UploadView ref="child" @upload-completed="handleUplaoadCompleted"> </UploadView>


    </div>
</template>

<script>
    import {apiGetPhotos} from "../api";
    import UploadView from "../components/UploadView"

    
    export default {
        methods: {
            handleUplaoadCompleted(){
                //通知后更新
                 apiGetPhotos().then((res) => {
                console.log(res);
                this.photos = res.data.photos
            }).catch((err) => {
                console.log(err)
            })
            },
            //ref
            showView() {
                console.log("我点击了");
                this.$refs.child.childMethod()


            }
        },
        components: {
            UploadView,
        },
        //渲染页面
        data(){
            //
            return{
                //我没有后端接口的图片所以
                photos: [
                    {
                        id:1,
                        imgUrl : "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRN4DT-h0M9bUfwa9aOHXcnPwqHNyMch5q3iw&usqp=CAU"
                    },
                    {
                        id:2,
                        imgUrl: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRN4DT-h0M9bUfwa9aOHXcnPwqHNyMch5q3iw&usqp=CAU"
                    }
                ]
            }
        },
        //连接后端接口
        //**无后端接口， */
        created () {
            apiGetPhotos().then((res) => {
                console.log(res);
                this.photos = res.data.photos
            }).catch((err) => {
                console.log(err)
            })
        },
    }
</script>






















<style scoped>
.container {
  width: 100%;
  background: rgb(224, 240, 244);
  padding: 30px;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.photoHeader {
  width: 100%;
  display: flex;
}

.photoName {
  width: 70px;
  height: 70px;
  margin: 0px;
}

.btnContainer {
  display: flex;
  flex-direction: column;
  margin-left: 10px;
  font-size: 22px;
}

.imgContainer {
  width: 70px;
  height: 70px;
  border: 1px solid #d9d9d9;
  overflow: hidden;
  background-color: #fff;
  padding: 3px;
  top: 0;
  left: 0;
}

.photoTitle {
  margin-bottom: 10px;
}

.mybtn {
  width: 168px;
  height: 35px;
  background: #5ccfe6;
  border: 1px solid #5ccfe6;
  color: white;
  font-size: 16px;
}

.photoContainer {
  margin-top: 50px;
}

.photoItem {
  display: flex;
  flex-direction: column;
  margin-right: 20px;
  float: left;
  margin-bottom: 30px;
}

.photoItem img {
  width: 164px;
  height: 123px;
  opacity: 1;
  background: rgb(222, 222, 222);
}

.photoItem span {
  text-align: center;
  width: 164px;
  height: 32px;
  background: rgb(244, 253, 255);
  line-height: 32px;
  float: left;
}

.mybtn {
  cursor: pointer;
}

.addPhotoContainer {
  position: fixed;
  top: 0px;
  left: 0px;
  background: rgb(0, 0, 0);
  opacity: 0.2;
  width: 100%;
  height: 100vh;
}

.addController {
  width: 80%;
  height: 650px;
  background: white;
  opacity: 1;
  position: absolute;
  left: 10%;
  top: 60px;
  display: flex;
  flex-direction: column;
  border-radius: 5px;
  overflow: hidden;
  box-shadow: 0 0 5px #535658;
}

.addTitle {
  font-size: 12px;
  line-height: 31px;
  margin: 0px;
  background: #f3f3f3;
  border: 1px solid #f3f3f3;
  padding-left: 20px;
  border-bottom: 1px solid #e5e5e5;
}

.close {
  float: right;
  margin-right: 20px;
  font-size: 10px;
  cursor: pointer;
}

.photoTitles {
  width: 100%;
  height: 58px;
  background: #f5f4f5;
  display: flex;
}

.uploadTo {
  font-size: 12px;
  line-height: 40px;
  margin-right: 10px;
  padding-left: 20px;
  margin-top: 8px;
}

.photoSelect {
  width: 210px;
  height: 40px;
  line-height: 40px;
  font-size: 12px;
  /* text-align: center; */
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  background: white;
  margin-top: 8px;
}

.showPhoto {
  width: 40px;
  height: 40px;
  display: block;
  float: left;
  margin-right: 10px;
  margin-left: 5px;
}

.uploadContainer {
  margin-top: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.fileinput-button {
  position: relative;
  display: inline-block;
  overflow: hidden;
  background: #5caae6;
  border-radius: 3px;
  padding: 0 30px;
  color: white;
  width: 210px;
  height: 50px;
  text-align: center;
  line-height: 50px;
  font-size: 18px;
}

.fileinput-button:hover {
  background: #3092f5;
}

.fileinput-button input {
  position: absolute;
  right: 0px;
  top: 0px;
  opacity: 0;
  font-size: 50px;
}

.hint {
  margin-top: 10px;
  color: #999;
  font-size: 14px;
}

.masking {
  display:block;
}

.wantUpload {
  margin-left: 10px;
  margin-top: 10px;
  position: relative;
}

.uploadPhotoItem {
  display: flex;
  flex-direction: column;
  margin-right: 20px;
  float: left;
  margin-bottom: 30px;
  position: relative;
}

.uploadPhotoItem img {
  width: 164px;
  height: 123px;
  opacity: 1;
  background: rgb(222, 222, 222);
}

.pictureName {
  background: white;
  border: 1px solid rgb(225, 225, 225);
  text-align: center;
}

.myProgress {
  top: 50px;
  height: 24px;
  background: rgba(0, 0, 0, 0.5);
  text-align: center;
  position: absolute;
  width: 164px;
  color: white;
}

.plan {
  position: absolute;
  width: 30%;
  left: 0px;
  background: rgba(0, 255, 0, 0.5);
  height: 24px;
}

.bottomStyle {
  height: 64px;
  width: 100%;
  background: #f3f3f3;
  position: absolute;
  bottom: 20px;
  cursor: pointer;
}

.uploadBtn:hover {
  background: #3092f5;
}

.uploadBtn {
  width: 150px;
  height: 40px;
  background: #5caae6;
  border-color: #4798d6;
  display: block;
  border-radius: 2px;
  margin-left: 10px;
  margin-top: 10px;
  text-align: center;
  line-height: 40px;
  color: white;
  font-size: 18px;
}

.loadContainer {
  display: none;
}

.myProgress {
  display: none;
}

.fileinput-add {
  position: relative;
  display: inline-block;
  overflow: hidden;
  background-color: red;
  background-position: 0 0;
  border-radius: 3px;
  padding: 0 30px;
  width: 92px;
  height: 148px;
  line-height: 50px;
  font-size: 18px;
}

.fileinput-add input {
  position: absolute;
  right: 0px;
  top: 0px;
  opacity: 0;
  font-size: 100px;
}

.changeBtn {
  border: 1px solid #dfdfdf;
  width: 150px;
  height: 40px;
  display: block;
  border-radius: 2px;
  margin-left: 10px;
  margin-top: 10px;
  text-align: center;
  line-height: 40px;
  font-size: 18px;
}


</style>
