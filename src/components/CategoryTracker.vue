<template>
    <div class="category-tracker">
        <div class="thumb">
            <img :src="setImage" :alt="'category image '+currentCategoryName">
        </div>
        <div class="title">
            <span>{{currentCategoryName}}</span>
            <span>{{calcPercentage}}%</span>
        </div>
        <hr>
    </div>
</template>

<script>
export default {
    data(){
        return{

        }
    },
    props: {
        currentCategoryName: String,
        currentCount: Number,
        overallCount: Number
    },
    methods:{
    },
    computed:{
        setImage(){
            let strg = this.currentCategoryName.toLowerCase()
            return require(`../assets/categories/${strg}.png`)
        },
        calcPercentage(){
            let percentage = (this.currentCount / this.overallCount)*100
            let rounded = percentage.toFixed(1);
            return rounded
        }
    }

}
</script>

<style scoped>
    .category-tracker{
        display: flex;
        padding: 16px 0 16px 16px;
    }
    .thumb{
        width: 40px;
        height: 40px;
        display:flex;
        justify-content: center;
        align-items: center;
        background: rgba(255,255,255,.06);
        border-radius:12px;
        margin-right: 16px;
    }
    .thumb img{
        width: 24px;
    }
    .title{
        color: white;
        display: flex;
        flex-direction: column;
    }
    .title span:last-child{
        color: var(--txt-sublines);
    }
    hr{
        border: 0;
        height: 1px;
        background: #444;
        margin-left: 16px;
    }


</style>