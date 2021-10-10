<template>
    <div class="wrapper-dropdown">
        <div class="dropdown">
            <div class="bounds">
                <div class="contents">
                    <div class="thumb">
                        <img :src="setImage(currentCategory)" :alt="'category image '+currentCategory">
                    </div>
                    <div class="desc">
                        <span>{{currentCategory}}</span>
                        <span>{{categories[currentCategory].entries.length}}</span>
                    </div>
                </div>
                <img src="../assets/icons/chevron_down.svg" alt="view details" 
                :class="[hidden?'toggled':'']"
                @click="toggleDropdown"
                >
            </div>
            <hr>
        </div>
        <div class="wrapper-dropdown-items" :class="[hidden ? 'hide' : '']">
            <dropdown-item 
            
            v-for="(category,name) in categories" 
            v-bind:key="category"
            :category="category"
            :propName="name"
            @click="selectItem(name)"
            />   
        </div>
        <hr>
    </div>
    
</template>

<script>

import DropdownItem from './DropdownItem.vue'

export default {
    name: 'dropdown',
    data(){
        return{
            category: "Overview",
            items: 200,
            hidden: true
        }
    },
    props: {
        currentCategory:String,
        categories:Object,
        setCategory: Function
    },
    methods:{
        setImage(category){
            let strg = category.toLowerCase()
            return require(`../assets/categories/${strg}.png`)
        },
        toggleDropdown(){
            !this.hidden ? this.hidden = true : 
            this.hidden = false
        },
        selectItem(propName){
            this.setCategory(propName)
            this.toggleDropdown()
        }
    },
    components:{
        DropdownItem
    }
}
</script>

<style scoped>
    .wrapper-dropdown{
        position: fixed;
        z-index: 10;
        width: 50%;
        background: var(--ui-bg-categories);
    }
    .dropdown{
        display: flex;
        flex-direction: column;
    }
    .bounds{
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 16px 12px 16px 16px;
    }
    hr{
        border: 0;
        height: 1px;
        background: #444;
    }
    .contents{
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
        background: rgba(255,255,255,.06);
        border-radius:12px;
    }
    .thumb img{
        width: 24px;
    }
    .desc{
        display: flex;
        flex-direction: column;
    }
    span{
        color:white;
    }
    .desc span:last-child{
        color: var(--txt-sublines);
    }
    img[alt="view details"]{
        cursor: pointer;
        transform-origin: center;
        transition: transform .25s ease-in-out;
    }
    img[alt="view details"].toggled{
        transform: rotate(180deg)
    }
    /* dropdown items */
    .wrapper-dropdown-items{
        max-height: 288px;
        overflow: scroll;
    }
    .wrapper-dropdown-items.hide{
        display: none;
    }
</style>