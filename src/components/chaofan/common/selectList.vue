<template>
 <div class="nkl">  
    <div class="c_top_nav">
        <div v-for="(item,index) in options" @click="chooseNav(index,item)" :key="index" :class="['c_nav_item',{'c_nav_item_active': params.order ==item.value}]">
            <img v-if="index==0" class="img1" src="../../../assets/newicon/new.png" alt="">
            <img v-if="index==0" class="img2" src="../../../assets/newicon/new_a.png" alt="">

            <img v-if="index==1" class="img1" src="../../../assets/newicon/hot.png" alt="">
            <img v-if="index==1" class="img2" src="../../../assets/newicon/hot_a.png" alt="">

            <img v-if="index==2" class="img1" src="../../../assets/newicon/comment.png" alt="">
            <img v-if="index==2" class="img2" src="../../../assets/newicon/comment_a.png" alt="">

            <img v-if="index==3" class="img1" src="../../../assets/newicon/up.png" alt="">
            <img v-if="index==3" class="img2" src="../../../assets/newicon/up_a.png" alt="">
            {{item.label}}
        </div>
        <el-select v-if="!ISPHONE&&params.order ==='ups'" v-model="params.range" placeholder="请选择"
                    @change="changes" style="padding: 0px 20px; ">
            <el-option
                v-for="item in ranges"
                :key="item.value"
                :label="item.label"
                :value="item.value">
            </el-option>
        </el-select>
    </div>
    <div v-if="ISPHONE&&params.order ==='ups'" class="phones">
      <el-select v-model="params.range" placeholder="请选择"
                  @change="changes" style="padding: 0px">
          <el-option
              v-for="item in ranges"
              :key="item.value"
              :label="item.label"
              :value="item.value">
          </el-option>
      </el-select>
    </div>
        
        
 </div>
</template>

<script>
 export default {
   name: '',
   data(){
     return {
         options: [
          {
            label: '最新',
            value: 'new',
            choose: true,
          },
          {
            label: '最热',
            value: 'hot',
            choose: false,
          },
          {
            label: '热评',
            value: 'comment',
            choose: false,
          },
          {
            label: '最赞',
            value: 'ups',
            choose: false,
          },
        ],
        ranges: [
          {
            label: '现在',
            value: '1hour'
          },
          {
            label: '一天',
            value: '1day'
          },
          {
            label: '一周',
            value: '1week'
          },
          {
            label: '一个月',
            value: '1month'
          },
          {
            label: '一年',
            value: '1year'
          },
          {
            label: '全部',
            value: 'all'
          },
        ],
     }
   },
   
   props: {
       params:{
           type: Object,
           default(){
               return {}
           }
       }
   },
   components: {

   },
   created() {
   },
   mounted() {
    
   },
   methods: {
    changes() {
        localStorage.setItem('chao.fun.timeline.order', this.params.order);
        localStorage.setItem('chao.fun.timeline.range', this.params.range);
        delete this.params.marker;
        delete this.params.key;
        this.$emit('updateList',this.params)
    },
    chooseNav(index,item){
        this.options.forEach(i=>{
          i.choose = false;
        })
        item.choose = true;
        this.options.splice(index,1,item);
        localStorage.setItem('chao.fun.timeline.order', item.value);
        localStorage.setItem('chao.fun.timeline.range', this.params.range);
        delete this.params.marker;
        delete this.params.key;
        this.params.order = item.value;
        this.$emit('updateList',this.params)
        // this.lists = []
        // this.getLists();
    },
   }
 }
</script>

<style type='text/scss' lang='scss' scoped>

.phones{
  height: 34px;
  text-align: left;
  // margin-bottom: ;
}
</style>
