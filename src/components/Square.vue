<template>
    <div class="game-cell" @click="onClick" :class="{'game-cell-x': value==='x','game-cell-o': value==='o'}">
        <span>{{value}}</span>
    </div>
</template>

<script>
export default {
    name:'Square',
    props:{
        value:String,
        
    },
    methods:{
        onClick(){
            this.$emit("click");
        }
    }
}
</script>

