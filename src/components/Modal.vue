<template>
  <!-- 
    Teleport is like Portal in React. Here we are "teleporting" the 
    modal to the body element. 'to' attribute can be any selector,
    like ".modal-container". 

    We can also use other directives on teleport, like 'v-if' etc.
  -->

  <teleport to="body">
    <!-- 
      @click.xxxx is how we apply event modifiers. 
      '.self' means the click event doesn't apply to any child elements and only the element it's on (prevent event bubbling)
    -->

    <div class="backdrop" @click.self="closeModal">
      <div class="modal" :class="{ sale: theme === 'sale' }">
        <h1>{{ title }}</h1>
        <p>{{ bodyText }}</p>
        <img v-if="showVueLogo" alt="Vue logo" src="../assets/logo.png">

        <!-- 'slots' are like props.children in React. -->
        <slot>
          <div>
            Default content for this slot in case no slot is passed in.
          </div>
        </slot>
        
        <button @click.alt="closeModal">Close (ALT + Click)</button>

        <!-- Named slot to place slot wherever you want. -->
        <div class="namedSlotContent">
          <slot name="namedSlot"></slot>
        </div>
      </div>
    </div>
  </teleport>
</template>

<script>
export default {
  name: 'Modal',
  props: [
    'title',
    'bodyText',
    'showVueLogo',
    'theme'
  ],
  methods: {
    closeModal() {
      //Custom event to close modal so that the parent app can update
      //Emit custom event named closeModal.
      this.$emit('closeModal');
    }
  }
}
</script>

// Adding scoped attribute will scope the styles to this component only
<style scoped>
  .modal {
    width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: paleturquoise;
    border-radius: 10px;
  }

  .backdrop {
    position: fixed;
    top: 0;
    background: rgba(0, 0, 0, 0.4);
    width: 100%;
    height: 100%;
  }

  h1 {
    color: yellow;
  }

  .modal.sale {
    background-color: lightgreen; 
  }

  .namedSlotContent {
    font-weight: 700;
  }
</style>