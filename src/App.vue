<template>
    <div id="app">
        <div class="show">{{this.$store.state.key_data}}</div>
        <div class="container">
            <div class="left">
                <Num :num="item" v-for="(item, index) in num" :key="index" @key-num="keyNum"/>
            </div>
            <div class="right">
                <CalcuMark :symbol="item" v-for="(item, index) in symbol" :key="index" @key-calcu="keyCalcu" />
            </div>
        </div>
    </div>
</template>

<script>
import Num from './components/Num.vue'
import CalcuMark from './components/CalcuMark.vue'
export default {
    name: "app",
    components: {
        Num,
        CalcuMark
    },
    data(){
        return{
            num: ['AC', '←', 7, 8, 9, 4, 5, 6, 1, 2, 3, 0, '.'],
            symbol: ['+', '-', '*', '/', '='],
            now: "",
            before: "",
            save: "",
            keyin: null,
            useCalcu: true,
            useSymbol: "",
            beforeSymbol: "",
            calcuNumber: "",
        }
    },
    created(){
        console.log(typeof(this.now))
    },
    methods: {
        keyNum(value){
            if(value === 0 || value === 1 || value === 2 || value === 3 || value === 4 || value === 5 || value === 6 || value === 7 || value === 8 || value === 9){
                if(this.now.length <= 10){
                    if(this.now === 0){
                        this.now = "";
                        this.$store.state.key_data = 0;
                    }else{
                        this.now += value;
                        this.$store.state.key_data = this.now;
                        console.log(this.$store.state.key_data)
                    }
                }else{
                    return false
                }
                if(this.before || this.before === 0){
                    this.calcuNumber = eval(`${this.before} ${this.useSymbol} ${this.now}`)
                }
            }
            if(value === "AC"){
                this.now = "";
                this.$store.state.key_data = 0;
                this.save = "";
                this.calcuNumber = "";
                this.before = "";
            }
            if(value === "."){
                // 若是沒包含 "."，則可加小數點，有的話則不執行
                if(!this.now.includes(".")){
                    if(this.now === "" || this.now === "."){
                        this.now = "0" + ".";
                    }else{
                        this.now += ".";
                    }
                }
                console.log(this.now)
            }
            if(value === "←"){
                // 截取字串從頭到倒數第二個字
                if(this.calcuNumber){
                    if(this.useSymbol){
                        let numberLength = String(this.calcuNumber).length;
                        this.calcuNumber = String(this.calcuNumber).slice(0, numberLength - 1);
                        this.$store.state.key_data = this.calcuNumber;
                        this.now = this.calcuNumber;
                        if(this.calcuNumber === ""){
                            this.$store.state.key_data = 0;
                        }
                    }else{
                        return false
                    }
                }else if(this.before){
                    return false
                }else{
                    let strNow = String(this.calcuNumber).length;
                    this.now = String(this.now).slice(0 , strNow - 1);
                    this.$store.state.key_data = this.now
                    if(this.now === ""){
                        this.$store.state.key_data = 0;
                    }
                }
                console.log(this.$store.state.key_data)
                console.log(this.now)
            }
        },
        keyCalcu(value){
            switch(value){
                case "+":
                    if(this.before === ""){
                        this.save = this.now
                        this.before = Number(this.save)
                        this.now = ""
                        console.log('hahaha')
                        if(this.calcuNumber){
                            this.$store.state.key_data = this.calcuNumber
                            this.before = this.calcuNumber
                            this.save = this.now
                            this.now = ""
                            console.log(this.calcuNumber)
                        }
                    }else{
                        if(this.calcuNumber){
                            this.$store.state.key_data = this.calcuNumber
                            this.before = this.calcuNumber
                            this.save = this.now
                            this.now = ""
                            console.log(this.calcuNumber)
                        }
                    }
                    // this.useSymbol = value;
                    console.log(this.useSymbol)
                    break;
                case "-":
                    if(this.before === ""){
                        this.save = this.now
                        this.before = Number(this.save)
                        this.now = ""
                        if(this.calcuNumber){
                            this.$store.state.key_data = this.calcuNumber
                            this.before = this.calcuNumber
                            this.save = this.now
                            this.now = ""
                            console.log(this.calcuNumber)
                        }
                    }else{
                        if(this.calcuNumber){
                            this.$store.state.key_data = this.calcuNumber
                            this.before = this.calcuNumber
                            this.save = this.now
                            this.now = ""
                        }
                    }
                    // this.useSymbol = value;
                    break;
                case "*":
                    if(this.before === ""){
                        this.save = this.now
                        this.before = Number(this.save)
                        this.now = ""
                        if(this.calcuNumber){
                            this.$store.state.key_data = this.calcuNumber
                            this.before = this.calcuNumber
                            this.save = this.now
                            this.now = ""
                            console.log(this.calcuNumber)
                        }
                    }else{
                        if(this.calcuNumber){
                            this.$store.state.key_data = this.calcuNumber
                            this.before = this.calcuNumber
                            this.save = this.now
                            this.now = ""
                        }
                    }
                    // this.useSymbol = value;
                    break;
                case "/":
                    if(this.before === ""){
                        this.save = this.now
                        this.before = Number(this.save)
                        this.now = ""
                        if(this.calcuNumber){
                            this.$store.state.key_data = this.calcuNumber
                            this.before = this.calcuNumber
                            this.save = this.now
                            this.now = ""
                            console.log(this.calcuNumber)
                        }
                    }else{
                        if(this.calcuNumber){
                            this.$store.state.key_data = this.calcuNumber
                            this.before = this.calcuNumber
                            this.save = this.now
                            this.now = ""
                        }
                    }
                    // this.useSymbol = value;
                    break;
                case "=":
                    if(!this.before){
                        if(this.calcuNumber === ""){
                            return false
                        }
                        this.$store.state.key_data = this.calcuNumber;
                        this.before = ""
                        this.save = ""
                        this.now = ""
                        this.calcuNumber = ""
                    }else{
                        if(String(this.calcuNumber).length >= 10){
                            this.calcuNumber = String(this.calcuNumber).slice(0, 10);
                            this.$store.state.key_data = this.calcuNumber
                            this.before = ""
                            this.save = ""
                            this.now = ""
                            console.log('hahaha')
                        }else{
                            this.$store.state.key_data = this.calcuNumber
                            this.before = ""
                            this.save = ""
                            this.now = ""
                        }
                    }
                    break;
                default:
                    break;
            }
            this.useSymbol = value;
            console.log(this.useSymbol)
        },
    },
    computed: {
        
    }
}
</script>

<style lang="scss">
#app{
    width: 500px;
    margin: 0 auto;
    padding-top: 3%;
    font-size: 36px;

    .show{
        background-color: black;
        color: white;
        text-align: end;
        font-size: 72px;
        padding: 10% 10% 10% 0;
        border-radius: 20px 20px 0 0;
    }

    // 去掉雙箭頭 /* Chrome, Safari, Edge, Opera */
    input[type=number]::-webkit-outer-spin-button,
    input[type=number]::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }

    // firefox
    input[type=number] {
        -moz-appearance: textfield;
    }

    .container{
        width: 100%;
        display: flex;
        height: 500px;

        .left{
            width: 400px;
            background-color: #D3D3D3;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            justify-items: center;
            align-items: center;
            border-bottom: 1px solid black;
            border-left: 1px solid black;
            border-radius: 0 0 0 20px;

            .btn_container:nth-child(1){
                grid-column-start: 1;
                grid-column-end: 3;
            }

            .btn_container:nth-child(12){
                grid-column-start: 1;
                grid-column-end: 3;
            }

        }

        .right{
            background-color: #FF8033;
            display: flex;
            flex-direction: column;
            width: calc(100% - 400px);
            border-right: 1px solid black;
            border-bottom: 1px solid black;
            border-radius: 0 0 20px 0;
        }
    }
}


</style>
