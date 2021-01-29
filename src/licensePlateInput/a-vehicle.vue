<template>
  <div class="add_car">
    <div class="contentDiv" >
        <div class="selectLicensePlateNum">
            <ul>
                <li class="plateNumDiv" :class="{'active': clickIndex === 1}" @click="getKeyChina">
                    <!-- <input type="text" size="1" onfocus='this.blur();' v-model="plate1"> -->
                    <div v-text="plate1"></div>
                </li>
                <li class="plateNumDiv" :class="{'active': clickIndex === 2}" @click="getKeyEnglish(2)">
                    <!-- <input type="text" size="1" onfocus='this.blur();' v-model="plate2"> -->
                    <div v-text="plate2"></div>
                </li>
                <li class="dian"></li>
                <li class="plateNumDiv" :class="{'active': clickIndex === 3}" @click="getKeyEnglish(3)">
                    <!-- <input type="text" size="1" onfocus='this.blur();' v-model="plate3"> -->
                    <div v-text="plate3"></div>
                </li>
                <li class="plateNumDiv" :class="{'active': clickIndex === 4}" @click="getKeyEnglish(4)">
                    <!-- <input type="text" size="1" onfocus='this.blur();' v-model="plate4"> -->
                    <div v-text="plate4"></div>
                </li>
                <li class="plateNumDiv" :class="{'active': clickIndex === 5}" @click="getKeyEnglish(5)">
                    <!-- <input type="text" size="1" onfocus='this.blur();' v-model="plate5"> -->
                    <div v-text="plate5"></div>
                </li>
                <li class="plateNumDiv" :class="{'active': clickIndex === 6}" @click="getKeyEnglish(6)">
                    <!-- <input type="text" size="1" onfocus='this.blur();' v-model="plate6"> -->
                    <div v-text="plate6"></div>
                </li>
                <li class="plateNumDiv" :class="{'active': clickIndex === 7}" @click="getKeyEnglish(7)">
                    <!-- <input type="text" size="1" onfocus='this.blur();' v-model="plate7"> -->
                    <div v-text="plate7"></div>
                </li>
                <li v-if="plate3 === 'D' || plate3 === 'F'" class="plateNumDiv" :class="{'active': clickIndex === 8}" @click="getKeyEnglish(8)">
                    <!-- <input type="text" size="1" onfocus='this.blur();' v-model="plate8"> -->
                    <div v-text="plate8"></div>
                </li>
                <li v-else class="plateNumDiv plateNumDiv8">
                    <i></i>
                </li>
            </ul>
        </div>
    </div>
    <div>
        <!-- <button @click="keyState = true">键盘</button> -->
        <keyword :isShow="keyState" :keyBoardType="keyBoardType" @exit="exit" @inputchange="getKey" :oinp="str" @ok="confirm"/>
    </div>
  </div>
</template>
<script>
import keyword from './keyword'
import { Cell, Button, Search, Icon, Field } from 'vant'
export default {
    props:{
        plateNumber: {
            type: String,
        }
    },
  name: 'addAVehicle',
  // 车牌组件   
  components: {
    keyword,
    'van-cell': Cell,
    'van-button': Button,
    'van-search': Search,
    'van-icon': Icon,
    'van-field': Field,
  },
  data () {
    return {
        keyState: false,
        // isShow: false,
        str: "",
        strArr: '',
        keyBoardType: 1,
        clickIndex: null,
        plate1: '',
        plate2: '',
        plate3: '',
        plate4: '',
        plate5: '',
        plate6: '',
        plate7: '',
        plate8: '',
        userName: '',
        tel: '',
        message: ''
    }
  },
 
  computed: {
      isShow () {
        if (this.plate3 === 'D' || this.plate3 === 'F') {
            if (this.strArr.length === 8 && this.userName !== '' && this.tel !== '') {
                return true
            }
        } else {
            if (this.strArr.length === 7 && this.userName !== '' && this.tel !== '') {
                return true
            }
        }
      }
  },
  created () {
  },
  methods: {
    
    getKeyChina () {
        setTimeout(() => {
            this.keyState = true
            this.keyBoardType = 1
            this.clickIndex = 1
        }, 500)
    },
    getKeyEnglish (i) {
        setTimeout(() => {
            this.keyState = true
            this.keyBoardType = 2
            this.clickIndex = i
        }, 500)
    },
    exit () {
        this.keyState = false
    },
    getKey (val) {
        // if (this.str.length >= 8&&val!="delete") {
        //     return false
        // }
        if(val == 'delete'){
            if (this.clickIndex === 1) {
                this.plate1 = ''
            } else if (this.clickIndex === 2) {
                this.plate2 = ''
                this.keyBoardType = 1
                this.clickIndex = 1
            } else if (this.clickIndex === 3) {
                this.plate3 = ''
                this.clickIndex = 2
            } else if (this.clickIndex === 4) {
                this.plate4 = ''
                this.clickIndex = 3
            } else if (this.clickIndex === 5) {
                this.plate5 = ''
                this.clickIndex = 4
            } else if (this.clickIndex === 6) {
                this.plate6 = ''
                this.clickIndex = 5
            } else if (this.clickIndex === 7) {
                this.plate7 = ''
                this.clickIndex = 6
            } else if (this.clickIndex === 8) {
                this.plate8 = ''
                this.clickIndex = 7
            } 
            // this.str = this.str.slice(0, this.str.length-1)
            // this.strArr = this.strArr.splice(0, 1)
        }else{
            // this.str+=val
            if (this.clickIndex === 1) {
                this.plate1 = val
                this.clickIndex = 2
                this.keyBoardType = 2
            } else if (this.clickIndex === 2) {
                this.plate2 = val
                this.clickIndex = 3
            } else if (this.clickIndex === 3) {
                this.plate3 = val
                this.clickIndex = 4
            } else if (this.clickIndex === 4) {
                this.plate4 = val
                this.clickIndex = 5
            } else if (this.clickIndex === 5) {
                this.plate5 = val
                this.clickIndex = 6
            } else if (this.clickIndex === 6) {
                this.plate6 = val
                this.clickIndex = 7
            } else if (this.clickIndex === 7) {
                this.plate7 = val
                if (this.plate3 === 'D' || this.plate3 === 'F') {
                    this.clickIndex = 8
                }
            } else if (this.clickIndex === 8) {
                this.plate8 = val
            }
        }
        this.strArr = this.plate1 + this.plate2 + this.plate3 + this.plate4 + this.plate5 + this.plate6 + this.plate7 + this.plate8;
        this.$emit("update:plateNumber", this.strArr);
        if (this.plate3 === 'D' || this.plate3 === 'F') {
            if (this.strArr.length === 8) {
                // this.isShow = true
                this.confirm()
            }
        } else {
            if (this.strArr.length === 7) {
                // this.isShow = true
                this.confirm()
            }
        }
    },
    confirm (e) {
        this.keyState = false
    },
  },
  watch: {
  }

}
</script>
<style scoped lang='less'>
  .add_car {
    background: #F2F3F5;
    .contentDiv {
        // background: #fff;
        .selectLicensePlateNum {
            padding: 16px 16pX 5pX;
            font-size: 16px;
            background: #fff;
            h6 {
                margin: 10px 0;
                font-size: 16px;
                color: #1B1C33;
            }
            ul {
                display: flex;
                align-items: center;
                justify-content: space-between;
                padding: 16px 0;
                .plateNumDiv {
                    width: 60px;
                    height: 60px;
                    // padding: 7px 13.5px;
                    text-align: center;
                    line-height: 60px;
                    border: 1px solid #D1D1DA;
                    color: #5E5E66;
                    border-radius: 5px;
                    overflow: hidden;
                    input {
                        width: 26px;
                        height: 37px;
                        border: 0;
                        padding:  0 5px 0;
                        margin: 0;
                        text-align: center;
                    }
                    div{
                        height: 100%;
                        text-align: center;
                        font-size: 28px;
                    }
                }
                .active.plateNumDiv {
                    border: 1px solid #209B57;
                }
                .dian {
                    width: 6px;
                    height: 6px;
                    border-radius: 100%;
                    background: #D1D1DA;
                }
                .plateNumDiv8 {
                    border: 1px dashed #D1D1DA;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    flex-wrap: wrap;
                    i {
                        display: block;
                        width: 46px;
                        height: 47px;
                        background: url('./images/nowJia.png') no-repeat center;
                        background-size: 46px;
                    }
                }
            }
            
        }
        .annotationDiv {
            color: #FF4040;
            font-size: 12px;
            padding-left: 16px;
            padding-top: 16px;
        }
       
    }
  }
</style>