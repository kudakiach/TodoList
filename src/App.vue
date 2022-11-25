<script>
export default {

  data: () => {
    return {
      entry: '',
      todoList:[]
    }
  },
  methods: {
    addItem() {
      if(this.entry !== '') {
        let date = new Date;
        let newItem =  {
          id:date.getTime(),
          title:this.entry,
          complete:false
        }

        this.todoList.push(newItem);
      }

      this.entry = '';
    },
    countItems() {
    count = 0
      for(var x = 0; x < todoList.length; x++) {
          if(todoList[x].complete == false){
            count += 1;
          }
      }
      return count;
    }
  }

}
</script>

<template>
  <header>
    <div class="header-content">
      <h1>TODO</h1>
      <div class="add-todo">
      <div class="add-item">
        <div class="add-icon">
        <div class="circle" @click="addItem"></div>
          
        </div>
        <form @submit.prevent="addItem">
          <input type="text" v-model="entry" placeholder="Create a new todo...">
        </form>
      </div>
   
    </div>

    </div>
    
  </header>
  <div class="todo-list">
  <div class="lists">
    <div class="items" v-for="(item, index) in todoList" :key="index">
      <div class="check-btn">
        <div class="circle"></div>
      </div>
      <div class="item-name">{{item.title}}</div>
      <div class="delete-btn"><i class="fa fa-close"></i></div>
    </div>
    <div class="actions">
        <div class="count"> 5 items </div>
        <div class="item-actions">
          <div class="act">
              <div class="all"><button class="clear-btn">All</button></div>
              <div class="active"> <button class="clear-btn">Active</button></div>
              <div class="completed"><button class="clear-btn">Complete</button></div>
          </div>
        </div>
        <div class="clear">Clear Complete</div>
    </div>
  </div>
   

<h3>Below this</h3>
    <div class="item-actions-sm">
     
          <div class="all"><button class="clear-btn">All</button></div>
          <div class="active"> <button class="clear-btn">Active</button></div>
          <div class="completed"><button class="clear-btn">Complete</button></div>
     
    </div>

  </div>
  
</template>

<style scoped>

.circle { 
  width:16px;
  height:16px;
  border-radius:50%;
  border:1px solid #444;
}

.circle:hover { 
  width:16px;
  height:16px;
  border-radius:50%;
  border:1px solid #444;
}

header {
  display:flex;
  line-height: 1.5;
  padding:15px;
  justify-content:center;
  align-items:center;
  color:white;
  background:url('assets/images/bg-desktop-dark.jpg');
  background-repeat:no-repeat;
  background-size:cover;
  min-height:250px
}
.header-content{
  padding:10px;
  width:60%;
}

.header-content h1{
  margin-bottom:25px;
  font-weight:700;
  font-family: Rubik sans;
  letter-spacing:3px;
}
.add-item {
  display:flex;
  gap:20px;
  border:1px solid #fffff;
  background-color:#ffffff;
  padding:5px;
  align-items:center;
}

form{
width:80%;
}

input[type=text] {
  padding:1px;
  font-weight:400;
  font-family:Rubik Sans;
 	font-size: 19px;
  width:100%;
  border:none;
  height:inherit;
  outline:none;
}

.todo-list{
  display:flex;
  justify-content:center;
  align-items:center;
  position:relative;
}
.lists{
  background-color:hsl(235, 21%, 11%);
  position: absolute;
  width:60%;
  clear:both;
}

.items{
  width:calc(100% - 20px);
  flex:100%;
  display:flex;
  gap:10px;
  align-items:center;
  justitfy-content:center;
  padding: 10px 10px;
  font-size:19px;
  color:white;
  border-bottom:1px solid hsl(235, 24%, 19%);
}

.items:hover .delete-btn{
display:block;
}

.border-b{
 background-color:#333;
 max-height:1px;
  min-width:0 0 100%;
  flex:0 0 100%;
}
.check-btn {
  min-width:0 0 10%;
  flex:0 0 10%;
}

.item-name{
  min-width:0 0 80%;
  flex:0 0 80%;
}
.delete-btn{ 
  min-width:0 0 10%;
  flex:0 0 10%;
  display:none;
}

.actions {
  display:flex;
  gap:20px;
  padding:10px;
}

.counts {
  display:flex;
  min-width:30%;
  flex:0 0 30%;
  text-align:center;
  justify-content:center;
}

.clear {
display:flex;
  min-width:30%;
  flex:0 0 30%;
  text-align:center;
  cursor:pointer;
}

.clear-btn{
  padding:5px;
  color:white;
  border:none;
  outline:none;
  background-color:transparent;
  cursor:pointer;
}
@media (min-width: 375px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

.item-actions {
  display:flex;
  justify-content:center;
  gaps:10px;
  min-width:40%;
  flex:0 0 40%;
}

  h3 { font-size:30px; color:red}
  item-actions-sm{
    display:none;   
  }
}
@media (max-width: 375px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

.header-content {
    width:100%;
}

  h3 { font-size:30px; display:none; color:red}
  item-actions-sm{
    display:flex;
    clear:both;
    z-index:1;  
  
  }
.item-actions {
  display:none;
}
.count {
font-size:16px;
font-family: Rubik sans;
width:50%;
 }

 .complete {
font-size:16px;
font-family: Rubik sans;
width:50%;
 }

}


</style>
