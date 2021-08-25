<template>
  <main id="app" class="bg-light">
    <div id="sliders" class="w-25">

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
        <label for="range-1">
          Horário selecionado: {{ tratarHorario(data) }}
        </label>
        <input type="range" 
          id="range-1" class="custom-range-1"
          min="0" max="1439" step="1" 
          v-model="data">
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
}

</style>
