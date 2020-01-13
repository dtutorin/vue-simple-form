<template>
<transition name="fade" appear>
  <div class="campaign__rules-item">
    <button class="button-remove" @click="$emit('remove', rule.id)"> 
      ✕
    </button>
    <p class="campaign__rules-label">Type a ful or partial url where you would like to display notifications.</p>
    <form class="campaign__rules-item-form" 
          novalidate="true"
      >
      <div class="campaign__rules-item-left">
        <select class="select" v-model="conformity">
          <option v-for="option in options" v-bind:key="option.value">
              {{ option.text }}
          </option>
        </select>

      </div>
      <div class="campaign__rules-item-right">
        <InputText 
          placeholder="Display URL"
          required
          v-model="newURL"
          v-on:input="$emit('inputText', newURL)"
        />
        <transition name="fade">
          <div v-if="!isValid" class="error-note">
            <span>{{ errors}}</span>
          </div>
        </transition>  
      </div>      
    </form>
  </div>
</transition>  
</template>

<script>
	import InputText from './Common/InputText.vue'
  export default {
    components: {
			InputText
    },
    props: {
      isValid: {
        type: Boolean,
        default: false
      },
      rule: {
        type: Object,
        required: true
      },
      errors: {
        type: String,
        text: 'URL is Missing'
      }
    },
		data () {
      return {
        newURL: '',
        conformity: 'Contains',
        options: [
          { 
            text: 'Contains', 
            value: '1' 
          },
          { 
            text: 'Exact Match', 
            value: '2' 
          }
        ]
      }
    },

  }
</script>

<style lang="scss" scoped>
  @import '../styles/common/index.scss';
  
  .campaign {
    &__rules{
      &-item {
        @include border();
        @include b-round();
        box-shadow: 3px 3px 0px 1px $c-blue-l;
        margin-bottom: 1.5rem;
        padding: 20px 30px;
        position: relative;
        .button-remove {
          position: absolute;
          top: 9px;
          right: 9px;
          width: 20px;
          height: 20px;
          font-size: $f-size-xs;
          font-weight: 900;
          display: block;
          @include b-round(50%);
          @include border(2px, $c-gray);
          text-align: center;
          line-height: 18px;
          color: $c-gray;
          cursor: pointer;
          transition: all $duration;
            &:hover,
            &:active,
            &:focus {
              @include border(2px, $c-danger);
              color: $c-danger;
            }

        }
        select {
          &.select {
            @include input-style();
          }
        }
        &-form {
          display: flex;
          flex-direction: row;
          flex-wrap: nowrap;
          justify-content: space-between;
            @media screen and (max-width: 600px) {
              flex-direction: column;
              flex-wrap: wrap;
            }
          }
        &-left {
          flex: 1 2 30%;
          margin-right: 30px;
            @media screen and (max-width: 600px) {
              flex: 1 1 100%;
              margin-right: 0;
              margin-bottom: 1rem;
            }
        }
        &-right {
          flex: 1 1 70%;
            @media screen and (max-width: 600px) {
              flex: 1 1 100%;
            }
        }
      }
      &-label{
        margin-bottom: 1rem;
      }
    } 
  }

</style>