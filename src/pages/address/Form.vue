<template>
  <form @submit.prevent="handleSubmit(item)">
    <v-layout wrap>
      <v-flex xs12>
        <item-errors entity="address" />
      </v-flex>

      <v-flex md6 px-2>
        <form-select
          :item="item"
          :errors="errors"
          property="country"
          option-store="country"
          label="country"
          @formUpdated="updateValue"
        />
        <form-select
          :item="item"
          :errors="errors"
          property="city"
          option-store="city"
          label="city"
          @formUpdated="updateValue"
        />
        <form-input
          :item="item"
          :errors="errors"
          property="region"
          label="region"
          @formUpdated="updateValue"
        />
        <form-input
          :item="item"
          :errors="errors"
          property="district"
          label="district"
          @formUpdated="updateValue"
        />
      </v-flex>
      <v-flex md6 px-2>
        <form-input
          :item="item"
          :errors="errors"
          property="postCode"
          label="postCode"
          @formUpdated="updateValue"
        />
        <form-input
          :item="item"
          :errors="errors"
          property="street"
          label="street"
          @formUpdated="updateValue"
        />
        <form-input
          :item="item"
          :errors="errors"
          property="building"
          label="building"
          @formUpdated="updateValue"
        />
        <form-input
          :item="item"
          :errors="errors"
          property="apartment"
          label="apartment"
          @formUpdated="updateValue"
        />
      </v-flex>
      <v-flex xs12 px-2>
        <form-textarea
          :item="item"
          :errors="errors"
          property="comment"
          label="comment"
          @formUpdated="updateValue"
        />
      </v-flex>
      <v-flex xs12 px-2>
        <form-checkbox
          :item="item"
          :errors="errors"
          property="isActive"
          label="isActive"
          @formUpdated="updateValue"
        />
      </v-flex>

      <item-edit-actions
        v-if="showActions"
        :item="item"
        entity="Address"
        path="address"
      />
    </v-layout>
  </form>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
import ItemEditActions from '../../components/layout/ItemEditActions'
import ItemErrors from '../../components/layout/errors/ItemErrors'

export default {
  components: {
    ItemErrors,
    ItemEditActions
  },
  props: {
    handleSubmit: {
      type: Function,
      required: true
    },
    item: {
      type: Object,
      required: true
    },
    showActions: {
      type: Boolean,
      default() {
        return true
      }
    }
  },
  computed: {
    ...mapGetters({
      errors: 'address/errors'
    })
  },
  beforeDestroy() {
    this.reset()
  },
  methods: {
    ...mapActions({
      reset: 'address/reset'
    }),
    updateValue(property, value) {
      this.$store.commit('address/ADDRESS_UPDATE_ITEM', { [property]: value })
    }
  }
}
</script>
