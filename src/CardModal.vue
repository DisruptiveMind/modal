<template>
  <transition
    :name="transition"
    mode="in-out"
    appear
    :appear-active-class="enterClass"
    :enter-active-class="enterClass"
    :leave-active-class="leaveClass"
    @beforeEnter="beforeEnter"
    @afterEnter="afterEnter"
    @beforeLeave="beforeLeave"
    @afterLeave="afterLeave"
  >
    <div :class="classes" v-if="show">
      <div class="modal-background" @click="deactive"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">{{ title }}</p>
          <button class="delete" @click="deactive"></button>
        </header>
        <section class="modal-card-body">
          <slot>{{content}}<div v-html="contentHtml"></div></slot>
        </section>
        <footer class="modal-card-foot">
          <!--<slot name="footer">-->
            <a class="button is-primary" @click="ok">{{ okText }}</a>
            <a class="button" @click="cancel">{{ cancelText }}</a>
          <!--</slot>-->
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
import BaseModal from './BaseModal'

export default {
  mixins: [BaseModal],

  props: {
    title: {
      type: String
    },
    okText: {
      type: String,
      default: 'Ok'
    },
    cancelText: {
      type: String,
      default: 'Cancel'
    },
    content: {
      type: String
    },
    contentHtml: {
      type: String
    }
  },

  computed: {
    classes () {
      return ['modal', 'animated', 'is-active']
    }
  },

  methods: {
    ok () {
      this.$emit('ok')
    },

    cancel () {
      this.$emit('cancel')
    },

    afterEnter () {
      this.$emit('afterEnter')
    },

    beforeLeave () {
      this.$emit('beforeLeave')
    },
  }
}
</script>
