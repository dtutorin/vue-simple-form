<template>
    <button class="button" type="button" role="button"
        :class="type"
        :disabled="disabled"
        @click="callback($event)"
         >
        <slot></slot>
    </button>
</template>

<script>
    export default {
        props: {
            type: String,
            disabled: Boolean
        },
        methods: {
            callback: function(e) {
                this.$emit('click', e);
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import '../../styles/common/index.scss';
    .button {
        display: block;
        position: relative;
        padding: 0 29px;
        font-size: $f-size-xs;
        font-family: $f-primary;
        font-weight: 500;
        color: $c-text-d;
        background: none;
        text-transform: uppercase;
        @include border-element();
        cursor: pointer;
         &::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background-color:$c-white;
            transition: transform $duration;
            transform: translate3d(0, 0, 0);
            transform-origin: right center;
        }
        &::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background-color: $c-gray-l;
            transition: transform $duration;
            transform: translate3d(0, 0, 0) scale(0, 1);
            transform-origin: right center;
        }
        &:hover,
        &:active {
            &::after {
                transform-origin: left center;
                transform: translate3d(0, 0, 0);
            }
        }

        span {
            color: $c-gray;
        }

        &[disabled]{
            cursor: not-allowed;
        }
        // For presentation only
        &.danger {
            border: 2px solid $c-danger;
            color: $c-white;
            transition: all $duration;
            &:hover,
            &:active,
            &:focus {
                transition: all $duration;
                border: 2px solid darken($c-danger, 10%);
            }
            &::before {
                background-color: $c-danger;
            }
            &::after {
                 background: darken($c-danger, 10%);
            }
        }
    }
</style>
