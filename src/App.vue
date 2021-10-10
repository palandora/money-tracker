<template>
  <Input :showInput="showInput" 
  :hideInput="hideInput"
  :currentEntry="currentEntry"
  :categories="entries"
  :addEntry="addEntry"
  />
  <div class="container">
    <!-- left col -->
    <div class="categories">
      <dropdown 
      :categories="entries" 
      :currentCategory="currentCategory"
      :setCategory="setCurrentCategory"
      />
      <div class="expense-counter">
        <span>Total</span>
        <h1>{{entries[currentCategory].total}}</h1>
      </div>
      <div class="stats">
        <hr>
        <div class="bounds">
          <category-tracker
          v-for="(entry,name) in entries" :key="name" 
          :currentCategoryName="name"
          :currentCount="entry.total"
          :overallCount="entries.Overview.total"
          />
        </div>
      </div>
    </div>
    <!-- right col -->
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
import CategoryTracker from './components/CategoryTracker.vue'

export default {
  name: 'App',
  data(){
    return {
      currentCategory: "Overview",
      showInput: false,
      currentEntry: null,
      isNewEntry: {state: false},
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
          ],total: 20
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
              category: "Shopping",
              amount: 200
            }
          ],total: 200
        }
      }
    }
  },
  methods:{
    addEntry(obj){
      try{
        console.log(obj)
        let objCat = obj.category
        this.entries[objCat].total += obj.amount
        this.entries[objCat].entries.push(obj)
        this.entries.Overview.entries.push(obj)
        this.entries.Overview.total += obj.amount
        this.hideInput()
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
        console.log("create new ")
        this.currentEntry = null
        this.showInput = true
        this.isNewEntry.state = true
      }else{
        console.log("open existing")
        this.currentEntry = obj
        this.isNewEntry.state = false
        this.showInput = true
      }
      
    }
  },
  provide(){
    return {
      newEntry : this.isNewEntry
    }
  },
  components: {
    Entry,
    Dropdown,
    Input,
    CTA,
    CategoryTracker
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
    /*font-size*/ 
    --h1: 64px;
    /* colors */
    --ui-bg-categories: #2b2b2b;
    --ui-divider:#dedede;
    --ui-light-grey: #ccc;
    --ui-accent-green:#04c600;
    --ui-accent-delete:#ff2929;
    --txt-headlines: #000;
    --txt-headlines-light: #fff;
    --txt-sublines:#8d8d8d;
  }
  h1{
    font-size: var(--h1);
    font-weight: 800;
    line-height: 74px;
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
    justify-content: flex-start;
    flex-grow: 1;
    width: 50%;
  }
  .expense-counter{
    margin-top: 72px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    flex-grow:1;
  }
  .expense-counter > *{
    color: var(--txt-headlines-light);
  }
  .expense-counter span {
    opacity: .5;
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
  .bounds{
    display: flex;
    overflow-y: hidden;
  }
  hr{
    border: 0;
    height: 1px;
    background: #444;
  }
</style>
