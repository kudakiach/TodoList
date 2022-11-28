<script>
import lightImage from "./assets/images/bg-desktop-light.jpg";
import darkImage from "./assets/images/bg-desktop-dark.jpg";
import mobileDark from "./assets/images/BG-MOBILE-DARK.jpg";
//import sunIcon from "./assets/images/ICON-MOON.SVG"
const body = document.querySelector("body");
export default {
  data: () => {
    return {
      sun: {
        display: "block",
      },
      lineThrough: {
        textDecoration: "line-through",
      },
      moon: {
        display: "none",
      },
      image: darkImage,
      bgImage: {
        backgroundImage: "url(lightImage)",
      },
      inputStyle: {
        backgroundColor: "hsl(235, 21%, 11%)",
        color: "hsl(234, 39%, 85%)",
      },
      list: {
        backgroundColor: "hsl(235, 24%, 19%)",
        color: "hsl(234, 39%, 85%)",
      },
      bgColor: {
        backgroundColor: "hsl(235, 21%, 11%)",
        color: "hsl(234, 39%, 85%)",
      },
      circle: {
        backgroundColor: "none",
      },
      entry: "",
      count: 0,
      complete: 0,
      todoList: [],
      completedList: [],
    };
  },
  methods: {
    addItem() {
      if (this.entry !== "") {
        let date = new Date();
        let newItem = {
          id: date.getTime(),
          title: this.entry,
          complete: false,
        };
        this.count += 1;
        this.todoList.push(newItem);
      }

      this.entry = "";
    },
    clearComplete() {
      this.todoList = this.todoList.filter((item, index) => {
        return !item.complete;
      });
      this.complete = 0;
    },
    deleteItem(item) {
      if (item.complete == true) {
        this.todoList.splice(this.todoList.indexOf(item), 1);
      } else {
        this.count -= 1;
        this.todoList.splice(this.todoList.indexOf(item), 1);
      }
    },

    completeItem(item) {
      if (item.complete == false) {
        const itemId = document.getElementById(item.id);
        const circleId = document.getElementById(
          item.id + this.todoList.indexOf(item) + 1
        );
        item.complete = true;
        this.complete += 1;
        this.count -= 1;
        this.completedList.push(item);
      } else {
        item.complete = false;
        this.completedList.splice(this.completedList.indexOf(item), 1);
        this.count += 1;
      }
    },
    displayAll() {
      return this.todoList;
    },

    completedTasks() {
      let newList =
      this.todoList.filter(item =>
          item.complete == true
      )

      let todoList = newList;

      return todoList
    },

    activeTasks() {
      for (let i = this.todoList.length - 1; i >= 0; i--) {
        if (this.todoList[i].complete == true) {
          this.todoList.splice(i, 1);
        }
      }
    },

    lightTheme() {
      this.bgColor.backgroundColor = "hsl(0, 0%, 98%)";
      this.bgColor.color = "hsl(233, 14%, 35%)";
      this.list.backgroundColor = "hsl(0, 0%, 98%)";
      this.inputStyle.color = "hsl(233, 14%, 35%)";
      this.inputStyle.backgroundColor = "hsl(0, 0%, 98%)";
      this.list.color = "hsl(233, 14%, 35%)";
      this.sun.display = "none";
      this.moon.display = "block";
      this.image = lightImage;
      body.style.backgroundColor = "hsl(236, 33%, 92%)";
    },

    darkTheme() {
      this.bgColor.backgroundColor = "hsl(235, 21%, 11%)";
      this.inputStyle.color = "hsl(234, 39%, 85%)";
      this.inputStyle.backgroundColor = "hsl(235, 24%, 19%)";
      this.bgColor.color = "hsl(236, 9%, 61%)";
      this.list.backgroundColor = "hsl(235, 24%, 19%)";
      this.list.color = "hsl(236, 9%, 61%)";

      this.moon.display = "none";
      this.sun.display = "block";
      this.image = darkImage;
      body.style.backgroundColor = "hsl(235, 21%, 11%)";
    },
  },

  // computed: {
  //   completedTasks: function () {
  //     let todoList = this.todoList;
  //     todoList = this.todoList.filter(item => item.completed)
  //     return todoList;
  //   },
  //   activeTasks () {
  //     return this.todoList.filter(item => !item.completed)
  //   }

  // }
};
</script>

<template>
  <header :style="{ backgroundImage: 'url(' + image + ')' }">
    <div class="header-content">
      <div class="header-title">
        <div class="title">
          <h1>TODO</h1>
        </div>
        <div class="theme-icon">
          <i
            v-bind:style="moon"
            id="mood-id"
            class="fa fa-moon-o fa-1x"
            @click="darkTheme"
          ></i>
          <i
            v-bind:style="sun"
            id="sun-id"
            class="fa fa-sun-o fa-1x"
            @click="lightTheme"
          ></i>
        </div>
      </div>

      <div class="add-todo">
        <div v-bind:style="inputStyle" class="add-item">
          <div class="add-icon">
            <div class="circle" @click="addItem"></div>
          </div>
          <form @submit.prevent="addItem">
            <input
              v-bind:style="inputStyle"
              type="text"
              v-model="entry"
              placeholder="Create a new todo..."
            />
          </form>
        </div>
      </div>
    </div>
  </header>

  <main>
    <div class="todo-list">
      <div  class="lists">
        <div
        v-bind:style="list"
          class="items"
          v-for="(item, index) in todoList"
          :key="index"
          :id="item.id"
          draggable="true"
        >
          <div class="check-btn">
            <div
              :id="item.id + index + 1"
              v-bind:style="circle"
              :class="{ completelist: item.complete }"
              class="circle"
              @click="completeItem(item)"
            >
              <i
                style="font-size: 12px;"
                :class="{ checked: item.complete }"
                class="fa fa-check"
              ></i>
            </div>
          </div>
          <div v-bind:style="list" class="item-name">
            <p :class="{ strokeline: item.complete }">{{ item.title }}</p>
          </div>
          <div class="delete-btn">
            <i class="fa fa-close" @click="deleteItem(item)"></i>
          </div>
        </div>

        <div class="actions"  v-bind:style="list">
          <div class="count">{{ this.count }} items left</div>
          <div class="item-actions">
            <div class="all">
              <button class="clear-btn" @click="displayAll">All</button>
            </div>
            <div class="active">
              <button class="clear-btn" @click="activeTasks">Active</button>
            </div>
            <div class="completed">
              <button class="clear-btn" @click="completedTasks">
                Complete
              </button>
            </div>
          </div>
          <div class="clear">
            <div class="" @click="clearComplete">Clear Complete</div>
          </div>
        </div>

        <div class="card">
        <div class="card-cont">
          <div class="all"><button class="clear-btn">All</button></div>
          <div class="active"><button class="clear-btn">Active</button></div>
          <div class="completed">
            <button class="clear-btn">Complete</button>
          </div>
        </div>
      </div>
      <div class="drag-drop">
        Drag and Drop to reorder list
      </div>
      </div>

     
      
    </div>
  </main>
</template>

<style scoped>
.fa-check {
  display: none;
}
.completelist {
  background: linear-gradient(hsl(192, 100%, 67%), hsl(280, 87%, 65%));
}

.checked {
  display: block;
}
.strokeline {
  text-decoration: line-through;
}
.showIcon {
  display: block;
}
.circle {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  border: 1px solid hsl(192, 100%, 67%);
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}

.circle:hover {
  border-color: hsl(192, 100%, 67%);
}

header {
  display: flex;
  line-height: 1.5;
  justify-content: center;
  align-items: center;
  color: white;
  background-repeat: no-repeat;
  background-size: cover;
  min-height: 250px;
}
.header-content {
  padding: 10px;
  width: 60%;
}

.header-title {
  display: flex;
  align-items: center;
}
.title {
  width: 50%;
  display: flex;
  justify-content: flex-start;
}
.theme-icon {
  width: 50%;
  display: flex;
  justify-content: flex-end;
}

.header-content h1 {
  margin-bottom: 25px;
  font-weight: 700;
  font-family: Rubik sans;
  letter-spacing: 3px;
}
.add-item {
  display: flex;
  gap: 20px;
  border: 1px solid #fffff;
  background-color: #ffffff;
  padding: 5px;
  align-items: center;
}

form {
  width: 100%;
}

input[type="text"] {
  padding: 1px;
  font-weight: 400;
  font-family: Rubik Sans;
  font-size: 19px;
  width: 100%;
  border: none;
  height: inherit;
  outline: none;
}

.todo-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: auto;
  width: 60%;
}

.list-container {
  width: 100%;
  padding: 10px;
}

.lists {
  /* background-color:hsl(235, 21%, 11%);*/
  width: 100%;
  margin: auto;
  padding: 10px;
  position: absolute;
  top: -30px;
}

.items {
  width: 100%;
  flex: 100%;
  display: flex;
  gap: 10px;
  /* background-color: rgb(37, 39, 60); */
  justify-content: center;
  padding:15px;
  font-size: 19px;
  align-items: center;
  color: white;
  border-bottom: 1px solid hsl(234, 39%, 85%);
}

.items:hover .delete-btn {
  display: block;
}

.border-b {
  background-color: #333;
  max-height: 1px;
  min-width: 0 0 100%;
  flex: 0 0 100%;
}
.check-btn {
  min-width: 0 0 10%;
  flex: 0 0 10%;
}

.item-name {
  min-width: 0 0 80%;
  flex: 0 0 80%;
  text-align: center;
}
.delete-btn {
  min-width: 0 0 10%;
  flex: 0 0 10%;
  color: hsl(200, 31%, 21%);
}

.item-actions{
  display: flex;
}
.card {
 display:none;
}

.drag-drop{
  text-align: center;
}

.actions {
  display: flex;
  gap: 10px;
  justify-content: center;
  align-items: center;
  /* background-color: rgb(37, 39, 60); */
  padding:7px;
}

.clear-btn {
  padding: 5px;
  border: none;
  outline: none;
  background-color: transparent;
  cursor: pointer;
  color: #bbb;
}

.clear-btn:hover {
  color: hsl(235, 88%, 75%);
}

.drag-drop{
  margin-top:30px;
}


@media (max-width: 414px) {
  header {
    display: flex;
    min-width: 100%;
    background-color:red;
    align-items: center;
    justify-content: center;
    background-repeat: no-repeat;
    background-size: cover;
  }

  .header-content {
    width: 90%;
    margin:auto;
  }

  .header-title{
    display:flex;
  }
.title{
  display:flex;
  justify-content: flex-start;
  width:70%
}
.theme-icon{
  width: 30%;
  display:flex;
  justify-content: flex-end;
}
  .todo-list {
    width: 85%;
    margin: auto;
  }

  .lists {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  .actions {
    width: 100%;
  }

  .card {
    display: flex;
    justify-content: center;
    margin-top: 15px;
    width: 100%;
  }

  .card-cont {
    display: flex;
    justify-content: center;
    width: 100%;
    background-color: #eee;
    padding:0 10px;
  }
  .all,
  .complete,
  .active {
    flex: 1;
    font-family: Rubik sans;
  }

  .item-actions {
    display: none;
  }

  .count {
    font-size: 13px;
    font-family: Rubik sans;
    width: 0 0 50%;
    flex: 0 0 50%;
    text-align: center;
  }

  .clear {
    display: flex;
    width: 0 0 50%;
    flex: 0 0 50%;
    cursor: pointer;
    font-family: Rubik sans;
    justify-content: center;
    font-size: 13px;
  }

  .complete {
    font-size: 13px;
    font-family: Rubik sans;
    display: flex;
    justify-content: center;
  }
}
</style>
