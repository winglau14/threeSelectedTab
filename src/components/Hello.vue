<template>
        <ThreeSelectedTab :mounth-data="mounthData"></ThreeSelectedTab>
</template>

<script>
    import ThreeSelectedTab from "./ThreeSelectedTab";

    //已知当前月份往后推5个月
    const iMounth = new Date().getMonth() + 1;
    const mounthArray = [];
    const getForBackMounth = function (iMounth, forBackVal) {
        const tempArray = [];
        //<=5月
        if (iMounth <= forBackVal) {
            for (let i = iMounth; i > iMounth - forBackVal && i <= forBackVal; i--) {
                tempArray.push(i);
            }
        } else {
            //>5月
            for (let i = iMounth; i > iMounth - forBackVal; i--) {
                tempArray.push(i);
            }
        }
        //再换算成需要的月份
        tempArray.map((item) => {
            let currentYear = new Date().getFullYear();
            let tempObj = {
                isSelected: false,
                yearTxt: null
            };
            if (item <= 0) {
                //小于12月减一年
                currentYear = currentYear - 1;
                item = item + 12;
            }
            tempObj.yearTxt = `${currentYear}年${item}月`;
            mounthArray.push(tempObj);
        });
    };
    getForBackMounth(iMounth, 5);

    export default {
        name: 'three-selected-tab',
        components: {
            ThreeSelectedTab
        },
        data () {
            return {
                mounthData: [
                    {
                        isActive: false,
                        title: '近5个月',
                        dataList: mounthArray
                    }, {
                        isActive: false,
                        title: '范围',
                        dataList: [
                            {
                                isSelected: false,
                                yearTxt: '1'
                            },
                            {
                                isSelected: false,
                                yearTxt: '2'
                            },
                            {
                                isSelected: false,
                                yearTxt: '3'
                            }
                        ]
                    }, {
                        isActive: false,
                        title: '类型',
                        dataList: [
                            {
                                isSelected: false,
                                yearTxt: '门店'
                            },
                            {
                                isSelected: false,
                                yearTxt: '线上'
                            }
                        ]
                    }
                ]
            }
        }
    }
</script>

