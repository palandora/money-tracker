<template>
  <Input :showInput="showInput" 
  :hideInput="hideInput"
  :currentEntry="currentEntry"
  :categories="entries"
  />
  <div class="container">
    <div class="categories">
      <dropdown 
      :categories="entries" 
      :currentCategory="currentCategory"
      :setCategory="setCurrentCategory"
      />
    </div>
    <div class="entries">
      <div class="wrapper-entries">
        <entry 
        v-for="entry in entries[currentCategory].entries" 
        :key="entry" 
        :content="entry"
        @click="showEntryDetails(entry)"
        />
      </div>
      
      <CTA 
      :showSecondary="false"
      @click="showEntryDetails()"
      />
    </div>
  </div>
  
</template>

<script>
import Entry from './components/Entry.vue'
import Dropdown from './components/Dropdown.vue'
import Input from './components/Input.vue'
import CTA from './components/CTA.vue'

export default {
  name: 'App',
  data(){
    return {
      currentCategory: "Overview",
      showInput: true,
      currentEntry: null,
      entries: {
        Vacation : {
          entries: [],total: 0
        },
        Shopping : {
          entries: [],total: 0
        },
        Food : {
          entries: [],total: 0
        },
        Household : {
          entries: [],total: 0
        },
        Work : {
          entries: [
            {
              title: "Shopping with pamela",
              category: "Work",
              amount: 200
            },
          ],total: 0
        },
        Other : {
          entries: [],total: 0
        },
        Income : {
          entries: [],total: 0
        },
        Overview : {
          entries: [
            {
              title: "Shopping with pamela",
              category: "Overview",
              amount: 200
            }
          ],total: 0
        }
      }
    }
  },
  methods:{
    addEntry(obj){
      try{
        let objCat = obj.category
        let category = objCat.toLowerCase()
        // nee to define in entry mask if amout is added or substracted
        this.entries[category].total += obj.amount
        this.entries[category].entries.push(obj)

        this.entries.overview.entries.push(obj)
        this.entries.overview.total += obj.amount
      }catch(e){
        console.log(e)
      }
    },
    setCurrentCategory(newCategory){
      this.currentCategory = newCategory
    },
    hideInput(){
      this.showInput = false
    },
    showEntryDetails(obj){
      if(obj == undefined){
        this.currentEntry = {}
        this.showInput = true
      }else{
        this.currentEntry = obj
        this.showInput = true
      }
      
    }
  },
  components: {
    Entry,
    Dropdown,
    Input,
    CTA
  }
  
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@600;700;800&display=swap');
  *{
    margin:0;
    padding: 0;
    box-sizing: border-box;
  }
  #app {
    overflow: hidden;
    font-family: 'Open Sans', sans-serif;
    font-weight: 600;
    line-height: 19px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    position: relative;
    /* colors */
    --ui-bg-categories: #2b2b2b;
    --ui-divider:#dedede;
    --ui-light-grey: #ccc;
    --ui-accent-green:#04c600;
    --ui-accent-delete:#ff2929;
    --txt-headlines: #000;
    --txt-sublines:#8d8d8d;
  }
  
  .container{
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: stretch;
  }
  .categories{
    background: var(--ui-bg-categories);
    display: flex;
    flex-direction: column;
    width: 50%;
  }
  .entries{
    display: flex;
    flex-direction: column;
    width: 50%;
  }
  .wrapper-entries{
    display:flex;
    flex-direction: column;
    flex-grow:1;
  }
</style>
