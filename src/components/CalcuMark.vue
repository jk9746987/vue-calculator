<template>
    <div class="symbol_container" @click="keyIn">
        <div >
            {{symbol}}
        </div>
    </div>
</template>

<script>
export default {
    name: 'ClacuMark',
    props: ['symbol'],
    data(){
        return{

        }
    },
    created(){
        // console.log(this.symbol)
    },
    methods: {
        keyIn(){
            this.$emit('key-calcu', this.symbol)
        }
    }
}
</script>

<style lang="scss">
.symbol_container{
    width: 100%;
    cursor: pointer;
    border-top: 1px solid black;
    border-left: 1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 48px;
    flex-grow: 1;

    // div{
    //     width: 50px;
    //     height: 50px;
    //     display: flex;
    //     justify-content: center;
    //     align-items: center;
    // }
}

.symbol_container:nth-child(3){
    div{
        position: relative;
        top: 8px;
    }
}


</style>