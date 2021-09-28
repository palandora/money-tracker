<template>
    <div class="entry">
        <div class="bounds">
            <div class="contents">
                <div class="thumb">
                    <img :src="setImage(content.category)" :alt="'category image '+content.category">
                </div>
                <div class="desc">
                    <span>{{content.title}}</span>
                    <span>{{content.category}}</span>
                </div>
            </div>
            <div class="details">
                <span>{{content.amount}}€</span>
                <img src="../assets/icons/chevron_right.svg" alt="view details" >
            </div>
            
        </div>
        <hr>
    </div>
</template>

<script>
export default {
    name: 'entry',
    data(){
        return{

        }
    },
    props: {
        content: Object,
        toogleEditPanel: Function
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
    .entry{
        display: flex;
        flex-direction: column;
        cursor:pointer;
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
        background: var(--ui-divider);
        margin-left: 16px;
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
    .details{
        display:flex;
        align-items: center;
    }
    .details span{
        margin-right: 4px;
    }
    

</style>