<template>
  <div class="about">
    <h1>Try</h1>
    <div>
    <label class="typo__label">Tagging</label>
    <multiselect v-model="value" tag-placeholder="Add this as new tag" placeholder="Search or add a tag" label="name" track-by="code" :options="options" :multiple="true" :taggable="true" @tag="addTag"></multiselect>
    <pre class="language-json"><code>{{ value  }}</code></pre>
  </div>
  </div>
</template>

<script>
//https://vue-multiselect.js.org/
//官方文件

import MultiSelectFunc from '../../src/components/multiSelect.js';
export default {

 // Vue.component('vue-multiselect', window.VueMultiselect.default);
  components: {
    Multiselect
  },
  data () {
    return {
      value: [
        { name: 'Javascript', code: 'js' }
      ],
      options: [
        { name: 'Vue.js', code: 'vu' },
        { name: 'Javascript', code: 'js' },
        { name: 'Open Source', code: 'os' }
      ]
    }
  },
  methods: {
    addTag (newTag) {
      const tag = {
        name: newTag,
        code: newTag.substring(0, 2) + Math.floor((Math.random() * 10000000))
      }
      this.options.push(tag)
      this.value.push(tag)
    }
  },
  created(){
    MultiSelectFunc();
  }
}

</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
  div{
    flex-wrap: wrap;
  }
}
</style>
