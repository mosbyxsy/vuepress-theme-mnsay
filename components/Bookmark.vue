<template>
    <main v-else class="page">
        <div class="bookmark" v-if="linkList.length">
            <div class="bookmark-option" v-for="(option, index) in linkList" :key="index">
                <div class="bookmark-state">
                    <span class="bookmark-title">{{option.title}}</span>
                    <span class="bookmark-description">{{option.tip}}</span>
                </div>
                <div class="bookmark-option-wrap" v-if="option.children">
                    <a class="bookmark-item"
                       :title="item.tip || item.detail || item.title"
                       v-for="(item, index) in option.children"
                       @click="item.action && action(option.title, item.action)"
                       :key="index">
                        <div class="bookmark-item-title global-ellipsis">{{item.title}}</div>
                        <div class="bookmark-item-detail global-ellipsis">{{item.detail || item.tips || item.title}}</div>
                    </a>
                </div>
            </div>
        </div>
        <Content/>
    </main>
</template>

<script>
    import axios from 'axios';

    const linkList = [
        {
            title: 'React',
            tip: '前端js框架',
            children: [{
                title: 'React官网',
                tip: 'React官方网站',
                detail: '详细说明',
                link: ''
            }, {
                title: 'antd',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'fusion',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'Ant Design Mobile',
                tip: '基于React的移动端UI库',
                link: ''
            },  {
                title: 'antd2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'fusion2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'Ant Design Mobile2',
                tip: '基于React的移动端UI库',
                link: ''
            }, {
                title: 'antd2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'fusion2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'Ant Design Mobile2',
                tip: '基于React的移动端UI库',
                link: ''
            }, {
                title: 'antd2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'fusion2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'Ant Design Mobile2',
                tip: '基于React的移动端UI库',
                link: ''
            }, {
                title: 'antd2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'fusion2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'Ant Design Mobile2',
                tip: '基于React的移动端UI库',
                link: ''
            }, {
                title: 'antd2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'fusion2',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'Ant Design Mobile2',
                tip: '基于React的移动端UI库',
                link: ''
            }]
        }, {
            title: 'VUE',
            tip: '前端js框架',
            children: [{
                title: 'React官网',
                tip: 'React官方网站',
                link: ''
            }, {
                title: 'antd',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'fusion',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'Ant Design Mobile',
                tip: '基于React的移动端UI库',
                link: ''
            },  {
                title: 'antd',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'fusion',
                tip: 'React UI库',
                link: ''
            }, {
                title: 'Ant Design Mobile',
                tip: '基于React的移动端UI库',
                link: ''
            }]
        }
    ];
    export default {
        components: {
        },
        data () {
            return {
                linkList: []
            }
        },
        mounted () {
            axios.get('https://cdn.jsdelivr.net/gh/vuejs/vuepress/package.json', {
            }).then(result => {
                console.log(result);
                this.linkMap = {};
                linkList.forEach(item => {
                    if (item.children && item.children.length > 11) {
                        this.linkMap[item.title] = item.children;
                        item.children = item.children.slice(0, 11);
                        item.children.push({
                            title: '查看更多',
                            tip: '查看更多',
                            detail: '点击展开更多',
                            action: 'more'
                        })
                    }
                });
                this.linkList = linkList;
            })
        },
        methods: {
            action(option) {
                let optionList = this.linkList.find(item => item.title = option);
                if (optionList && this.linkMap[option]) {
                    optionList.children = this.linkMap[option];
                }
                // this.linkList = this.linkList;
                console.log(optionList, this.linkList);
            }
        }
    }
</script>

<style lang="stylus" scoped>
    .page
        padding-top 3.6rem
        .bookmark
            padding 0 1.5rem
    .bookmark-option
        border-bottom  dotted 1px $borderColor
        .bookmark-state
            font-size 1.2rem
            line-height 1.6rem
            text-overflow ellipsis
            overflow hidden
            white-space nowrap
            padding 0.8rem 0 0.2rem
            .bookmark-description
                color #717171
                font-size 0.8rem
        .bookmark-option-wrap
            font-size 0
            text-align left
    .bookmark-item
        box-sizing border-box
        display inline-block
        width 15rem
        padding 0.4rem 0.8rem
        font-size 1rem
        border-radius 1rem
        max-width 46%
        margin-right 0.8rem
        margin-bottom 0.4rem
        border solid 1px $borderColor
        text-align left
        cursor pointer
        &:hover {
            border-color $accentColor
        }
        .bookmark-item-title {
            color $textColor
            font-weight normal
            line-height 1.6rem
        }
        .bookmark-item-detail {
            color $textColor
            font-weight 300
            font-size 0.8rem
            line-height 1.2rem
        }
    @media (max-width: $MQMobile) {
        .bookmark-option .bookmark-option-wrap {
            text-align center
        }
        .bookmark-item {
            margin 0.4rem
        }
    }
</style>
