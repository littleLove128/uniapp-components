<template>
    <div class="pagination">
        <div :class="total"> {{'total'+total}}</div>

        <ul class="mo-paging">

            <!-- first -->
            <li
                    :class="['paging-item','iconfont', 'paging-item--first', {'paging-item--disabled' : index === 1}]"
                    @click="first" :style="{color:index===1?'rgba(48, 48, 48, 0.5)':'rgba(48, 48, 48, 1)',fontSize:'16px'}">
					&#xe61c;
            </li>
            <!-- prev -->
            <li
                    :class="['paging-item', 'iconfont','paging-item--prev', {'paging-item--disabled' : index === 1}]"
                  :style="{color:index===1?'rgba(48, 48, 48, 0.5)':'rgba(48, 48, 48, 1)',fontSize:'20px'}"  @click="prev">&#xe682;
            </li>

            <li
                    :class="['paging-item', 'paging-item--more']"
                    v-if="showPrevMore">...
            </li>

            <li
                    :class="['paging-item', {'paging-item--current' : index === pager}]"
                    v-for="pager in pagers"
                    :key="pager"
                    @click="go(pager)">{{ pager }}
            </li>
            <li
                    :class="['paging-item', 'paging-item--more']"
                    v-if="showNextMore">...
            </li>
            <!-- next -->
            <li
                    :class="['paging-item','iconfont', 'paging-item--next', {'paging-item--disabled' : index === pages}]"
                    :style="{color:index==pages?'rgba(48, 48, 48, 0.5)':'rgba(48, 48, 48, 1)',fontSize:'20px'}" @click="next">&#xe683;
            </li>
            <!-- last -->
            <li
                    :class="['paging-item','iconfont', 'paging-item--last', {'paging-item--disabled' : index === pages}]"
                    :style="{color:index==pages?'rgba(48, 48, 48, 0.5)':'rgba(48, 48, 48, 1)',fontSize:'16px'}"
                    @click="last">&#xe61b;
            </li>
        </ul>
        <div>goto</div>
        <input ref="input" @keyup.enter="submit(e)" type="number" class="line" v-model="goto" min="1"
               :max="pages"/>
        <div>page</div>
    </div>
</template>

<script>
    export default {
        name: "Pagination",
        props: {

            //页面中的可见页码，其他的以...替代, 必须是奇数
            perPages: {
                type: Number,
                default: 5
            },

            //当前页码
            pageIndex: {
                type: Number,
                default: 1
            },

            //每页显示条数
            pageSize: {
                type: Number,
                default: 10
            },

            //总记录数
            total: {
                type: Number,
                default: 0
            },

        },
        created(){
            document.onkeydown = this.submit;
        },
        methods: {
            // 监听回车事件
            submit() {
                let e = window.event;
                if (e.keyCode == 13) {
                    if(this.goto){// 防止回车事件执行两次
                        if(this.goto>this.pages){
                            this.goto = this.pages;
                        }
                        if(this.goto<1){
                            this.goto = 1;
                        }
                        this.goto = parseInt(this.goto);
                        this.go(this.goto);
                        this.goto = null;
                    }

                }
            },
            prev() {
                if (this.index > 1) {
                    this.go(this.index - 1)
                }
            },
            next() {
                if (this.index < this.pages) {
                    this.go(this.index + 1)
                }
            },
            first() {
                if (this.index !== 1) {
                    this.go(1)
                }
            },
            last() {
                if (this.index != this.pages) {
                    this.go(this.pages)
                }
            },
            go(page) {
                if (this.index !== page) {
                    this.index = page;

//父组件通过change方法来接受当前的页码
                    this.$emit('change', this.index)
                }
            }
        },
        computed: {
            //计算总页码
            pages() {
                return Math.ceil(this.size / this.limit)
            },
            //计算页码，当count等变化时自动计算
            pagers() {
                const array = [];
                const perPages = this.perPages;//页面中可见页码 5
                const pageCount = this.pages;//共几页
                let current = this.index;
                const _offset = (perPages - 1) / 2;


                const offset = {
                    start: current - _offset,
                    end: current + _offset
                }

                //-1, 3
                if (offset.start < 1) {
                    offset.end = offset.end + (1 - offset.start)
                    offset.start = 1
                }
                if (offset.end > pageCount) {
                    offset.start = offset.start - (offset.end - pageCount)
                    offset.end = pageCount
                }
                if (offset.start < 1) offset.start = 1

                this.showPrevMore = (offset.start > 1)
                this.showNextMore = (offset.end < pageCount)

                for (let i = offset.start; i <= offset.end; i++) {
                    array.push(i)
                }

                return array
            }
        },
        data() {
            return {
                index: this.pageIndex, //当前页码
                limit: this.pageSize, //每页显示条数
                size: this.total || 1, //总记录数
                showPrevMore: false,
                showNextMore: false,
                goto: null,//input的value
            }
        },
        watch: {
            //如果父元素传过来的当前页面变了也改变子元素的当前页面
            pageIndex(val) {
                this.index = val || 1
            },
            pageSize(val) {
                this.limit = val || 10
            },
            total(val) {
                this.size = val || 1
            }
        }
    }

</script>

<style scoped lang="scss">
    .pagination {
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
        .total{
            margin-right:27px;
        }
        > div {
            color: rgba(48, 48, 48, .5);
        }

        .line {
            height: 15px;
            width: 33px;
            border: 1px solid rgba(211, 211, 211, .5);
            border-radius: 3px;
            margin: 0 8px;
        }

        input::-webkit-outer-spin-button,
        input::-webkit-inner-spin-button {
            -webkit-appearance: none;
        }

        input[type="number"] {
            -moz-appearance: textfield;
        }
    }

    .mo-paging {
        padding: 0;
        margin: 1rem 0;
        list-style: none;
        user-select: none;
        display: flex;
        align-items: center;
        > .paging-item {
            display: inline;
            position: relative;
            padding: 6px 6px;
            line-height: 1.42857143;
            text-decoration: none;
            background-color: #fff;
            margin-left: -1px;
            cursor: pointer;
            color: rgba(48, 48, 48, .5);

            &:first-child {
                margin-left: 0;
            }

            &:hover {
                color: rgba(48, 48, 48, 1);
            }

            &.paging-item--disabled,
            &.paging-item--more {
                background-color: #fff;
                color: #505050;
            }

            //禁用
            &.paging-item--disabled {
                cursor: not-allowed;
                opacity: .5;
            }

            &.paging-item--more,
            &.paging-item--current {
                cursor: default;
            }
            //选中
            &.paging-item--current {

                color: rgba(48, 48, 48, 1);
                position: relative;
                z-index: 1;
            }
        }
    }
</style>
