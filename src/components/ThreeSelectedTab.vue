<template>
    <div class="mounth-data">
        <div class="mounth-data-tab-model">
            <p v-for="(item,index) in mounthData" @click="tabClick(item,index)" class="mounth-data-tab-title">
                <span v-bind:class="{'mounth-data-tab-title-up':item.isActive}" v-text="item.title"></span>
                <!--<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" v-bind:class="{'vux-x-icon-act':item.isActive}" class="vux-x-icon vux-x-icon-ios-arrow-down">
                    <path d="M396.6 160l19.4 20.7L256 352 96 180.7l19.3-20.7L256 310.5z"></path>
                </svg>-->
            </p>
        </div>
        <ul v-if="isHidden" class="mounth-data-tab-list">
            <li v-bind:class="{'mounth-data-tab-list-act':item.isSelected}" @click="selectedVal(item);" v-for="(item,index) in contentList" v-text="item.yearTxt"></li>
        </ul>
    </div>
</template>

<style>
    @import "../style/mounthData.css";
</style>
<script>
    export default {
        name: 'three-selected-tab',
        data () {
            return {
                contentList: null,
                isHidden: false,
                selectedIndex: 0,
                selectedData: {
                    mounth: '',
                    range: '',
                    type: ''
                }
            }
        },
        props:['mounthData'],
        components: {

        },
        methods: {
            //tab选项卡切换
            tabClick(obj, index){
                this.selectedIndex = index;
                //当前被选中
                if (obj.isActive) {
                    obj.isActive = false;
                    this.isHidden = obj.isActive;
                } else {//未选中
                    //初始化所有小箭头isActive = false;
                    this.mounthData.map((item) => {
                        item.isActive = false;
                    });
                    obj.isActive = !obj.isActive;
                    this.isHidden = obj.isActive;
                    //初始化isSelected = false;
                    obj.dataList.map((item) => {
                        item.isSelected = false;
                    });
                    //binded  li data
                    this.contentList = obj.dataList;
                }
            },
            //list选val
            selectedVal(obj){
                this.contentList.map((item) => {
                    item.isSelected = false;
                });
                obj.isSelected = true;
                //三个选项卡选中的值
                switch (this.selectedIndex) {
                    case 0:
                        this.selectedData.mounth = obj.yearTxt;
                        break;
                    case 1:
                        this.selectedData.range = obj.yearTxt;
                        break;
                    case 2:
                        this.selectedData.type = obj.yearTxt;
                }
                this.selectedData.mounth && this.selectedData.range && this.selectedData.type && alert(`
                选择值为：${this.selectedData.mounth}-${this.selectedData.range}-${this.selectedData.type}
                    `);

            }
        },
        mounted(){

        },
        created(){

        }
    }
</script>