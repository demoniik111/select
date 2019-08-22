<template>
  <div id="app">
    <h1>My-select</h1>
    <div class="parent">
      <div
        v-for="(e,i) in propers"
        :key="i"
        class="input"
        :class="e.class"
        @click="e.checked=!e.checked">
          <input type="checkbox" :id="e.class" name="scales" :checked="e.checked">
          <label @click="e.checked=!e.checked" :for="e.class">{{e.class}}</label>
      </div>
    </div>
    <Select
      :source="mass"
      :searchLine="propers.filter(e => e.class === 'searchLine')[0].checked"
      :allowEmpty="propers.filter(e => e.class === 'allowEmpty')[0].checked"
      v-model="inputValue"
    /> 
  </div>
</template>

<script>
import Select from "./components/Select";

export default {
  name: "App",
  components: {
    Select
  },
  data: function(){
    return {
      mass: [
        {key: 'm', value: 'male'},
        {key: 'f', value: 'female'},
        {key: '0', value: ''}
      ],
      inputValue: '',
      propers: [
        {
          class: "allowEmpty",
          checked: true,
        },
        {
          class: "searchLine",
          checked: false,
        }
      ]
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  .parent {
    display: flex;
    justify-content: center;
    margin: 10px;

    .input{
      cursor: pointer;
      width: auto;
      padding: 10px;
      display: flex;
      align-items: center;
    }

    .input * {
      cursor: pointer;
    }
  }
}
</style>
