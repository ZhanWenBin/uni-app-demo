<template>
	<view class="content">
		 <swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" class="swiper" :style="{'height':windowHeight}"
         @animationfinish="animationfinish">
            <swiper-item>
                <view class="swiper-item" :style="{'height':windowHeight,'background-color':'red'}">A</view>
            </swiper-item>
            <swiper-item>
                <view class="swiper-item" :style="{'height':windowHeight,'background-color':'green'}">B</view>
            </swiper-item>
            <swiper-item>
                <view class="swiper-item" :style="{'height':windowHeight,'background-color':'pink'}">C</view>
            </swiper-item>
            <swiper-item>
                <view class="swiper-item" :style="{'height':windowHeight,'background-color':'yellow'}">进入首页</view>
            </swiper-item>
        </swiper>
        <text :style="{color:'red','font-weight':200}">这是一个sssH1</text>
	</view>
</template>

<script>
	export default {
		data() {
            return {
                windowHeight: '603px'  //定义手机屏幕高度值变量
            }
        },
        onLoad() {
            var _me = this;
            uni.getSystemInfo({//获取手机屏幕高度信息，让swiper的高度和手机屏幕一样高
                success: function(res) {
                    console.log(res.model);
                    console.log(res.pixelRatio);
                    console.log(res.windowWidth);
                    console.log(res.windowHeight);//这里是手机屏幕高度
                    console.log(res.language);
                    console.log(res.version);
                    console.log(res.platform);
                    _me.windowHeight = res.windowHeight + 'px';
                    console.log('手机屏幕高度为' + _me.windowHeight);
                }
            });
        },
        methods: {
            animationfinish(e) {
                console.log(JSON.stringify(e.detail.current));
                //判断到最后一张后，自动转向进入首页
                if (e.detail.current == 3) {
                    console.log('动画已经播放结束');
                    setTimeout(function() {
						console.info(uni)
                        uni.switchTab({
                            url: '/pages/views/book/index'
                        });
                    }, 1000)
                }
            }
        }
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
	.swiper {
        width: 100%;
        /*     height: 100vw; */
        /* background: red; */
    }
</style>
