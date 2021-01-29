<template>
  <div id="app">
    <div class="survey-headers">
      <div class="survey-data-column-nm-headers">Study Name</div>
      <div class="survey-data-column-headers">Study ID</div>
      <div class="survey-data-column-headers">Created</div>
      <div class="survey-data-column-headers">Completes</div>
      <div class="survey-data-column-headers"> </div>
    </div>
    <NewSurvey
      v-for="(study,index) in studyData"
      v-bind:study="study"
      v-on:delete-study="deleteStudy(index)"
     
      v-bind:key="study.id"
      :set="study.numCompletes = parseInt(study.numCompletes)"
      ></NewSurvey>
      <div class="add-survey"><button class="add-btn" v-on:click="addStudy">+ Add Study</button></div>
  </div>
</template>

<script>
  import NewSurvey from './components/NewSurvey.vue'
  import moment from 'moment'
  export default {
    name: 'app',
    components: {
      NewSurvey
    },
    data() {
      return {
        studyData: null
      }
    },
    methods: {
      deleteStudy: function(index) {
        this.studyData.splice(index,1);
      },
      addStudy: function() {
        let newStudy = {"id": this.formatId(),
          "studyName":"Untitled Study",
          "creationDate": this.formatDate(new Date()),
          "numCompletes": 0} 
        this.studyData.push(newStudy)
      },
      formatDate(value){
        if (value) {
          return moment(value).format('MMMM DD, YYYY')
        }
      },
      formatId(){
        return parseInt(this.studyData[this.studyData.length - 1].id) + 1;
      },
    },
    async created() {
        const response = await fetch("https://www.cxsurveys.com/devtest/getStudyData.php");
        const data = await response.json();
        this.studyData = data.studyData;
      }
  }
</script>
<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    margin-top: 200px;
  }
  body {
    background-color: #4176a5;
  }
  div.survey-headers {
    display: flex;
    justify-content: space-between;
    padding: 5px;
    width: 1050px;
    margin: auto;
    font-weight: bold;
    font-size: 14px;
  }
  div.survey-data-column-nm-headers {
    flex-basis: 45%;
    color: white;
    text-align: left;
  }
  div.survey-data-column-headers {
    flex-basis: 140px;
    color: white;
    text-align: left;
  }
  div.add-survey {
    padding: 5px;
    width: 1050px;
    margin: auto;
    text-align: left;
  }
  button.add-btn {
    box-shadow: 2px 2px 2px #224b6e;
    border-radius: 5px;
    border: none;
    padding: 5px;
    color: white;
    background-color: #224b6e;
  }
</style>
