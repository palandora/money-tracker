<template>
    <div class="dropdown-item">
        <div class="bounds">
            <div class="contents">
                <div class="thumb">
                    <img :src="setImage(propName)" :alt="'category image '+category">
                </div>
                <div class="desc">
                    <span>{{propName}}</span>
                    <span>{{category.entries.length}}</span>
                </div>
            </div>
        </div>
        <hr>
    </div>
</template>

<script>
export default {
    name: 'dropdown-item',
    data(){
        return {

        }
    },
    props: {
        category:Object,
        propName:String
    },
    methods:{
        setImage(category){
            let strg = category.toLowerCase()
            return require(`../assets/categories/${strg}.png`)
        }
    }
}
</script>

<style scoped>
    .dropdown-item{
        display: flex;
        flex-direction: column;
        cursor: pointer;
    }
    .dropdown-item:hover{
        background:rgba(255,255,255,.06)
    }
    .bounds{
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 16px;
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
    

</style>