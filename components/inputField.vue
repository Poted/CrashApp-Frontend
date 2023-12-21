<template>
  <div class="inputGroup" >
    
    <!-- <textarea v-if="isTextArea" :type="inputType" :required="requiredField" autocomplete="off" @focus="isFocused = true"
      @blur="isFocused = false" maxlength=30 v-model="inputValue"></textarea>
     -->
      <textarea v-if="isTextArea" :type="inputType" :required="requiredField" autocomplete="off" @focus="isFocused = true"
      @blur="isFocused = false" maxlength=300 v-model="inputValue" ></textarea>
    

    <input v-else :type="inputType" :required="requiredField" autocomplete="off" @focus="isFocused = true"
      @blur="isFocused = false" maxlength=30 v-model="inputValue"/>
    <label :class="{ 'labelActive': isFocused || inputValue }">{{ label }}</label>
    <!-- <label :for="labelFor" :class="{ 'labelActive': isFocused || inputValue }">{{ label }}</label> -->
  </div>
</template>
  
<script>
export default {

  props: {
    label: {
      type: String,
      default: 'Input',
    },

    requiredField: {
      type: Boolean,
      default: false,
    },

    isTextArea: {
      type: Boolean,
      default: false,
    },

    
    inputType: {
      type: String,
      default: "text",
    },
  },

  data() {
    return {
      inputValue: '',
      isFocused: false,
      // labelFor: "name",
    };
  },

  methods: {
    clearInputValue() {
        this.inputValue = ''
    },

  }

};
</script>
  
<style scoped lang="scss">

.inputGroup {  

  font-family: 'Segoe UI', sans-serif;
  margin: 1em 0 1em 0;
  position: relative;

  input, textarea {
    font-size: 100%;
    padding: 0.8em;
    outline: none;
    border: 2px solid rgb(200, 200, 200);
    background-color: transparent;
    border-radius: 20px;
    width: 100%;
  }

  label {
    margin-left: 0.5em;
    pointer-events: none;
    position: absolute;
  }

  label, textarea {
    font-size: 100%;
    left: 0;
    padding: 0.8em;
    transition: all 0.3s ease;
    color: rgb(100, 100, 100);  
  }

  .labelActive {
    transform: translateY(-50%) scale(.9);
    margin: 0em;
    margin-left: 1.3em;
    color: black;
    border-radius: 10px;
    padding: 0.3em 0.5em 0.3em 0.5em;
    background-color: #e8e8e8;
  }

  textarea {
    color: white;
    min-height: 60px;
    max-height: 320px;
  }
  
  textarea:focus,
  textarea:valid, 
  input:focus,
  input:valid {
    background-color: rgba(1, 1, 1, 0.2);
    border-color: violet;
  }


  textarea::-webkit-scrollbar {
    width: 12px;
  }
  
  textarea::-webkit-scrollbar-track {
    border-radius: 3px;
    background: #f1f1f1; 
    margin-top: 15px;
  }
  
  textarea::-webkit-scrollbar-thumb {
    background-color: #888;
    border-radius: 3px;
  }
  
  textarea::-webkit-scrollbar-thumb:hover {
  background-color: #555; 
}


}


</style>
  