<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-xs-12">
          <br>
          <navigation></navigation>
          <hr>
        </div>
      </div>
    </div>

    <router-view></router-view>
  </div>
</template>

<script>
  import Navigation from './Navigation.vue';

  export default {
    data() {
      return { }
    },
    methods: {
      directiveTest: () => {
        console.log('Hello! Directive is clicked!')
      }
    },
    components: {
      navigation: Navigation,
    },
    directives: {
      'local-highlight': {
        bind(el, binding, vnode) {
          console.log('hello 1')
          var delay = 0;
          if(binding.modifiers['delayed']) {
            delay = 3000;
          }

          if(binding.modifiers['blink']) {
            let mainColor = binding.value.mainColor;
            let secondColor = binding.value.secondColor;
            let currentColor = mainColor;
            setTimeout(() => {
              setInterval(() => {
                currentColor = currentColor === secondColor ? mainColor : secondColor;
                if(binding.arg === 'color') {
                  el.style.color = currentColor;
                }
              }, binding.value.delay);
            }, delay);
          } else {
            setTimeout(() => {
              if(binding.arg === 'color') {
                el.style.color = binding.value;
              }
            }, delay);
          }
        }
      },
      'myon': {
        bind(el, binding) {
          el.addEventListener(binding.arg, binding.value);
        }
      }
    }
  }
</script>

<style></style>
