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
          <input type="radio" id="addicon" name="icon" @click="addItem">
        </div>
        <form @submit.prevent="addItem">
            <input type="text" id="add-input" placeholder="Create a new todo...">
          </form>
      </div>
   
    </div>

    </div>
    
  </header>
  <div class="todo-list">
    <div class="items" v-for="(item, index) in todoList">
      <div class="check-btn"></div>
      <div class="item-name"></div>
      <div class="delete-btn"></div>
    </div>
  </div>

</template>

<style scoped>
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
  padding-left:20px;
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
  gap:10px;
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

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

}
</style>
