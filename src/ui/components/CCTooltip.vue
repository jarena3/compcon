<template>
  <v-tooltip
    :top="isTop"
    :bottom="bottom"
    :left="left"
    :right="right"
    content-class="cc-tooltip"
    :open-delay="delayed ? 500 : 150"
  >
    <template v-slot:activator="{ on }">
      <div :class="{ 'd-inline': inline }" v-on="on">
        <slot />
      </div>
    </template>
    <span v-if="err">
      Unable to load tooltip information. This may be due to malformed data or an unloaded content
      package.
    </span>
    <div v-else>
      <div v-if="simple">
        <p class="body-text stark--text mb-0" v-html="content" />
      </div>
      <div v-else>
        <span v-if="title" class="heading h3 stark--text">{{ title }}</span>
        <v-divider v-if="title" class="my-1" />
        <p class="body-text stark--text pb-0 mb-0" v-html="content" />
      </div>
    </div>
  </v-tooltip>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'

@Component({ name: 'cc-tooltip' })
export default class CCTooltip extends Vue {
  @Prop({ type: String, required: false, default: '' })
  readonly err: string

  @Prop({ type: Boolean, required: false })
  readonly simple?: boolean

  @Prop({ type: Boolean, required: false })
  readonly top?: boolean

  @Prop({ type: Boolean, required: false })
  readonly bottom?: boolean

  @Prop({ type: Boolean, required: false })
  readonly left?: boolean

  @Prop({ type: Boolean, required: false })
  readonly right?: boolean

  @Prop({ type: Boolean, required: false })
  readonly inline?: boolean

  @Prop({ type: Boolean, required: false })
  readonly delayed?: boolean

  @Prop({ type: String, required: false, default: '' })
  readonly title: string

  @Prop({ type: String, required: true })
  readonly content!: string

  get isTop(): boolean {
    if (this.top) return true
    return !this.bottom && !this.left && !this.right
  }
}
</script>

<style scoped>
.cc-tooltip {
  background: var(--v-tooltip-base) !important;
  background-color: var(--v-tooltip-base) !important;
  opacity: 1 !important;
  max-width: 50vw;
  border: 1px var(--v-active-base) solid;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
