// Template
// In Vue 3.0 you can have multiple root elements in the template. Used to be you'd need to have 1 root element like a wrapping div (like in React, although in React you can use a fragment.)
<template>
  <h1>Hi! \o/</h1>
  <h2>{{ title }}</h2>

  <input type="text" ref="forename" />
  <button @click="handleFieldButtonClick">Click me</button>

  <!--
    You can pass strings as props by directly adding them as attribute 
    values (see title).

    You can also pass other data types by data binding the attributes 
    using `:` (see bodyText).

    @closeModal is a listener for a custom event being emitted from the Modal component to close the modal
  -->

  <div v-if="showModal">
    <Modal 
      title="Yo!" 
      :bodyText="modalText"
      :theme="modalTheme"
      :showVueLogo="true"
      @closeModal="toggleModal" 
    >
      <div>
        <h3>Slot content</h3>
        <p>My extra content goes here and can be shown using slots. Like props.children in react</p>
      </div>
      <template v-slot:namedSlot>
        <p>More slot content which has been placed in a specific place using a named slot.</p>
      </template>
    </Modal>
  </div>

  <div v-if="showModalTwo">
    <Modal 
      title="Modal 2" 
      bodyText="Another modal!"
      :theme="modalTheme"
      :showVueLogo="true"
      @closeModal="toggleModalTwo" 
    >
      <div>
        <h3>Second modal</h3>
        <input type="password" />
      </div>
    </Modal>
  </div>

  <button @click="toggleModal">Open Modal</button>
  <button @click="toggleModalTwo">Open Modal 2</button>
</template>

<script>
import Modal from './components/Modal.vue';

export default {
  name: 'App', //name is optional but recommended
  data() {
    return {
      title: 'Hello! o/',
      modalText: 'Yes!! it worksss!!',
      modalTheme: 'sale',
      showModal: false,
      showModalTwo: false
    }
  },
  methods: {
    handleFieldButtonClick() {
      this.$refs.forename.classList.add('active');
      this.$refs.forename.focus();
      console.log(this.$refs.forename.value);
    },
    toggleModal() {
      this.showModal = !this.showModal;
    },
    toggleModalTwo() {
      this.showModalTwo = !this.showModalTwo;
    }
  },
  // any components you are importing and using in the component go here. This is where we register the components.
  components: { 
    Modal
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  border-bottom: 2px dashed skyblue;
  display: inline-block;
}

.active {
  background-color: lightyellow;
}
</style>
