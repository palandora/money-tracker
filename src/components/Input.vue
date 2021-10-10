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
                        <span>{{setHeadline()}}</span>
                        <span>{{getCurrentDate()}}</span>  
                    </div>
                </div>
            </div>
            <hr>
        </div>
        <div class="wrapper-inputs">
            <div class="input-field">
                <input v-model="title" type="text" id="title" placeholder="Title" autocomplete="off">
                <hr>
            </div>
            <div class="input-field">
                <div class="toggle_dropdown" 
                :class="[isToggled ? 'show' : '']"
                @click="toggleDropdown"
                >
                    <img src="../assets/icons/caret_down.svg" alt="toggle">
                </div>
                
                <input v-model="category" type="text" id="category" placeholder="Category" readonly>
                <hr>
                <div class="dropdown"
                :class="[isToggled ? 'show' : '']"
                >
                    <div class="dropdown-item"
                    v-for="(category,index) in filteredCateogries" 
                    :key="index"
                    @click="selectCategory(category[0])"
                    >
                        {{category[0]}}
                    </div>
                </div>
            </div>
            <div class="input-field">
                <input v-model="amount" type="number" id="amount" placeholder="Amount">
                <hr>
            </div>
        </div>
        
        <CTA 
        :checkInputs="checkInputs"
        v-on:createNewObject="addEntry({'title': title, 'category' : category, 'amount' : amount})"
        />
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
            amount: null,
            isToggled: false
        }
    },
    props: {
        hideInput: Function,
        showInput:Boolean,
        currentEntry: Object,
        categories:Object,
        addEntry: Function
    },
    methods:{
        selectCategory(selectedCat){
            this.category = selectedCat
            this.toggleDropdown()
        },
        toggleDropdown(){
            this.isToggled ? this.isToggled = false : 
            this.isToggled = true
        },
        getCurrentDate(){
            const today = new Date()
            const currentDate = `${today.getDate()}-${today.getMonth()+1}-${today.getFullYear()}`
            return currentDate
        },
        setHeadline(){
            if(this.newEntry.state){
                return "Create new Entry"
            }else{
                return "Update Entry"
            }
        },
        getCategoriesLength(obj){
            let keys = Object.keys(obj)
            let length = keys.length
            return length
        },
        checkInputs(){
            if(this.title.length > 0 && 
            this.category.length > 0 && 
            this.amount != null &&
            this.amount.toString().length > 0){
                return true
            }else{
                return false
            }
        }
    },
    computed:{
        filteredCateogries(){
            const asArray = Object.entries(this.categories)
            let counter = 0
            let filtered = []

            asArray.forEach(item => {
                counter++
                if(counter < asArray.length)
                filtered.push(item)
            });
            return filtered
        }
    },
    watch:{
        currentEntry(obj){
            if(obj == null){
                this.title = ""
                this.category = ""
                this.amount = null
            }else{
                this.title = obj.title
                this.category = obj.category
                this.amount = obj.amount
            }
        }
    },
    inject: ['newEntry'],
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
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }
    .input-field{
        position: relative;
    }
    .input-field hr{
        margin-left:16px;
    }
    /* dropdown */
    .toggle_dropdown{
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        right: 16px;
        display: flex;
        justify-content: center;
        align-items: center;
        cursor: pointer;
    }
    .toggle_dropdown img{
        transform-origin: center;
        transform: rotate(0deg);
    }
    .dropdown{
        position: absolute;
        z-index: 1;
        left: 16px;
        right: 16px;
        display:none;
        flex-direction: column;
        padding: 6px 0;
        background: white;
        border-radius: 6px;
        box-shadow: 0 0 0 1.5px rgba(0,0,0,.04),
        0 4px 6px rgba(0,0,0,.08);
    }
    /*toggled states*/ 
    .dropdown.show{
        display:flex;
    }
    .toggle_dropdown.show img{
        transform: rotate(180deg);
    }

    .dropdown-item{
        cursor: pointer;
        padding: 8px 16px;
    }
    .dropdown-item:hover{
        background: #f4f4f4;
    }


</style>