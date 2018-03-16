<template>
    <div>
        <div>
            <div class="header">
                <div class="nav">
                    <text class="navTitle">header</text>
                </div>
            </div>
        </div>
        <wxc-tab-page ref="wxc-tab-page"
                :tab-titles="tabTitles"
                :tab-styles="tabStyles"
                title-type="icon"
                :needSlider="needSlider"
                :is-tab-view="isTabView"
                :tab-page-height="tabPageHeight"
                @wxcTabPageCurrentTabSelected="wxcTabPageCurrentTabSelected">
          <cuslist v-for="(v,index) in tabList" :key="v"
            :pageName="pageName"
            :page="page"
            :cus="cus"
            :hpageName="hpageName"
            :hpage="hpage">
              
          </cuslist>
        </wxc-tab-page>
    </div>
  
</template>

<style scoped>
  .header{
      top: 0;
      left: 0;
      right: 0;
      height: 128px;
      background-color: #44B5F0;
  }
  .nav{
      left: 150px;
      right: 150px;
      top: 40px;
      height: 88px;
      justify-content: center;
      align-items: center;
      position: absolute;
  }
  .navTitle{
      font-size: 34px;
      text-align: center;
      color: white;
  }
</style>
<script>
  const dom = weex.requireModule('dom');
  import { WxcTabPage, WxcPanItem, Utils } from 'weex-ui';
  import cuslist from './components/cuslist.vue';
  var navigator = weex.requireModule('navigator')
  // https://github.com/alibaba/weex-ui/blob/master/example/tab-page/config.js
  import homeBigConfig from './components/homeBigConfig'
  var kpageName;
  export default {
    components: { WxcTabPage, WxcPanItem, cuslist },
    data: () => ({
      tabTitles: homeBigConfig.tabTitles,
      tabStyles: homeBigConfig.tabStyles,
      tabList: [],
      page: [],
      pageName: [],
      hpage: 0,
      hpageName: '',
      cus: {},
      kpageName: '',
      needSlider: false,
      isTabView: true,
      demoList: [1, 2, 3, 4, 5, 6, 7, 8, 9],
      tabPageHeight: 1206
    }),
    created () {
      this.tabPageHeight = Utils.env.getPageHeight();
      this.tabList = [...Array(this.tabTitles.length).keys()].map(i => []);
      Vue.set(this.tabList, 0, this.demoList);

      kpageName = this.tabTitles[0]['title'];
      Vue.set(this.pageName, 0, kpageName);
      Vue.set(this.page, 0, 0)
      Vue.set(this.cus, 'title', kpageName);
      Vue.set(this.cus, 'pages', 0);
      this.hpage=0;
      this.hpageName='热门跟团';

    },
    methods: {
      wxcTabPageCurrentTabSelected (e) {
        const self = this;
        const index = e.page;
        /* Unloaded tab analog data request */
        // if (!Utils.isNonEmptyArray(self.tabList[index])) {
        //   setTimeout(() => {
        //     Vue.set(self.tabList, index, self.demoList);
        //     // Vue.set(self.page, 'page', index);
        //     // Vue.set(self.pageNames, 'pageNames', self.tabTitles);
        //     self.page = index;
        //   }, 100);
        // }
        setTimeout(() => {
            Vue.set(self.tabList, index, self.demoList);
            Vue.set(self.page, 0, index)
            kpageName = self.tabTitles[index]['title'];
            Vue.set(self.pageName, 0, kpageName);
            Vue.set(this.cus, 'title', kpageName);
            Vue.set(this.cus, 'pages', index);
            self.hpage=index;
            self.hpageName=kpageName;
        }, 100);
      }
    }
  };
</script>