<template>

  <div class = "wrapper">

    <div class="odometer">
      <Honeycomb :stopNumber = "stopNumber" :status = "status" delay = "0" />
    </div>

    <div class = "form">

      <input
        v-model = "stopNumber"
        type = "tel"
        class = "input"
        placeholder = "Должно выпасть.." />

      <button
        class = "button"
        :class = "{ 'error': !stopNumber || stopNumber < 0 || stopNumber > 9, 'loading': status == 'start' }"
        @click = "start()">Старт</button>

    </div>

  </div>

</template>

<script>
import Honeycomb from '~/components/Honeycomb.vue'

export default {
  components: {
    Honeycomb
  },
  data: function() {
    return {
      stopNumber: undefined,
      status: undefined
    }
  },
  methods: {

    start: function () {
      this.$set(this, 'status', 'start');

      setTimeout(() => {
        this.$set(this, 'status', undefined);
      }, 2000);
    }

  }
}
</script>

<style>

.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background: rgb(46, 28, 76);
  width: 100vw;
  height: 100vh;
}

.odometer {
  display: flex;
  align-items: center;
  justify-content: center;
}

.odometer > * {
  margin-right: 15px;
}

.odometer > *:last-child {
  margin-right: 0;
}

.form {
  display: flex;
  align-items: stretch;
  justify-content: center;
  margin-top: 20px;
}

.input,
.button {
  border: 0;
  padding: 10px;
}

.input {
  background: #fff;
  border-radius: 5px 0 0 5px;
}

.button {
  background: rgb(133, 171, 104);
  border-radius: 0 5px 5px 0;
  cursor: pointer;
  color: #fff;
}

.button:not(.error):hover {
  background: rgb(116, 191, 46);
}

.button.error {
  background: rgb(205, 83, 84);
  pointer-events: none;
}

.button.loading {
  opacity: .8;
  pointer-events: none;
}

</style>
