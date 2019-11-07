<template>
  <div class="GcInput">
    <div class="gc_input">
      <input :class="{err: err}" :type="type" :rules="rules" v-model="data" @blur="verify"/>
      <p>{{msg}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'GcInput',
  data () {
    return {
      data: '',
      msg: '',
      err: false
    }
  },
  props: {
    type: {
      type: String,
      required: true
    },
    rules: {
      type: Array,
      required: true
    },
    value: {}
  },
  watch: {
    data () {
      this.$emit('input', this.data)
    }
  },
  methods: {
    verify () {
      this.rules.forEach(d => {
        if (d.verify(this.data)) {
          this.err = true
          this.msg = d.msg
          return false
        } else {
          this.err = false
          this.msg = ''
        }
      })
    }
  }
}
</script>

<style scoped>
  .GcInput{
    display: flex;
    justify-content: center;
    align-items: center;
  }
  input{
    border-radius: 4px;
    width: 280px;
    height: 34px;
    line-height: 34px;
    border: 1px solid rgba(0, 0, 0, 0.2);
    font-size: 16px;
    padding: 0 15px;
    outline: none;
  }
  .err{
    border: 1px solid #f56c6c;
  }
  p{
    margin-top: 2px;
    color: #f56c6c;
    font-size: 14px;
  }
</style>