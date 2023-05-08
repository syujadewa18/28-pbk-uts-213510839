<template>
  <div>
    <h1>TO-DO List</h1>
    <form @submit.prevent="addActivity">
      <input class="addactivity" type="text" v-model="newActivity" placeholder="Tambahkan Aktivitas Anda...">
      <button class="button1">Add</button>
    </form>
    <ul class="ul">
      <li class="li" v-for="(activity, index) in filteredActivities" :key="index" :class="{ done: activity.completed }">
        <input type="checkbox" v-model="activity.completed">
        <span>{{ activity.text }}</span>
        <button @click="removeActivity(index)">Remove</button>
      </li>
    </ul>
    <div>
      <label class="label1">Tampilkan aktivitas ganteng:</label>
      <input class="input1" type="checkbox" v-model="showUnfinished">
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '',
      activities: [
        { text: 'Pray To God 5:00 AM', completed: false },
        { text: 'Clean House 6:00 AM - 11:00 AM', completed: true },
        { text: 'Rest 6:00 PM - 5:00 AM ', completed: false }
      
      ],
      showUnfinished: false
    }
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        this.activities.push({ text: this.newActivity, completed: false });
        this.newActivity = '';
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    }
  },
  computed: {
    filteredActivities() {
      if (this.showUnfinished) {
        return this.activities.filter(activity => !activity.completed);
      } else {
        return this.activities;
      }
    }
  }
}
</script>

<style>
.done {
  text-decoration: line-through;
}
.input{
  padding: 10px;
  border: none;
  border-radius: 5px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
  margin-right: 20px;
  width: 60%;
  text-align: center;
  letter-spacing: normal;
  display: flex;
  justify-content: center;
}

.addactivity{
  letter-spacing: normal;
  padding: 5px;
  text-align: center;
  border-radius: 10px;
  width: 50%;
  margin: 10px;
  text-align: center;
  height: 20px;
  width: 500px;
  
 
}

button{
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background-color: #1E90FF;
  color: white;
  cursor: pointer;
}
ul{
  list-style: none;
  margin: 0;
  padding: 0;
}
li{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: green;
  margin-bottom: 10px;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
}

html{
  background-color: bisque;
}

h1{
  text-align: center;
}

form{
  display: flex;
  justify-content: center;
  
}
.button1{
  padding: 10px;
  border: none;
  border-radius: 5px;
  background-color: red;
  color: white;
  cursor: pointer;
  width: 60px;
  height: 40px;
}


</style>
