<template>
  <div class="ui-wrapper">
    <input v-for="(country, index) in countries" :key="index" :id="country.id" name="flag" type="radio">
    <input @blur="closeDropdown" class="dropdown-checkbox" name="dropdown" id="dropdown" type="checkbox">
    <label @click="openDropdown" class="dropdown-container" for="dropdown"></label>
    <div class="input-wrapper" >
      <legend>
        <label for="phonenumber">
          Phonenumber
        </label>
      </legend>
      <div class="textfield">
        <input pattern="\d+" maxlength="11" id="phonenumber" type="text">
        <span class="invalid-msg">This is not a valid phone number</span>
      </div>
    </div>
    <div  v-if="bul" class="select-wrapper">
      <!-- <ul > -->
      <ul>
        <li v-for="(country, index) in countries" :key="index" :class="country.id">
          <label :for="country.id"><span>{{ country.flag }}</span>{{ country.name }}</label>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {

  
  data() {
    return {
      
      bul: true,

      countries: [
        { id: 'Austria', name: 'Austria', flag: '🇦🇹' },
        { id: 'Belgium', name: 'Belgium', flag: '🇧🇪' },
        { id: 'Bulgaria', name: 'Bulgaria', flag: '🇧🇬' },
        { id: 'Croatia', name: 'Croatia', flag: '🇭🇷' },
        { id: 'Cyprus', name: 'Cyprus', flag: '🇨🇾' },
        { id: 'Czech', name: 'Czech Republic', flag: '🇨🇿' },
        { id: 'Denmark', name: 'Denmark', flag: '🇩🇰' },
        { id: 'Estonia', name: 'Estonia', flag: '🇪🇪' },
        { id: 'Finland', name: 'Finland', flag: '🇫🇮' },
        { id: 'France', name: 'France', flag: '🇫🇷' },
        { id: 'Germany', name: 'Germany', flag: '🇩🇪' },
        { id: 'Greece', name: 'Greece', flag: '🇬🇷' },
        { id: 'Hungary', name: 'Hungary', flag: '🇭🇺' },
        { id: 'Iceland', name: 'Iceland', flag: '🇮🇸' },
        { id: 'Ireland', name: 'Republic of Ireland', flag: '🇮🇪' },
        { id: 'Italy', name: 'Italy', flag: '🇮🇹' },
        { id: 'Latvia', name: 'Latvia', flag: '🇱🇻' },
        { id: 'Liechtenstein', name: 'Liechtenstein', flag: '🇱🇮' },
        { id: 'Lithuania', name: 'Lithuania', flag: '🇱🇹' },
        { id: 'Luxembourg', name: 'Luxembourg', flag: '🇱🇺' },
        { id: 'Malta', name: 'Malta', flag: '🇲🇹' },
        { id: 'Netherlands', name: 'Netherlands', flag: '🇳🇱' },
        { id: 'Norway', name: 'Norway', flag: '🇳🇴' },
        { id: 'Poland', name: 'Poland', flag: '🇵🇱' },
        { id: 'Portugal', name: 'Portugal', flag: '🇵🇹' },
        { id: 'Romania', name: 'Romania', flag: '🇷🇴' },
        { id: 'Slovakia', name: 'Slovakia', flag: '🇸🇰' },
        { id: 'Slovenia', name: 'Slovenia', flag: '🇸🇮' },
        { id: 'Spain', name: 'Spain', flag: '🇪🇸' },
        { id: 'Sweden', name: 'Sweden', flag: '🇸🇪' }
      ]
    };
  },
  methods: {
    
    
    openDropdown() {
      console.log("1: " + this.bul)
        this.bul = true; // Set bul to true when the input is focused
        console.log("2: " + this.bul)

      },
      closeDropdown() {
        // Delay setting bul to false to allow click events to propagate
        setTimeout(() => {
          this.bul = false; // Set bul to false when the input loses focus
        }, 2);
    }
    
  }
  
};
</script>

<style scoped>
.ui-wrapper {
  --width: 250px;
  --height:60px;
  --background: #383535;
  --text-color: rgb(255, 255, 255);
  --border-color:  violet;
  --border-focus-color: rgb(185, 184, 184);
  --shadow-color: rgba(32, 34, 36, 0.2);
  --shadow-focus-color: rgba(0, 110, 255, 0.2);
  --dropdown-button-color: #292727;
  --dropdown-button-hover-color: #292727;
}

.ui-wrapper *,
.ui-wrapper *::before,
.ui-wrapper *::after {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  font-family: sans-serif;
  color: var(--text-color);
}

.ui-wrapper {
  width: var(--width);
  height: var(--height);
  display: -webkit-inline-box;
  display: -ms-inline-flexbox;
  display: inline-flex;
  border-radius: 10px;
  position: relative;
  border: 2px solid var(--border-color);
  background-color: var(--background);
  -webkit-box-pack: justify;
  -ms-flex-pack: justify;
  justify-content: space-between;
  padding-right: 10px;
  -webkit-box-shadow: 0px 2px 5px 0px var(--shadow-color);
  box-shadow: 0px 2px 5px 0px var(--shadow-color);
  -webkit-transition: .4s;
  -o-transition: .4s;
  transition: .4s;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  margin-top: 2vh;
}

.ui-wrapper>input {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  margin: 0;
  width: 0;
  height: 0;
  opacity: 0;
  position: absolute;
  left: 9999px;
}

.dropdown-container {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  padding: 0 10px;
  cursor: pointer;
  border-radius: 20px 0 0 20px;
  background-color: var(--dropdown-button-color);
}

.dropdown-container::before {
  content: "🇦🇹";
  font-size: 20px;
  background: none !important;
}

.dropdown-container::after {
  content: "";
  background-image: url("data:image/svg+xml;base64,PHN2ZyBmaWxsPSIjNDk0OTQ5IiB3aWR0aD0iNzAwcHQiIGhlaWdodD0iNzAwcHQiIHZlcnNpb249IjEuMSIgdmlld0JveD0iMCAwIDcwMCA3MDAiCiAgICB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj4KICAgIDxwYXRoCiAgICAgICAgZD0ibTM4MC4zOSA0ODQuNzkgMzA3LjA0LTMwNS45OWMxNi43NjYtMTcuODEyIDE2Ljc2Ni00NS4wNTkgMC02MS44MjgtMTYuNzY2LTE2Ljc2Ni00NS4wNTktMTYuNzY2LTYxLjgyOCAwbC0yNzUuNiAyNzUuNi0yNzUuNi0yNzUuNmMtMTcuODEyLTE2Ljc2Ni00NS4wNTktMTYuNzY2LTYxLjgyOCAwLTE2Ljc2NiAxNi43NjYtMTYuNzY2IDQ0LjAxMiAwIDYxLjgyOGwzMDUuOTkgMzA1Ljk5YzE3LjgxMiAxNi43NjYgNDUuMDU5IDE2Ljc2NiA2MS44MjggMHoiCiAgICAgICAgZmlsbC1ydWxlPSJjdXJyZW50Q29sb3IiIC8+Cjwvc3ZnPg==");
  width: 12px;
  height: 12px;
  background-position: center;
  background-size: cover;
  margin-left: 5px;
  -webkit-transition: .2s;
  -o-transition: .2s;
  transition: .2s;
}

.select-wrapper {
  width: var(--width);
  position: absolute;
  top: calc(var(--height) + 20px);
  left: 0;
  opacity: 0;
  visibility: hidden;
  -webkit-transition: .2s;
  -o-transition: .2s;
  transition: .2s;
  
}

.select-wrapper ul {
  width: 100%;
  background-color: rgb(51, 50, 50);
  border-radius: 10px;
  border: 2px solid white;
  padding: 10px;
  margin: 0;
  list-style: none;
  height: 300px;
  display: -webkit-inline-box;
  display: -ms-inline-flexbox;
  display: inline-flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
  overflow-y: auto;
  white-space: nowrap;
}

.select-wrapper ul li {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  padding: 5px;
  border-radius: 5px;
}

.select-wrapper ul li label {
  width: 100%;
}

.select-wrapper ul li,
.select-wrapper ul li * {
  cursor: pointer;
}

.select-wrapper ul li:hover {
  background: lightgray;
}

.select-wrapper ul li span {
  display: inline-block;
  margin-right: 15px;
}

.input-wrapper {
  width: 100%;
  padding-left: 10px;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  justify-content: center;
  row-gap: 2px;
}

.input-wrapper legend {
  font-size: 11px;
}

.input-wrapper .textfield {
  width: 100%;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
}

.input-wrapper .textfield::before {
  content: "+31";
  margin-right: 5px;
  white-space: nowrap;
}

.input-wrapper .textfield input {
  width: 100%;
  font-size: 16px;
  outline: none;
  border: none;
  background: none;
}

.invalid-msg {
  font-size: 18px;
  position: absolute;
  color: red;
  background-color: rgba(0, 0, 0, 0.5);
  width: 100%;
  text-align: center;
  border-radius: 0 0 15px 15px;
  top: 115%;
  left: 0;
  opacity: 0;
  visibility: hidden;
  -webkit-transition: .2s;
  -o-transition: .2s;
  transition: .2s;
  padding: 2px 0 4px 0;
}

/* actions */

#phonenumber:invalid+.invalid-msg {
  top: 110%;
  opacity: 1;
  visibility: visible;
}

.ui-wrapper:focus-within {
  border-color: var(--border-focus-color);
  -webkit-box-shadow: 0px 2px 5px 0px var(--shadow-focus-color);
  box-shadow: 0px 2px 5px 0px var(--shadow-focus-color);
}

.dropdown-container:hover {
  background-color: var(--dropdown-button-hover-color);
}

.dropdown-checkbox:checked~.select-wrapper {
  top: calc(var(--height) + 5px);
  opacity: 1;
  visibility: visible;
}

.dropdown-checkbox:checked+.dropdown-container::after {
  rotate: 180deg;
  translate: 0 -2px;
}

.ui-wrapper input#Austria:checked~.dropdown-container::before,
.ui-wrapper input#Austria:checked~.select-wrapper li.Austria {
  content: "🇦🇹";
  background-color: lightgray;
}

.ui-wrapper input#Belgium:checked~.dropdown-container::before,
.ui-wrapper input#Belgium:checked~.select-wrapper li.Belgium {
  content: "🇧🇪";
  background-color: lightgray;
}

.ui-wrapper input#Bulgaria:checked~.dropdown-container::before,
.ui-wrapper input#Bulgaria:checked~.select-wrapper li.Bulgaria {
  content: "🇧🇬";
  background-color: lightgray;
}

.ui-wrapper input#Croatia:checked~.dropdown-container::before,
.ui-wrapper input#Croatia:checked~.select-wrapper li.Croatia {
  content: "🇭🇷";
  background-color: lightgray;
}

.ui-wrapper input#Cyprus:checked~.dropdown-container::before,
.ui-wrapper input#Cyprus:checked~.select-wrapper li.Cyprus {
  content: "🇨🇾";
  background-color: lightgray;
}

.ui-wrapper input#Czech:checked~.dropdown-container::before,
.ui-wrapper input#Czech:checked~.select-wrapper li.Czech {
  content: "🇨🇿";
  background-color: lightgray;
}

.ui-wrapper input#Denmark:checked~.dropdown-container::before,
.ui-wrapper input#Denmark:checked~.select-wrapper li.Denmark {
  content: "🇩🇰";
  background-color: lightgray;
}

.ui-wrapper input#Estonia:checked~.dropdown-container::before,
.ui-wrapper input#Estonia:checked~.select-wrapper li.Estonia {
  content: "🇪🇪";
  background-color: lightgray;
}

.ui-wrapper input#Finland:checked~.dropdown-container::before,
.ui-wrapper input#Finland:checked~.select-wrapper li.Finland {
  content: "🇫🇮";
  background-color: lightgray;
}

.ui-wrapper input#France:checked~.dropdown-container::before,
.ui-wrapper input#France:checked~.select-wrapper li.France {
  content: "🇫🇷";
  background-color: lightgray;
}

.ui-wrapper input#Germany:checked~.dropdown-container::before,
.ui-wrapper input#Germany:checked~.select-wrapper li.Germany {
  content: "🇩🇪";
  background-color: lightgray;
}

.ui-wrapper input#Greece:checked~.dropdown-container::before,
.ui-wrapper input#Greece:checked~.select-wrapper li.Greece {
  content: "🇬🇷";
  background-color: lightgray;
}

.ui-wrapper input#Hungary:checked~.dropdown-container::before,
.ui-wrapper input#Hungary:checked~.select-wrapper li.Hungary {
  content: "🇭🇺";
  background-color: lightgray;
}

.ui-wrapper input#Iceland:checked~.dropdown-container::before,
.ui-wrapper input#Iceland:checked~.select-wrapper li.Iceland {
  content: "🇮🇸";
  background-color: lightgray;
}

.ui-wrapper input#Ireland:checked~.dropdown-container::before,
.ui-wrapper input#Ireland:checked~.select-wrapper li.Ireland {
  content: "🇮🇪";
  background-color: lightgray;
}

.ui-wrapper input#Italy:checked~.dropdown-container::before,
.ui-wrapper input#Italy:checked~.select-wrapper li.Italy {
  content: "🇮🇹";
  background-color: lightgray;
}

.ui-wrapper input#Latvia:checked~.dropdown-container::before,
.ui-wrapper input#Latvia:checked~.select-wrapper li.Latvia {
  content: "🇱🇻";
  background-color: lightgray;
}

.ui-wrapper input#Liechtenstein:checked~.dropdown-container::before,
.ui-wrapper input#Liechtenstein:checked~.select-wrapper li.Liechtenstein {
  content: "🇱🇮";
  background-color: lightgray;
}

.ui-wrapper input#Lithuania:checked~.dropdown-container::before,
.ui-wrapper input#Lithuania:checked~.select-wrapper li.Lithuania {
  content: "🇱🇹";
  background-color: lightgray;
}

.ui-wrapper input#Luxembourg:checked~.dropdown-container::before,
.ui-wrapper input#Luxembourg:checked~.select-wrapper li.Luxembourg {
  content: "🇱🇺";
  background-color: lightgray;
}

.ui-wrapper input#Malta:checked~.dropdown-container::before,
.ui-wrapper input#Malta:checked~.select-wrapper li.Malta {
  content: "🇲🇹";
  background-color: lightgray;
}

.ui-wrapper input#Netherlands:checked~.dropdown-container::before,
.ui-wrapper input#Netherlands:checked~.select-wrapper li.Netherlands {
  content: "🇳🇱";
  background-color: lightgray;
}

.ui-wrapper input#Norway:checked~.dropdown-container::before,
.ui-wrapper input#Norway:checked~.select-wrapper li.Norway {
  content: "🇳🇴";
  background-color: lightgray;
}

.ui-wrapper input#Poland:checked~.dropdown-container::before,
.ui-wrapper input#Poland:checked~.select-wrapper li.Poland {
  content: "🇵🇱";
  background-color: lightgray;
}

.ui-wrapper input#Portugal:checked~.dropdown-container::before,
.ui-wrapper input#Portugal:checked~.select-wrapper li.Portugal {
  content: "🇵🇹";
  background-color: lightgray;
}

.ui-wrapper input#Romania:checked~.dropdown-container::before,
.ui-wrapper input#Romania:checked~.select-wrapper li.Romania {
  content: "🇷🇴";
  background-color: lightgray;
}

.ui-wrapper input#Slovakia:checked~.dropdown-container::before,
.ui-wrapper input#Slovakia:checked~.select-wrapper li.Slovakia {
  content: "🇸🇰";
  background-color: lightgray;
}

.ui-wrapper input#Slovenia:checked~.dropdown-container::before,
.ui-wrapper input#Slovenia:checked~.select-wrapper li.Slovenia {
  content: "🇸🇮";
  background-color: lightgray;
}

.ui-wrapper input#Spain:checked~.dropdown-container::before,
.ui-wrapper input#Spain:checked~.select-wrapper li.Spain {
  content: "🇪🇸";
  background-color: lightgray;
}

.ui-wrapper input#Sweden:checked~.dropdown-container::before,
.ui-wrapper input#Sweden:checked~.select-wrapper li.Sweden {
  content: "🇸🇪";
  background-color: lightgray;
}

.ui-wrapper input#Austria:checked~.input-wrapper .textfield::before {
  content: "+43";
}

.ui-wrapper input#Belgium:checked~.input-wrapper .textfield::before {
  content: "+32";
}

.ui-wrapper input#Bulgaria:checked~.input-wrapper .textfield::before {
  content: "+359";
}

.ui-wrapper input#Croatia:checked~.input-wrapper .textfield::before {
  content: "+385";
}

.ui-wrapper input#Cyprus:checked~.input-wrapper .textfield::before {
  content: "+357";
}

.ui-wrapper input#Czech:checked~.input-wrapper .textfield::before {
  content: "+420";
}

.ui-wrapper input#Denmark:checked~.input-wrapper .textfield::before {
  content: "+45";
}

.ui-wrapper input#Estonia:checked~.input-wrapper .textfield::before {
  content: "+372";
}

.ui-wrapper input#Finland:checked~.input-wrapper .textfield::before {
  content: "+358";
}

.ui-wrapper input#France:checked~.input-wrapper .textfield::before {
  content: "+33";
}

.ui-wrapper input#Germany:checked~.input-wrapper .textfield::before {
  content: "+49";
}

.ui-wrapper input#Greece:checked~.input-wrapper .textfield::before {
  content: "+30";
}

.ui-wrapper input#Hungary:checked~.input-wrapper .textfield::before {
  content: "+36";
}

.ui-wrapper input#Iceland:checked~.input-wrapper .textfield::before {
  content: "+354";
}

.ui-wrapper input#Ireland:checked~.input-wrapper .textfield::before {
  content: "+353";
}

.ui-wrapper input#Italy:checked~.input-wrapper .textfield::before {
  content: "+39";
}

.ui-wrapper input#Latvia:checked~.input-wrapper .textfield::before {
  content: "+371";
}

.ui-wrapper input#Liechtenstein:checked~.input-wrapper .textfield::before {
  content: "+423";
}

.ui-wrapper input#Lithuania:checked~.input-wrapper .textfield::before {
  content: "+370";
}

.ui-wrapper input#Luxembourg:checked~.input-wrapper .textfield::before {
  content: "+352";
}

.ui-wrapper input#Malta:checked~.input-wrapper .textfield::before {
  content: "+356";
}

.ui-wrapper input#Netherlands:checked~.input-wrapper .textfield::before {
  content: "+31";
}

.ui-wrapper input#Norway:checked~.input-wrapper .textfield::before {
  content: "+47";
}

.ui-wrapper input#Poland:checked~.input-wrapper .textfield::before {
  content: "+48";
}

.ui-wrapper input#Portugal:checked~.input-wrapper .textfield::before {
  content: "+351";
}

.ui-wrapper input#Romania:checked~.input-wrapper .textfield::before {
  content: "+40";
}

.ui-wrapper input#Slovakia:checked~.input-wrapper .textfield::before {
  content: "+421";
}

.ui-wrapper input#Slovenia:checked~.input-wrapper .textfield::before {
  content: "+386";
}

.ui-wrapper input#Spain:checked~.input-wrapper .textfield::before {
  content: "+34";
}

.ui-wrapper input#Sweden:checked~.input-wrapper .textfield::before {
  content: "+46";
}
</style>
