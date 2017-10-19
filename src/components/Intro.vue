<template>
    <div class="intro-block j-intro-block">
        <div class="style-block" v-html="styleFinal"></div>
        <pre class="display-block" ref="displayBlock">{{textFinal}}</pre>
        <div class="intro-box">
            <div class="intro-box-main" v-show="showIntro">
                <p class="intro-box-hide">&emsp;&emsp;我叫郑朝禹，毕业于桂林电子科技大学</p>
                <p class="intro-box-hide">&emsp;&emsp;16年年初开始在深圳软通动力相关部门，从事前端开发工作</p>
                <p class="intro-box-hide">&emsp;&emsp;擅长页面、前后端交互</p>
                <p class="intro-box-hide">&emsp;&emsp;在公司主要做外包页面以及数据交互的开发</p>
                <p class="intro-box-hide">&emsp;&emsp;平时工作用到的框架技术Angular、Vue及相关技术栈、Nodejs(主要是Express)</p>
                <h3 class="intro-box-hide">&emsp;&emsp;部分参与的项目：</h3>
                <ul class="intro-list-task">
                    <li class="intro-box-hide">
                        <p class="c-fff">2016：<a class="ud" href="dongsheng1992.cn" target="_blank">商城框架</a>+还没做完、就由后面的同事慢慢迭代了</p>
                        <p class="intro-text-desc">主要功能有购物车<br>
                            还有好多慢慢写吧<br>
                            </p>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'intro',
        data () {
            return {
                talk: this.$store.state.talk,
                start:true,
                showResult: false,
                closeText: false,
                showBtn: false,
                style: `
/* ......
* 厉害了我的哥，这下玩坏了吧！
* 没办法，那只能重新造一个网页了╮(╯_╰)╭
*/

/* 首先给所有元素加上过渡效果 */
* {
    -webkit-transition: all .3s;
    transition: all .3s;
}
/* 还是用绚烂的星空背景才有逼格 */
html,body {
    background-image: url("https://t.cn/RotuF4m");
    color: #333;
}
/* 好歹还是加个边框吧 */
.display-block {
    padding: 10px;
    border: 2px solid rgb(0,155,255);
    margin: 10px;
    overflow: auto;
    width: 400px; height: 90vh;
    float: left;
    background: rgba(0,155,255,0.5);
}
/* 还差一个版块来介绍自己 */
.intro-box{
    padding: 12px;
    background: rgba(0,55,205,0.3);
    margin: 10px;
    min-height: 110vh;
    overflow: hidden;
}
/* 使命完成了，给主要的版块让让位置吧 */
.display-block {
    transform-origin: 0 50%;
    -webkit-transform: rotateY(30deg);
    transform: rotateY(30deg);
    margin-right: -100px;
}
`,
                currLen: 0,
                showIntro: false
            }
        },
        computed: {
            styleFinal(){
                return `<style>${this.style.substring(0,this.currLen)}</style>`
            },
            textFinal(){
                return `${this.style.substring(0,this.currLen)}`
            }
        },
        created () {
            let len = this.style.length;
            let _this = this;

            this.$nextTick(function () {
                new Promise(function (resolve) {
                    function appendStyle() {
                        if(_this.currLen === len){
                            resolve();
                        }
                        _this.currLen++;
                        _this.$refs.displayBlock.scrollTop = 9999;
                        setTimeout(appendStyle,30);
                    }
                    appendStyle();
                }).then(function () {
                    _this.showIntro = true;
                    document.body.setAttribute('class', '');
                    let introBoxHide = document.querySelectorAll(".intro-box-hide");
                    let len = introBoxHide.length;
                    for (let i = 0; i < len; i++) {
                        (function (i) {
                            setTimeout(function () {
                                introBoxHide[i].classList.add('show');
                            },i*500);
                        })(i)
                    }
                });
            });
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
    html,body{
        background-color: #000!important;
    }

    .intro-block{
        overflow: hidden;
        perspective: 1000px;
        perspective-origin: 10px 400px;
    }
    .display-block{
        color: #fff;
    }
    .intro-box{
        color: #eee;
        font-size: 18px;
        line-height: 1.5;
    }
    .c-fff{
        color: #fff;
    }
    .intro-text-desc{
        font-size: 14px;
        color: #ececec;
    }
    .intro-list-task>li{
        margin-bottom: 40px;
    }
    .intro-box-hide{
        visibility: hidden;
    }
    .intro-box-hide.show{
        animation: show 1s;
        animation-fill-mode: forwards;
    }
    @keyframes show {
        0%{
            visibility: visible;
            opacity: 0;
            transform: translate(100px,-20px);
        }
        100%{
            opacity: 1;
            visibility: visible;
            transform: translate(0,0);
        }
    }
</style>
