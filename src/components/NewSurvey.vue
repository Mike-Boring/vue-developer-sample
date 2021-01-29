<template>
  <div class="new-survey">
    <div class="survey-data-column-nm" v-if="editName">
      <input
        v-model="study.studyName"
        @keyup.enter="nonEditMode"
        @blur="nonEditMode"
        id="studyNameValue"
      />
    </div>
    <div class="survey-data-column-nm" v-else>
      {{ study.studyName }}
      <font-awesome-icon
        icon="pencil-alt"
        id="edit-icon"
        v-on:click="editMode"
      />
    </div>
    <div class="survey-data-column">{{ study.id }}</div>
    <div class="survey-data-column">{{ study.creationDate }}</div>
    <div class="survey-data-column">{{ study.numCompletes }}</div>
    <div class="survey-data-column-add-delete">
      <button class="add-complete" v-on:click="study.numCompletes += 1">
        Add Complete</button
      ><font-awesome-icon
        id="delete-icon"
        icon="trash-alt"
        v-on:click="$emit('delete-study')"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "studyData",
  props: ["study"],
  data() {
    return {
      editName: false,
    };
  },
  methods: {
    editMode() {
      this.editName = true;
      this.focusInput();
    },
    nonEditMode() {
      this.editName = false;
    },
  },
};
</script>

<style scoped>
div.new-survey {
  display: flex;
  justify-content: space-between;
  background-color: white;
  border-radius: 5px;
  padding: 5px;
  width: 1050px;
  margin: auto;
  margin-bottom: 10px;
}
div.survey-data-column-nm {
  flex-basis: 45%;
  padding: 5px;
  text-align: left;
  font-weight: bold;
}
.survey-data-column {
  padding: 5px;
  flex-basis: 140px;
  text-align: left;
  font-size: 13px;
  font-weight: 500;
}
.survey-data-column-add-delete {
  padding: 5px;
  flex-basis: 140px;
  text-align: right;
}
button.add-complete {
  margin-right: 25px;
  box-shadow: 2px 2px 2px lightgrey;
  border-radius: 5px;
  border: 1px solid lightgrey;
  padding: 5px;
  color: #4176a5;
  background-color: #dad7d7;
}
button.add-complete:hover {
  background-color: #ece8e8;
}
#delete-icon {
  color: darkgrey;
}
#delete-icon:hover {
  color: lightgrey;
}
#edit-icon {
  color: darkgrey;
}
#edit-icon:hover {
  color: lightgrey;
}
</style>
