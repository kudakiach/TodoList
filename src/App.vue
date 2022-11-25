<script>
export default {

  data: () => {
    return {
      sun:{
        display:"block",
        color:"#ff0"
      },
      moon:{
        display:"none",
        color:"red"
      },

      bgColor:{
        backgroundColor:"hsl(235, 21%, 11%)",
        color:"hsl(234, 39%, 85%)"
      },
     
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

    lightTheme() {
      this.bgColor.backgroundColor = "hsl(0, 0%, 98%)"
      this.bgColor.color = "hsl(233, 14%, 35%)"
      this.sun.display = "none"
      this.moon.display = "block"
      
    },

    darkTheme() {
      this.bgColor.backgroundColor = "hsl(235, 21%, 11%)"
       this.bgColor.color = "hsl(236, 9%, 61%)"
      this.moon.display = "none"
      this.sun.display = "block"
     
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
    <div class="header-title">
      <div class="title">
        <h1>TODO</h1>
      </div>
      <div class="theme-icon">
       <i v-bind:style="moon" class=" fa fa-star fa-2x" @click="darkTheme"></i>
       <i v-bind:style="sun" class=" fa fa-star fa-2x" @click="lightTheme"></i>
      </div>
    </div>
      
      <div class="add-todo">
      <div v-bind:style="bgColor" class="add-item">
        <div class="add-icon">
        <div class="circle" @click="addItem"></div>
          
        </div>
        <form @submit.prevent="addItem">
          <input v-bind:style="bgColor" type="text" v-model="entry" placeholder="Create a new todo...">
        </form>
      </div>
   
    </div>

    </div>
    
  </header>
  <div class="todo-list">
  <div v-bind:style="bgColor" class="lists">
    <div class="items" v-for="(item, index) in todoList" :key="index">
      <div class="check-btn">
        <div class="circle"></div>
      </div>
      <div v-bind:style="bgColor" class="item-name">{{item.title}}</div>
      <div class="delete-btn"><i class="fa fa-close"></i></div>
    </div>
    <div class="actions">
        <div class="count"> 5 items left </div>
        <div class="item-actions">
        
              <div class="all"><button class="clear-btn">All</button></div>
              <div class="active"> <button class="clear-btn">Active</button></div>
              <div class="completed"><button class="clear-btn">Complete</button></div>
          
        </div>
        <div class="clear"><div class="">Clear Complete</div></div>
    </div>

  </div>
  
  <div class="card">
    <div class="card-cont">
            <div class="all"><button class="clear-btn">All</button></div>
            <div class="active"> <button class="clear-btn">Active</button></div>
            <div class="completed"><button class="clear-btn">Complete</button></div>
        
    </div>
  </div>
    

  </div>

  
  
</template>

<style scoped>

.circle { 
  width:16px;
  height:16px;
  border-radius:50%;
  border:1px solid hsl(192, 100%, 67%);
  cursor:pointer;
}

.circle:hover { 
 border-color: hsl(192, 100%, 67%) ;
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

.header-title{
  display:flex;
  align-items:center;
}
.title{
  width:50%;
display:flex;
justify-content:flex-start;
}
.theme-icon {
width:50%;
display:flex;
justify-content:flex-end;

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
width:100%;
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
flex-wrap:wrap;
justify-content:center;
width:100%;
background-color:red;

}
.lists{
  background-color:hsl(235, 21%, 11%);
  min-width:70%;
  margin:auto;
}

.items{
  width:calc(100% - 20px);
  flex:100%;
  display:flex;
  gap:10px;
  justitfy-content:center;
  padding: 10px 10px;
  font-size:19px;
  align-items:center;
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
  text-align:center;
}
.delete-btn{ 
  min-width:0 0 10%;
  flex:0 0 10%;
  color:hsl(200, 31%, 21%);
}

.actions {
  display:flex;
  gap:10px;
  justify-content:center;
  align-items:center;
}

.clear-btn{
  padding:5px;
  border:none;
  outline:none;
  background-color:transparent;
  cursor:pointer;
  color:#bbb;
}


@media (min-width: 375px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

.lists{
    width:90%;
    display:flex;
    flex-wrap:wrap;
    justify-content: center;
    
  }

  .actions{
  width:100%;
  pading:10px;
  clear:both;
  overlay:hidden;
  }
  .act {
    display:flex;
    justify-content:center;
    gap:5px;
  }

  

  .count {
    display:flex;
    width:0 0 30%;
    flex:0 0 30%;
    justify-content:center;
  }

  .item-actions {
  display:flex;
  gap:10px;
  justify-content:center;
  width:0 0 30%;
  flex:0 0 30%;

}


  .clear {
    display:flex;
    width:0 0 40%;
    flex:0 0 40%;
    cursor:pointer;
    justify-content:center;
    
  }
 
  .card{
    display:none;
  }

}

@media (max-width: 375px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
     background:url('assets/images/bg-mobile-dark.jpg');
    background-repeat:no-repeat;
    background-size:cover;
  }

  .header-content {
      width:100%;
  }

  .lists{
    width:90%;
    display:flex;
    flex-wrap:wrap;
    justify-content: center;
  }
  .actions{
      width:100%;
  }

 .card{
    display:flex;
    justify-content:center;
    margin-top:15px;
   width:90%;
  }

  .card-cont{
    display:flex;
    justify-content:center;
    width:100%;
    padding:10px;
    background-color:#eee;
  }
  .all, .complete, .active{
    flex:1;
  }

    .item-actions {
      display:none;
    }

    .count {
      font-size:13px;
      font-family: Rubik sans;
      width:0 0 50%;
      flex:0 0 50%;
      text-align:center;
    }

    .clear {
      display:flex;
      width:0 0 50%;
      flex:0 0 50%;
      cursor:pointer;
      justify-content:center;
      font-size:13px;
      
    }

    .complete {
        font-size:14px;
        font-family: Rubik sans;
        display:flex;
        justify-content:center;
        
    }

  }


</style>
