<template>
  <div>
    <page-header/>
    <p> Modal dialog with activator</p>

    <b-modal close-btn size="xs" title="My title" @click:outside="showModal = false">
      <template slot="title" slot-scope="scope">{{scope.title}} {{scope.visible}}</template>
      <template #footer="scope">
        <button class="btn btn-primary" @click="scope.close">Close</button>
      </template>
        Modal with activator
      <template #activator="{on}">
        <button class="btn btn-primary" @click="on">Open</button>
      </template>
    </b-modal>
    <hr>
    <p> Modal dialog with model</p>
    <b-modal v-model="showModal" close-btn size="xs" title="My title" @click:outside="showModal = false">
      Modal with model
    </b-modal>

    <button type="button" class="btn btn-primary" @click="showModal = !showModal">
      Launch demo modal
    </button>

    <hr>

    <p> Alert with activator</p>

    <b-alert
        type="info"
        :hideMessage="false"
        :automaticallyCloseAfterSomeTime="true"
        @alert-opened="alertWithActivatorOpened"
        @alert-closed="alertWithActivatorClosed"
    >
      <template #activator="{open}">
        <button class="btn btn-primary" @click="open">Open</button>
      </template>
      <template #default>
        Custom alert content goes here.
      </template>
    </b-alert>

    <hr>

    <p> Modal alert with model</p>
    <b-alert
        v-model="showAlert"
        type="danger"
        :hideMessage="false"
        :automaticallyCloseAfterSomeTime="true"
        :displayTimeBeforeAutomaticClosing="4000"
        @click="showAlert = !showAlert"
        @alert-opened="alertWithModelOpened"
        @alert-closed="alertWithModelClosed"
    />

    <button type="button" class="btn btn-primary" @click="showAlert = !showAlert">
      {{ toggleAlertBtnText }}
    </button>
  </div>
</template>

<script>
  import BModal from "../../components/bootstrap/BModal";
  import PageHeader from "./PageHeader";
  import BAlert from "@/components/bootstrap/BAlert";

  export default {
    name: "Home",
    components: {BAlert, PageHeader, BModal},
    data() {
      return {
        showModal: false,
        showAlert: false
      }
    },
    methods: {
      alertWithActivatorOpened() {
        console.log("alert with activator is opened")
      },
      alertWithActivatorClosed() {
        console.log("alert with activator is closed")
      },
      alertWithModelOpened() {
        console.log("alert with model is opened")
      },
      alertWithModelClosed() {
        console.log("alert with model is closed")
      }
    },
    computed: {
      toggleAlertBtnText() {
        return this.showAlert ? "Hide alert" : "Show alert";
      },
    }
  }
</script>

