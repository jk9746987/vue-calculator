<template>
    <div class="btn_container" @click="keyIn">
        {{num}}
    </div>
</template>

<script>

export default {
    name: 'num',
    props: ['num'],
    created(){
        console.log(this.num)
    },
    methods: {
        keyIn(){
            this.$emit('key-num', this.num)
        }
    }
}
</script>

<style lang="scss" scoped>
.btn_container{
    cursor: pointer;
    width: 100%;
    border-top: 1px solid black;
    border-right: 1px solid black;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

</style>