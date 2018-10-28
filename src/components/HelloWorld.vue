<template>
  <div class="wrap">
  	<mt-navbar v-model="selected">
  		<mt-tab-item id="1">选项一</mt-tab-item>
  		<mt-tab-item id="2">选项二</mt-tab-item>
  		<mt-tab-item id="3">选项三</mt-tab-item>
  	</mt-navbar>
  	<div class="main-body" style="height: 500px;overflow: scroll;">
  	<mt-loadmore :top-method="loadTop"
　　　　:bottom-method="loadBottom"
　　　　:bottom-all-loaded="allLoaded"
　　　　ref="loadmore">
  	<mt-tab-container v-model="selected">
  		<mt-tab-container-item id="1">
  			<mt-cell v-for="item in list" :key = "item.id" :title="'内容'+item"/>
  		</mt-tab-container-item>
  		<mt-tab-container-item id="2">
  			<mt-cell v-for="item in list02" :key = "item.id" :title="'内容'+item"/>
  		</mt-tab-container-item>
  		<mt-tab-container-item id="3">
  			<mt-cell v-for="item in list03" :key = "item.id" :title="'内容'+item"/>
  		</mt-tab-container-item>
  	</mt-tab-container>
  	</mt-loadmore>
  	</div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      list01:[1,2,3,4,5],
      list02:[1,2,3,4,5,6,7,8,9,10],
      list03:[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15],
      selected:'1',
      list:[],
      allLoaded:false,
      isAutoFill: false,
      wrapperHeight: 0,
    }
  },
  methods:{
  	// 下拉刷新加载
    loadFrist() {
    	this.list =[];
    	for(let i in this.list03){
    		this.list.push(this.list03[i]);
    	}
    	this.allLoaded = false; // 可以进行上拉
      this.$refs.loadmore.onTopLoaded();
      
    },
    // 加载更多
    loadMore() {
      for(let i in this.list01){
    		this.list.push(this.list01[i]);
    	}
      this.allLoaded = true;
      this.$refs.loadmore.onBottomLoaded();
    },
　　loadTop(){
			this.list =[];
    	for(let i in this.list03){
    		this.list.push(this.list03[i]);
    	}
    	this.allLoaded = false; // 可以进行上拉
      this.$refs.loadmore.onTopLoaded();
		},
　　loadBottom(){
			for(let i in this.list01){
    		this.list.push(this.list01[i]);
    	}
      this.allLoaded = false;
      this.$refs.loadmore.onBottomLoaded();
		}

  },
　created(){
		
　 },  
  mounted(){
  	this.loadFrist();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
@import url("../../static/css/index.less");
</style>
