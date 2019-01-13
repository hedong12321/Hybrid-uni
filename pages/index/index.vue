<template>
	<view class="content">
        <image class="logo" src="../../static/logo.png"></image>
		<view>
            <text class="title">{{title}}</text>
        </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		methods: {

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
</style>
