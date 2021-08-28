<template>
  <div>
    <div>
      <div class="text-xl ml-1">{{ pageTitle }}</div>
      <NuxtLink :to="`/${page}`" class="-ml-1 my-3 block">
        <md-button class="md-dense md-raised md-primary">Back</md-button>
      </NuxtLink>
    </div>
    <div class="mt-3">
      <md-field :class="messageClass">
        <label>Company</label>
        <md-input v-model="company" required></md-input>
        <span class="md-error">There is an error</span>
      </md-field>

      <md-field :class="messageClass">
        <label>VAT Number</label>
        <md-input v-model="vat" required></md-input>
        <span class="md-error">There is an error</span>
      </md-field>

      <md-field :class="messageClass">
        <label>Address</label>
        <md-textarea v-model="address" required></md-textarea>
        <span class="md-helper-text">Helper text</span>
        <span class="md-error">There is an error</span>
      </md-field>

      <md-switch v-model="hasMessages">{{ !hasMessages ? 'Show' : 'Hide' }} Errors</md-switch>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        page: "clients",
        pageTitle: "Create New Client",
        company: null,
        vat: null,
        address: null,
        hasMessages: false
      }
    },
    computed: {
      messageClass () {
        return {
          'md-invalid': this.hasMessages
        }
      }
    }
  }
</script>
