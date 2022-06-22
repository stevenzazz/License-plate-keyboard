
<script setup>
import { reactive, ref, watch } from "vue";
import Taro from '@tarojs/taro'

const provinceText = ['贵', '粤', '京', '冀', '沪', '津', '晋', '蒙', '辽', '吉', '黑', '苏', '浙', '皖', '闽', '赣', '鲁', '豫', '鄂', '湘', '桂', '琼', '渝', '川', '云', '藏', '陕', '甘', '青', '宁']
const lastWordText = ['新', '港', '澳', '学', '领', '警']
const numText = ['0','1', '2', '3', '4', '5', '6','7', '8', '9']
const wordText = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'J', 'K', 'L', 'M', 'N', 'P', 'Q', 'R', 'S', 'T', 'U', 'V']
const lastWordText2 = ['W', 'X', 'Y', 'Z']

const emit = defineEmits(['confirm'])

const state = reactive({
    licensePlateShow: false,
    licensePlate: '',
    licensePlateLetter: false
})

const confirm = () => {
    // 执行父组件方法 并携带车牌信息
    state.licensePlateShow = false
    emit('confirm', state.licensePlate)
}

const showPopup = () => {
    state.licensePlateShow = true
}

const openLicensePlate = () => {
    state.licensePlateShow = true
}

const onText = (value) => {
    // 限制车牌位数
    if (state.licensePlate.length > 7) return
    state.licensePlate = state.licensePlate + value
}

const deleteText = () => {
    state.licensePlate = state.licensePlate.substring(0, state.licensePlate.length - 1);
}

watch(() => state.licensePlate, (value) => {
    console.log(value)
    if (value.length == 1) {
        state.licensePlateLetter = true
    }
    if (value.length == 0) {
        state.licensePlateLetter = false
    }
})

// 向外暴露方法
defineExpose({ showPopup })
</script>

<template>
    <nut-popup pop-class="popclass" position="bottom" v-model:visible="state.licensePlateShow" :z-index="100">
        <div class="header flex flex-col-center">
            <div class="title">才风专用车牌键盘</div>
            <div class="confirm" @click='confirm'>完成</div>
        </div>
        <div class="header flex" v-if="state.licensePlate" style="height:30px">
            <div class="title" style="margin: 0 auto;">{{ state.licensePlate }}</div>
        </div>
        <div class="main" v-if="!state.licensePlateLetter">
            <div class="flex flex-ju-ev flex-warp">
                <div class="provinces" v-for="item in provinceText" :key="item" @click="onText(item)">{{ item }}</div>
            </div>
            <div class="flex flex-ju-ev">
                <div class="provinces abc" style="background:#b2bcc5" @click="state.licensePlateLetter = true">abc</div>
                <div class="provinces" v-for="item in lastWordText" :key="item" @click="onText(item)">{{ item }}</div>
                <div class="provinces close flex flex-col-center flex-row-center" style="background:#b2bcc5;"
                    @click="deleteText">
                    <nut-icon name="close-little"></nut-icon>
                </div>
            </div>
        </div>
        <div class="main" v-if="state.licensePlateLetter">
        <div class="flex flex-ju-ev flex-warp">
                <div class="provinces" v-for="item in numText" :key="item" @click="onText(item)">{{ item }}</div>
            </div>
            <div class="flex flex-ju-ev flex-warp">
                <div class="provinces" v-for="item in wordText" :key="item" @click="onText(item)">{{ item }}</div>
            </div>
            <div class="flex flex-ju-ev">
                <div class="provinces w108" style="background:#b2bcc5" @click="state.licensePlateLetter = false">字</div>
                <div class="provinces" v-for="item in lastWordText2" :key="item" @click="onText(item)">{{ item }}</div>
                <div class="provinces w108 close flex flex-col-center flex-row-center" style="background:#b2bcc5;"
                    @click="deleteText">
                    <nut-icon name="close-little"></nut-icon>
                </div>
            </div>
        </div>
    </nut-popup>
</template>

<style lang="scss">
.header {
    width: 375px;
    height: 44px;

    .title {
        color: #247edc;
        font-weight: 800;
        margin-left: 133px;
    }

    .confirm {
        color: #247edc;
        font-weight: 800;
        margin-left: 84px;
    }
}

.main {
    background-color: #d1d6d9;
    width: 375px;
    height: 220px;

    .close {
        width: 71px !important;
    }

    .abc {
        width: 71px !important;
    }

    .w108 {
        width: 108px !important;
    }

    .provinces {
        width: 35px;
        height: 40px;
        background-color: #fff;
        color: #000;
        text-align: center;
        line-height: 40px;
        border-radius: 5px;
        margin-top: 6px;
        box-shadow: 0px 1px 2px #333333;

        &:active {
            background-color: #80a4ff !important;
        }

        .closeIcon {
            width: 32px;
            height: 32px;
        }
    }
}
</style>