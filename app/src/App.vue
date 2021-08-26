<template>
  <main id="app" class="bg-light">
    <div id="sliders" class="w-50">

      <div class="form-group w-100">
        <label for="range-1">
          Horário selecionado: {{ tratarHorario(data) }}
        </label>
        <input type="range" 
          id="range-1" class="form-control" 
          min="0" max="1439" step="1" 
          v-model="data">
      </div>

      <div class="form-group w-100">
        <div class="custom-range-1">
          <div class="sliderValue">
            <span>{{ tratarHorario(data) }}</span>
          </div>
          <div class="field">
            <input type="range" 
              min="0" max="1439" step="1" 
              v-model="data" 
              @input="updateSliderPosition" @blur="removePointer">
          </div>
        </div>
      </div>

    </div>
  </main>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    data: 0
  }),
  methods: {
    tratarHorario(horario) {
      let horas = Math.floor(horario / 60)
      let minutos = Math.floor(horario % 60)
      return `${this.pad(horas)}:${this.pad(minutos)}`
    },
    pad(n) {
      return (n >= 0 && n < 10) ? `0${n}` : n.toString()
    },
    updateSliderPosition() {
      const sliderValue = document.querySelector('.sliderValue span')
      sliderValue.style.left = ((this.data / 1439) * 100) + '%';
      sliderValue.classList.add('show')
    },
    removePointer() {
      const sliderValue = document.querySelector('.sliderValue span')
      sliderValue.classList.remove('show')
    }
  }
}
</script>

<style lang="scss">

#app {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}

.custom-range-1 {
  display: block;
  width: 100%;
  height: 80px;
  background: #FFF;
  border-radius: 10px;
  text-align: center;
  padding: 0 50px 0 50px;
  min-width: 400px;

  .sliderValue {
    position: relative;
    width: 100%;

    span {
      position: absolute;
      height: 55px;
      width: 55px;
      color: #FFF;
      font-weight: 500;
      top: -40px;
      transform: translateX(-50%) scale(0);
      transform-origin: bottom;
      transition: transform 0.3s ease-in-out;
      line-height: 55px;
      z-index: 2;

      &.show {
        transform: translateX(-50%) scale(1);
      }

      &:after {
        position: absolute;
        content: '';
        height: 55px;
        width: 55px;
        background: #664AFF;
        left: 50%;
        transform: translateX(-50%) rotate(45deg);
        border: 3px solid #FFF;
        border-top-left-radius: 50%;
        border-top-right-radius: 50%;
        border-bottom-left-radius: 50%;
        z-index: -1;
      }
    }
  }

  .field {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;

    input {
      -webkit-appearance: none;
      height: 3px;
      width: 100%;
      background: #DDD;
      border-radius: 5px;
      outline: none;
      border: none;

      &::-webkit-slider-thumb {
        -webkit-appearance: none;
        height: 20px;
        width: 20px;
        background: #664AFF;
        border-radius: 50%;
        cursor: pointer;
      }
    }
  }
}

</style>
