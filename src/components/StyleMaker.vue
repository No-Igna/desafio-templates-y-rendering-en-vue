<template>
  <div class="container my-5">
    <div class="row g-5">
      <div class="col-12 col-md-6 py-3 formulario">
        <form>
          <!-- color de fondo -->
          <div class="mb-3">
            <label for="colorFondo" class="form-label">Color de fondo</label>
            <input type="text" class="form-control" v-model="colorFondo">
          </div>
          <!-- color de texto -->
          <div class="mb-3">
            <label for="colorTexto" class="form-label">Color de texto</label>
            <input type="text" class="form-control" v-model="colorTexto">
          </div>
          <!-- mostrar texto -->
          <div class="mb-3">
            <label class="form-check-label me-3" for="exampleCheck1">Mostrar Texto</label>
            <input type="checkbox" class="form-check-input" v-model="mostrarTexto">
          </div>
          <!-- borde -->
          <div class="mb-3">
            <label for="customRange2" class="form-label">Borde: {{ borde + '%' }}</label>
            <input type="range" class="form-range" min="0" max="50" v-model="borde">
          </div>
          <!-- contenido textual -->
          <div class="mb-3">
            <label for="contenidoTextual" class="form-label">Contenido Textual</label>
            <textarea class="form-control mb-3" v-model="contenidoTextual"></textarea>
          </div>
          <!-- tipografia -->
          <div class="mb-3">
            <label for="tipografia" class="form-label">Tipografia {{ fuente }}</label>
            <select class="form-select" v-model="fuente">
              <option value="" selected disabled>Elija un tipo de fuente</option>
              <option v-for="letra in tipografia" :value="letra">{{ letra }}</option>
            </select>
          </div>
          <!-- opaco -->
          <div class="mb-3">
            <label class="form-check-label me-3">Opaco</label>
            <input type="checkbox" class="form-check-input" v-model="opaco">
          </div>
          <!-- tamaño de letra -->
          <div class="mb-3">
            <label>Tamaño de letra</label>
            <div>
              <label v-for="(valor,clave) in fontSize" >
                <input class="mx-2" type="radio" v-model="seleccionado" @change="updateSizes(clave)" :value="clave" />
                {{ clave }}
              </label>
            </div>
          </div>
        </form>
      </div>
      <div class="col-12 col-md-6 ">
        <div :class="{
          opacidad: opaco,
          box: true,
        }" :style="{
          backgroundColor: colorFondo,
          color: colorTexto,
          borderRadius: borde + '%'
        }">
          <p v-show="mostrarTexto" :class="seleccionado + ' parrafo'"  :style="{ fontFamily: fuente }">{{ contenidoTextual }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'StyleMaker',
  data() {
    return {
      colorFondo: '',
      colorTexto: '',
      mostrarTexto: false,
      borde: 0,
      contenidoTextual: '',
      tipografia: ['Arial', '"courier new"', '"time new roman"'],
      fuente: '',
      opaco: false,
      fontSize: {
        pequeno: false,
        mediano: false,
        grande: false
      },
      seleccionado: null
    };
  },
  methods: {
    actualizarFontSize(size) {
      Object.keys(this.fontSize).forEach(key => {
        this.sizes[key] = (key === size);
      });

    }
  }
};
</script>

<style scoped>
.formulario{
  border-radius: 5%;
  background-color: #ccc;
  box-shadow: 3px 6px #777;
}
.box {
  width: 90%;
  height: 90%;
  display: flex;
  border: 1px solid black;
  align-items: center;
  justify-content: center;
}

.opacidad {
  opacity: 0.5;
}
.parrafo{
  overflow: auto;      /* Agrega scroll si el contenido se desborda */
  word-wrap: break-word;
}
.pequeno{
  font-size: 1rem;
}
.mediano{
  font-size: 2rem;
}
.grande{
  font-size: 4rem;
}
</style>