<template>
  <div class="transfer">
    <transfer-list title = "源文件" :data="resource"></transfer-list>
    <div class="transfer-operation">
      <p><input type="button" value="<"  @click="taTransformRe" /></p>
      <p><input type="button" value=">"  @click="reTransformTa"/></p>
    </div>
    <transfer-list title="目标文件" :data="target"></transfer-list>
  </div>
</template>

<script>
  export default {
    data(){
      return {
        resource:[
          {
            name:'admin',
            isChecked:false
          },
          {
            name:'student',
            isChecked:false
          },
          {
            name:'teacher',
            isChecked:false
          },
          {
            name:'other',
            isChecked:false
          }
        ],
        target:[
          {
            name:'visitor',
            isChecked:false
          }
        ]
      }
    },
    methods:{
        transform(obj1,obj2){
          /*let checkedItem = obj1.filter(item => item.isChecked).map((item) => {
            return {
              ...item,
              isChecked: false
            }
          })
          obj2.push(...checkedItem)

          return obj1.filter(item => !item.isChecked)*/

          let checkItem = obj1.filter(item => item.isChecked).map((item) => {
            return {
              ...item,
              isChecked:false
            }
          })
          obj2.push(...checkItem);
          return obj1.filter(item => !item.isChecked);
        },

        reTransformTa(){
          this.resource = this.transform(this.resource,this.target);
        },
        taTransformRe(){
          this.target = this.transform(this.target,this.resource);
        }
    },
    components:{
      'transfer-list':{
        props:['title','data'],
        template:`
            <div class="transfer-list">
              <div class="transfer-header">
                <input type="checkbox" name="">
                <span class="transfer-header-title">目标列表</span>
                <span class="transfer-header-count">6</span>
              </div>
              <div class="transfer-list-body">
                <ul class="transfer-list-content">
                  <li class="transfer-list-content-item" v-for="item in data">
                    <input type="checkbox" name="" v-model="item.isChecked">
                    <span>{{item.name}}</span>
                  </li>
                </ul>
              </div>
            </div>`
      }
    }
  }
</script>

<style>
  .transfer {
    line-height: 1.5;
    position: relative;
  }
  .transfer-list {
    display: inline-block;
    width: 280px;
    height: 210px;
    font-size: 12px;
    vertical-align: middle;
    position: relative;
    padding-top: 35px;
  }
  .transfer-header {
    box-sizing: border-box;
    padding: 8px 16px;
    background: #f9fafc;
    color: #495060;
    border: 1px solid #dddee1;
    border-bottom: 1px solid #e9eaec;
    border-radius: 6px 6px 0 0;
    overflow: hidden;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
  }
  .transfer-header-title {
    padding-left: 4px;
  }
  .transfer-header-count {
    float: right;
    margin-right: 4px;
  }
  .transfer-list-body {
    height: 100%;
    border: 1px solid #dddee1;
    border-top: none;
    border-radius: 0 0 6px 6px;
    position: relative;
    overflow: hidden;
  }
  .transfer-list-content {
    height: 100%;
    padding: 4px 0;
    overflow: auto;
  }
  .transfer-list-content-item {
    margin: 0;
    line-height: normal;
    padding: 7px 16px;
    clear: both;
    color: #495060;
    white-space: nowrap;
    list-style: none;
    cursor: pointer;
    transition: background .2s ease-in-out;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .transfer-operation {
    display: inline-block;
    overflow: hidden;
    margin: 0 16px;
    vertical-align: middle;
  }
</style>
