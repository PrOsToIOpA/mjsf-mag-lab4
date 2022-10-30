<template>
  <div>
    <slot name="activator" :open="open" />
    <div class="alert d-none" :class="alertClasses" role="alert">
      <template v-if="hideMessage">
        <p>Message is hidden</p>
      </template>
      <template v-else>
        <slot>
          A default alert content goes here.
        </slot>
      </template>
    </div>
  </div>
</template>

<script>
// @refs: https://getbootstrap.com/docs/5.2/components/alerts/
export default {
  name: "BAlert",
  model: {
    prop: 'visible',
    event: 'change'
  },
  props: {
    visible: {
      type: Boolean,
      default: false,
    },
    type: {
      type: String,
      default: 'primary'
    },
    hideMessage: {
      type: Boolean,
      default: false,
    },
    automaticallyCloseAfterSomeTime: {
      type: Boolean,
      default: true,
    },
    displayTimeBeforeAutomaticClosing: {
      type: Number,
      default: 2000, // in ms.
    }
  },
  data(){
    return {
      showAlert: this.visible,
      timer: null,
    }
  },
  watch: {
    visible(currentValue) {
      if (currentValue) {
        this.open();
      } else {
        this.showAlert = currentValue;
      }
    }
  },
  methods: {
    close() {
      this.showAlert = false;
      this.$emit("change", false);
      this.$emit("alert-closed");
      if (this.timer) {
        clearTimeout(this.timer);
      }
    },
    open() {
      this.showAlert = true;
      this.$emit("change", true)
      this.$emit("alert-opened");
      if (this.automaticallyCloseAfterSomeTime) {
        this.displaySpecificTime();
      }
    },
    displaySpecificTime() {
      //  Показывать определенноее время перед автоматическим закрытием.
     this.timer = setTimeout(() => {
        this.close();
      }, this.displayTimeBeforeAutomaticClosing)
    },
  },
  computed: {
    alertClasses() {
      return {
        'd-block': this.showAlert,
        [`alert-${this.type}`]: true
      }
    },
  }
}
</script>