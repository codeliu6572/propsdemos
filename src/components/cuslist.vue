<template>
  <list class="list">
    <cell class="cell" v-for="v in listData">
      <div class="panel">
        <div v-if="pageName">
          <!-- {{pageName[0]}} -->
          <!-- {{cus.title}} -->
          {{hpageName}}
        </div>
        <text>
           <!-- {{page[0]}} -->
           <!-- page:{{cus.pages}}-第{{v}}个 -->
           page:{{hpage}}-第{{v}}个
        </text>
      </div>
    </cell>
  </list>
</template>

<script>

export default {
  props: {
      pageName: {
        type: Array
      },
      page:{
        type: Array
      },
      cus: {
        title: '',
        pages: 0
      },
      hpageName: {
        type: String
      },
      hpage:{
        type: Number
      },

  },
  data () {
    return {
      listData: ['0','1', '2', '3', '4', '5', '6', '7', '8', '9'],
      // pageName: pageNames[page]
    }
  }
}
</script>


<style scoped>
  .list{
      width: 750px;
      height: 1086px;
  }
  .panel {
    width: 750px;
    height: 300px;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-width: 1px;
    border-style: solid;
    border-color: rgb(162, 217, 192);
    background-color: rgba(162, 217, 192, 0.2);
  }
</style>
