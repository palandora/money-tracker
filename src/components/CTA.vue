<template>
    <div class="cta-bar">
        <span v-if="showSecondary">Cancel</span>
        <div class="button" @click="action()">
            <img :src="setImage(newEntry.state)" alt="">
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
        createEntry: Function,
        updateEntry: Function,
        checkInputs: Function
    },
    methods:{
        setImage(existingEntry){
            if(!this.showSecondary){
                return require('../assets/icons/add.svg')
            }else{
                if(!existingEntry){
                    return require('../assets/icons/refresh.svg')
                }else{
                    return require('../assets/icons/add.svg')
                }
            }
        },
        action(){
            if(!this.showSecondary){
                return
            }else{
                if(!this.newEntry.state){
                    if(this.checkInputs()){
                        console.log("update object")
                    }   
                }else{
                    if(this.checkInputs()){
                        this.$emit('createNewObject')
                        console.log("new object")
                    }
                }
            }
              
        },
        
    },
    inject: ['newEntry']
    
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