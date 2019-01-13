<template>
    <view class="content">
        <image class="logo" src="../../static/logo.png"></image>
        <view>
            <text class="title">{{title}}</text>
        </view>
        
        <view>
            <!-- TODO 只支持微信小程序和百度小程序 -->
            <!-- <camera device-position="back" flash="off" @error="error" style="width: 100%; height: 300px;"></camera> -->
            <button type="primary" size="mini" @click="takePhoto">拍照</button>
            <image mode="widthFix" :src="src"></image>
        </view>
        
        <view>
            <button type="primary" plain="true" size="mini" v-on:click="scanCode()">扫码</button>
        </view>
        
        <view>
            <button type="primary" plain="true" size="mini" v-on:click="chooseImage()">选图</button>
        </view>
    </view>
</template>

<script>
    export default {
        data() {
            return {
                title: 'Hello',
                src:""
            }
        },
        onLoad() {

        },
        methods: {
            takePhoto : function () {
                // TODO 只支持微信小程序和百度小程序
                /*
                const ctx = uni.createCameraContext();
                ctx.takePhoto({
                    quality: 'normal',
                    success: (res) => {
                        this.src = res.tempImagePath
                    },
                    fail: () => {
                        uni.showToast({
                            title: "拍照fail",
                            mask:true
                        });
                    }
                });
                */
                
                const camera = plus.camera.getCamera();
                camera.captureImage((p) => {
                    plus.io.resolveLocalFileSystemURL(p, (entry) => {
                        this.src = entry.toLocalURL();
                    });
                });
            },
            error(e) {
                console.log(e.detail);
            },
            scanCode : function () {
                uni.scanCode({
                    onlyFromCamera:true,
                    success:function(res){
                        uni.showToast({
                            // title:"scanType: " + res.scanType + " result: " + res.result,
                            title: res.result,
                            mask:true
                        });
                    }
                });
            },
            chooseImage: function() {
                uni.chooseImage({
                    count:9,
                    sizeType:"compressed",
                    success: (res) => {
                        uni.showToast({
                            title: JSON.stringify(res.tempFilePaths),
                            mask:true
                        });
                    }
                });
            }
        }
    }
</script>

<style>
    .content {
        text-align: center;
        height: 300upx;
    }
    .logo{
        height: 60upx;
        width: 60upx;
        margin-top: 50upx;
    }
    .title {
        font-size: 24upx;
        color: #8f8f94;
    }
    
    /** flex布局,每一个容器都必须设置display: flex; */
    .flex-wrp {
        display: flex;
    }
</style>
