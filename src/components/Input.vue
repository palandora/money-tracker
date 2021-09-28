<template>
    <div class="input" :class="[showInput?'show':'']">
        <div class="header">
            <div class="bounds">
                <img src="../assets/icons/chevron_left.svg" alt="move back" 
                @click="hideInput()"
                >
                <div class="contents">
                    <div class="thumb">
                        <img src="../assets/categories/overview.png" alt="">
                    </div>
                    <div class="desc">
                        <span>Create new Entry</span>
                        <span>12.02.1995</span>  
                    </div>
                </div>
            </div>
            <hr>
        </div>
        <div class="wrapper-inputs">
            <div class="input-field">
                <input v-model="title" type="text" id="title" placeholder="Title">
                <hr>
            </div>
            <div class="input-field">
                <input v-model="category" type="text" id="category" placeholder="Category">
                <hr>
                <div class="dropdown">
                    <div class="dropdown-item"
                    v-for="(category,name) in categories" 
                    v-bind:key="category"
                    >
                        {{name}}
                    </div>
                </div>
            </div>
            <div class="input-field">
                <input v-model="amount" type="text" id="amount" placeholder="Amount">
                <hr>
            </div>
        </div>
        
        <CTA :currentEntry="currentEntry"/>
    </div>
</template>

<script>
import CTA from './CTA.vue'

export default {
    name: 'inputs',
    data(){
        return {
            title: '',
            category: '',
            amount: null
        }
    },
    props: {
        hideInput: Function,
        showInput:Boolean,
        currentEntry: Object,
        categories:Object
    },
    methods:{
        
    },
    watch:{
        currentEntry(obj){
            if(obj == {}){
                return
            }else{
                this.title = obj.title
                this.category = obj.category
                this.amount = obj.amount
            }
        }
    },
    components:{
        CTA
    }

}
</script>

<style scoped>
    .input{
        position: absolute;
        z-index: 2;
        width: 50%;
        height: 100vh;
        left:100%;
        display:flex;
        flex-direction: column;
        background: white;
        transition: left .5s ease-in-out;
        box-shadow: -4px 0 24px rgba(0,0,0,.08);
    }
    .input.show{
        left:50%;
    }
    .header{
        display: flex;
        flex-direction: column;
    }
    .bounds{
        display: flex;
        align-items: center;
        padding: 16px 16px 16px 12px;
    }
    .bounds > img{
        cursor: pointer;
    }
    hr{
        border: 0;
        height: 1px;
        background: var(--ui-divider);
    }
    .contents{
        margin-left: 12px;
        gap: 16px;
        display: flex;
        align-items: center;
    }
    .thumb{
        width: 40px;
        height: 40px;
        display:flex;
        justify-content: center;
        align-items: center;
        background: rgba(0,0,0,.06);
        border-radius:12px;
    }
    .thumb img{
        width: 24px;
    }
    .desc{
        display: flex;
        flex-direction: column;
    }
    .desc span:last-child{
        color: var(--txt-sublines);
    }
    /* inputs */
    .wrapper-inputs{
        flex-grow:1;
    }
    input{
        font-family: 'Open Sans', sans-serif;
        font-size:16px;
        font-weight: 600;
        line-height: 19px;
        border:0;
        padding: 18px 16px;
    }
    input:focus{
       outline: 0;
    }
    .input-field{
        position: relative;
    }
    .input-field hr{
        margin-left:16px;
    }
    /* dropdown */
    .dropdown{
        position: absolute;
        z-index: 1;
        left: 16px;
        right: 16px;
        display:flex;
        flex-direction: column;
        padding: 6px 0;
        background: white;
        border-radius: 6px;
        box-shadow: 0 0 0 1.5px rgba(0,0,0,.04),
        0 4px 6px rgba(0,0,0,.08);
    }
    .dropdown.hide{
        display:none;
    }
    .dropdown-item{
        cursor: pointer;
        padding: 8px 16px;
    }
    .dropdown-item:hover{
        background: #f4f4f4;
    }


</style>