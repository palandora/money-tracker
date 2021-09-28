<template>
    <div class="cta-bar">
        <span v-if="showSecondary">Cancel</span>
        <div class="button" @click="action()">
            <img :src="setImage(currentEntry)" alt="">
        </div>
    </div>
</template>

<script>
export default {
    name: 'cta-bar',
    data(){
        return {
            
        }
    },
    props:{
        showSecondary: {
            type: Boolean,
            default: true
        },
        currentEntry: Object,
        createEntry: Function,
        updateEntry: Function
    },
    methods:{
        setImage(hasEntry){
            if(hasEntry){
                return require('../assets/icons/refresh.svg')
            }else{
                return require('../assets/icons/add.svg')
            }
        },
        action(){
            if(this.showSecondary){
                if(this.currentEntry){
                    console.log("update existing entry")
                }else{
                    console.log("add new object")
                }
            }else{
                console.log("new empty object")
            }
            
        }
    }
    
}
</script>

<style scoped>
    .cta-bar{
        display:flex;
        justify-content: flex-end;
        align-items: center;
        gap:16px;
        padding: 16px;
        border-top: 1px solid var(--ui-divider);
    }
    .cta-bar > *{
        cursor: pointer;
    }
    .button{
        padding: 8px 16px;
        border-radius: 34px;
        background: var(--ui-accent-green)
    }
    img{
        display: block;
    }
</style>