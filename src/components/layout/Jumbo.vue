<template>
  <section :class="['hero', 'jumbo', { 'is-stars': stars }, { [`is-${size}`]: size }]">
    <div class="hero-head">
      <slot name="header" />
    </div>
    <div class="hero-body">
      <div class="container is-widescreen">
        <p class="is-size-8 has-text-uppercase has-text-centered has-text-weight-bold has-letter-spacing-xlarge">
          <template v-if="$slots.small">
            <slot name="small" />
          </template>
          <template v-else>
            {{ small }}
          </template>
        </p>
        <h1 :class="['is-size-1', 'has-text-centered', { [`into-${into}`]: into }]">
          <span v-if="into" />
          <span>
            <template v-if="$slots.title">
              <slot name="title" />
            </template>
            <template v-else>
              {{ title }}
            </template>
          </span>
          <span v-if="into" />
        </h1>
        <slot />
      </div>
    </div>
    <div class="hero-footer">
      <slot name="footer" />
    </div>
  </section>
</template>

<script>
export default {
  name: 'AJumbo',
  props: {
    /**
     * The title of the jumbo
     */
    title: {
      type: String,
      default: undefined
    },
    /**
     * The top description
     */
    small: {
      type: String,
      default: undefined
    },
    /** The outside character of the title
     *
     * possible values: `bracket, chevron, slash`
     */
    into: {
      type: String,
      default: undefined,
      validator: v => ['bracket', 'chevron', 'hash', 'slash'].includes(v)
    },
    /**
     * Sets the stars background
     */
    stars: {
      type: Boolean,
      default: true
    },
    size: {
      type: String,
      default: undefined,
      validator: v => ['medium', 'large', 'fullheight'].includes(v)
    }
  }
}
</script>

<docs>
### Playground

```jsx
<div>
  <a-jumbo size="fullheight" into="bracket" small="developer marketplace runtime">
    <a-navbar slot="header" dark :items="[{ name: 'Blog' }, { name: 'Documentation' }]" />
    <template slot="title">
      Asyncy amplifies <br /> the developer
    </template>
    <div class="columns is-centered is-desktop">
      <div class="column is-half">
        <a-form-beta />
      </div>
    </div>
    <div slot="footer" class="has-text-centered">
      <a-icon icon="separator" />
      <p class="has-text-weight-normal">Discover our mission to raise <br />any developer into a 10x developer.</p>
      <a-icon icon="arrow-down" stroke="white" />
    </div>
  </a-jumbo>
</div>
```
</docs>
