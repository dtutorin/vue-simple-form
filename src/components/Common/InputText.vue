<template>
    <input
        class="input"
        type="url"
        :value="value"
        :required="required"
        v-on="inputListeners"
        >
</template>

<script>
    export default {
        props: {
            value: {
                type: String,
                default: ''
            },
            required: {
                type: Boolean,
                default: false
            }
        },
        computed: {
            inputListeners: function () {
                return {
                    ...this.$listeners,
                    input: event => this.$emit('input', event.target.value)
                }
            }
        },
        data () {
          return {
          }
        }
    }
</script>

<style lang="scss" scoped>
    @import '../../styles/common/index.scss';

    .input {
        @include input-style();
    }
</style>
