<script>
  export default{
    data(){
      return{
        text:'hello',
        openBox: false,
        fruits:[
          {
            id: 1,
            name: 'a1 科 / 80 屬',
            checked:false,
          },
          {
            id: 2,
            name: 'a2 科 / 111 屬',
            checked:false,
          },  
        ],
        selectedItems:[],
        isActive:true,

      }
    },
    computed: {
      computedClasses(){
        return {
          'visible':this.openBox, //打開時 加上visible classname
        }
      },

    },
    methods:{
      //取得點擊的值，加入陣列，打api
      // 顯示 關閉
      clickList(event){
        event.stopPropagation(); // 阻止bubble冒泡
        //查看點擊的值
        console.log(event.target.value)
        console.log('clickeddddddd')
        //開關選單
        this.toggleOpen();
       
      },
      toggleOpen(){
        this.openBox = !this.openBox;
        //點擊其他空白處收合選單 
        if (this.openBox) {
          document.addEventListener('click', this.closeDropdownOnOutsideClick);
        } else {
          document.removeEventListener('click', this.closeDropdownOnOutsideClick);
        }
      },
      closeDropdownOnOutsideClick(event){
        //檢查根元素$el內是否包刮目標事件
        console.log(this.$el,'$el', event.target,'target')
        if (this.$el.contains(event.target)) {
          return;
        } else {
          this.openBox = false;
          //取消監聽
          document.removeEventListener('click', this.closeDropdownOnOutsideClick);
        }
      },
      toggleSelection(f) {
        console.log(f)
      if(this.selectedItems.includes(f)){
        //已在陣列者，從陣列中移除
        const itemIndex = this.selectedItems.indexOf(f);
        this.selectedItems.splice(itemIndex,1);
      }else{
        // 檢查陣列中沒有，就加入陣列
        this.selectedItems.push(f);
      }
    }
    },

  }
</script>

<template>
  <div>
    <label class="form-label select-label">Example label</label>
    <div id="list1" 
      class="dropdown-check-list" 
      :class="computedClasses">
      
      <span class="anchor"  @click="clickList" >Select Fruits</span>

      <div v-if="openBox">
        <ul class="items">
          <li v-for="f in fruits">
            <input type="checkbox" 
            v-model="f.checked"           
             @click="toggleSelection(f)" :id="f.id"/>
            <label :for="f.id">{{f.name}}</label>
          </li>
        </ul>  

      </div>

     

    </div>

    目前已選擇
        <div v-for="item in selectedItems">
        {{ item.name }}
        </div>
   
    
  </div>
</template>

<style lang="sass">

.dropdown-check-list
  display: inline-block
  &.visible
    .anchor
      color: #0094ff
    .items
      display: block
  .anchor
    position: relative
    cursor: pointer
    display: inline-block
    padding: 5px 50px 5px 10px
    border: 1px solid #ccc
    &:after
      position: absolute
      content: ""
      border-left: 2px solid black
      border-top: 2px solid black
      padding: 5px
      right: 10px
      top: 20%
      -moz-transform: rotate(-135deg)
      -ms-transform: rotate(-135deg)
      -o-transform: rotate(-135deg)
      -webkit-transform: rotate(-135deg)
      transform: rotate(-135deg)
    &:active:after
      right: 8px
      top: 21%

  ul.items
    padding: 10px
    display: none
    margin: 0
    border: 1px solid #ccc
    border-top: none
    li
      list-style: none
      padding: 10px 0
      input[type="checkbox"]
        width: 15px
        height: 15px
        margin-right: 10px
</style>

