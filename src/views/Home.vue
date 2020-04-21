<template>
  <div class="home">
    <button class="btn" @click="addList">Add your list</button>
    <input v-model="topic" id="topic" placeholder="Enter your topic" />
    <div class="side">
      <div class="cards" v-for="(list, index) in lists" :key="index">
        
        <form @submit="pushItems(index)" @submit.prevent="onSubmit">
          <h3>{{ list.topic }}</h3>
          <input v-model="title" id="title" placeholder="Title" />
          <input v-model="descr" id="descr" placeholder="Description" />
          <button class="btn">ADD</button>
        </form>

        <draggable ghost-class="ghost" @end="onEnd">
          <transition-group type="transition" name="flip-list">
            <div v-for="(item, ind) in list.items" :key="ind">
              <div class="car">
                <div class="card">
                  {{ ind + 1 }}-<strong>{{ item.title }}:</strong>
                  <div id="des">{{ item.descr }}</div>
                </div>
              </div>
            </div>
          </transition-group>
        </draggable>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "Home",
  components: {
    draggable,
  },
  data() {
    return {
      lists: [],
      title: "",
      descr: "",
      topic: "",
      oldIndex: "",
      newIndex: "",
    };
  },
  methods: {
    onEnd() {
      console.log(event);
      this.oldIndex = event.oldIndex;
      this.newIndex = event.newIndex;
    },

    pushItems(ind) {
      if (this.title && this.descr !== "")
        var it = {
          title: this.title,
          descr: this.descr,
        };
      this.lists[ind].items.push(it);
    },
    onSubmit() {
      this.title = "";
      this.descr = "";
      this.topic = "";
    },
    addList() {
      if (this.topic != "") {
        var board = {
          topic: this.topic,
          items: [],
        };
        this.lists.push(board);
      }
    },
  },
};
</script>

<style scope="global">
.home {
  display: grid;
  width: 900px;
  height: 550px;
  margin: auto;
  justify-items: center;
  border-radius: 16px 16px 16px 16px;
  display: inline-block;
}
#topic {
  height: 25px;
  color: black;
  margin-left: 16px;
  font-weight: bold;
  text-align: left;
  border-radius: 7px;
  padding: 3px;

}
h3 {
  color: aliceblue;
  font-size: 20px;
}

.side {
  display: grid;
  grid-template-columns: 300px 300px;
  grid-template-rows: 200px 200px;
  grid-gap: 170px;
  margin-bottom: 100px;
}

.btn {
  margin: 20px;
  padding: 7px;
  border-radius: 6px;
  background-color: rgb(22, 1, 7);
  color: rgb(242, 244, 247);
  display: inline-block;
  border: black;
}

.cards {
  width: 390px;
  height: 290px;
  background: #870000;
  background: -webkit-linear-gradient(to right, #190a05, #870000);
  background: linear-gradient(to right, #190a05, #870000);
  display: grid;
  justify-content: center;
  border-radius: 20px 0px 0px 20px;
  border-top-color: black solid;
  overflow-y: scroll;
}
::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px grey;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  background: rgb(54, 5, 5);
  /* background-color: #000000; */
  border-radius: 5px;
}

.car {
  background-color: rgb(241, 243, 242);
  width: 65%;
  height: 40px;
  text-align: left;
  margin-top: 10px;
  margin-left: 20px;
  margin-bottom: 12px;
  border-left-style: solid;
  border-radius: 4px;
  cursor: pointer;
}
.card {
  display: inline;
  margin: 20px;
  font-weight: bold;
}

#descr {
  width: 60%;
  height: 21px;
  border-radius: 3px;
  /* margin-left: 20px; */
  display: inline-block;
  padding: 5px;
}
#title {
  width: 40%;
  height: 14px;
  border-radius: 3px;
  /* margin-left: 9px; */
  display: inline-block;
  padding: 5px;
  margin-right: 160px;
}

#des {
  margin-left: 60px;
  color: darkred;
}
</style>
