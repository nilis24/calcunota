<template>
  <h1 class="text-3xl font-bold text-center my-5">Calcunota</h1>

  <div class="container mx-auto w-full max-w-lg">
    <div class="flex flex-wrap -mx-3 mb-6">
      <div class="w-full px-3">
        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="pond-esp-1">
            Estudis que has cursat
          </label>
          <div class="relative">
            <select @change="HideSeleGeneral" v-model="EstudisCursats" class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="pond-esp-1">
              <option>Batxillerat</option>
              <option>Batxibac</option>
              <option>CFGS</option>
            </select>
            <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
              <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
            </div>
          </div>
        </div>
    </div>


    <div class="flex flex-wrap -mx-3 mb-6">
      <div class="w-full px-3">
        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="nota-acces">
          Nota {{ EstudisCursats }}
        </label>
        <input min="0" max="10" step="0.01" :class="{ BorderError: NotaAccesHasError }" v-model="NotaAcces" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="nota-acces" type="number">
      </div>
      <p :class="{ hidden: !NotaAccesHasError }" class="text-red-500 text-xs italic ml-3">La nota ha d'estar entre 5 i 10</p>
    </div>


    <div :class="{ hidden: IsBatxiBacOrCFGS }" class="flex flex-wrap -mx-3 mb-6">
      <div class="w-full px-3">
        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="nota-sele-general">
          Nota selectivitat general
        </label>
        <input min="0" max="10" step="0.01" :class="{ BorderError: NotaSeleGeneralHasError }" v-model="NotaSeleGeneral" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="nota-sele-general" type="number">
      </div>
      <p :class="{ hidden: !NotaSeleGeneralHasError }" class="text-red-500 text-xs italic ml-3">La nota ha d'estar entre 5 i 10</p>
    </div>

    <div class="flex flex-wrap -mx-3 mb-6">
      <div class="w-full px-3">
        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="pond-esp-1">
            T'has examinat de les matèries especifiques?
          </label>
          <div class="relative">
            <select v-model="HasMadeSeleEsp" class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="pond-esp-1">
              <option :value="true">Sí</option>
              <option :value="false">No</option>
            </select>
            <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
              <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
            </div>
          </div>
        </div>
    </div>

    <div :class="{ hidden: !HasMadeSeleEsp}">
      <div class="flex flex-wrap -mx-3 mb-6">

        <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
          <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="pond-esp-1">
            ponderació especifica 1
          </label>
          <div class="relative">
            <select v-model="PondEsp1" class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="pond-esp-1">
              <option>0.1</option>
              <option>0.2</option>
            </select>
            <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
              <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
            </div>
          </div>
        </div>

        <div class="w-full md:w-1/2 px-3">
          <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="nota-esp-1">
            Nota especifica 1
          </label>
          <input min="0" max="10" step="0.5" :class="{ BorderError: NotaEsp1HasError }" v-model="NotaEsp1" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="nota-esp-1" type="number">
          <p :class="{ hidden: !NotaEsp1HasError }" class="text-red-500 text-xs italic ml-3">La nota ha d'estar entre 5 i 10</p>
        </div>
      </div>


      <div class="flex flex-wrap -mx-3 mb-6">

        <div class="w-full md:w-1/2 px-3 mb-6 md:mb-0">
          <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="pond-esp-2">
            ponderació especifica 2
          </label>
          <div class="relative">
            <select v-model="PondEsp2" class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="pond-esp-2">
              <option>0.1</option>
              <option>0.2</option>
            </select>
            <div class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700">
              <svg class="fill-current h-4 w-4" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"><path d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"/></svg>
            </div>
          </div>
        </div>

      <div class="w-full md:w-1/2 px-3">
        <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="nota-esp-2">
          Nota especifica 2
        </label>
        <input min="0" max="10" step="0.5" :class="{ BorderError: NotaEsp2HasError }" v-model="NotaEsp2" class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500" id="nota-esp-2" type="number">
        <p :class="{ hidden: !NotaEsp2HasError }" class="text-red-500 text-xs italic ml-3">La nota ha d'estar entre 5 i 10</p>
      </div>

      </div>
    </div>

    <div class="text-center">
      <button @click="CalcularNota" class="p-3 bg-cyan-500 hover:bg-cyan-600 text-white rounded">Calcular nota</button>
    </div>
  </div>

  <footer class="footer p-4 mt-2">
      <div class="text-center">
        <p>
          Fet amb &#10084; per Nilis24. Versió 1.0
        </p>
    </div>
  </footer>

</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      EstudisCursats: "Batxillerat",
      NotaAcces: "",
      NotaSeleGeneral: "",
      NotaEsp1: "",
      NotaEsp2: "",
      PondEsp1: 0.2,
      PondEsp2: 0.2,
      NotaAdmissio: 0,
      IsBatxiBacOrCFGS: false,
      NotaAccesHasError: false,
      NotaSeleGeneralHasError: false,
      NotaEsp1HasError: false,
      NotaEsp2HasError: false,
      HasMadeSeleEsp: true
    }
  },
  methods: {
    CalcularNota: function() {
      this.ShowErrors()
      switch(this.EstudisCursats) {
        case "Batxillerat":
          this.NotaAdmissio = (this.NotaAcces * 0.6) + (this.NotaSeleGeneral * 0.4) + (this.NotaEsp1 * this.PondEsp1) + (this.NotaEsp2 * this.PondEsp2)
          if(this.NotaAccesHasError === false && this.NotaSeleGeneralHasError === false && this.NotaEsp1HasError === false && this.NotaEsp2HasError === false) {
            alert("La teva nota és: " + this.NotaAdmissio + "/14")
            this.ResetValues()
          } else if(this.HasMadeSeleEsp === false) {
            alert("La teva nota és: " + this.NotaAdmissio + "/14")
            this.ResetValues()
          } else(
            alert("Hi ha errors en algunes notes, revisa-ho")
          )
          break;
        default:
          this.NotaAdmissio = this.NotaAcces + (this.NotaEsp1 * this.PondEsp1) + (this.NotaEsp2 * this.PondEsp2)
          if(this.NotaAccesHasError === false && this.NotaEsp1HasError === false && this.NotaEsp2HasError === false) {
            alert("La teva nota és: " + this.NotaAdmissio + "/14")
            this.ResetValues()
          } else if(this.HasMadeSeleEsp === false) {
            alert("La teva nota és: " + this.NotaAdmissio + "/14")
            this.ResetValues()
          } else {
            alert("Hi ha errors en algunes notes, revisa-ho")
          }
          break;
      }
    },
    HideSeleGeneral: function() {
      if(this.EstudisCursats === "CFGS" || this.EstudisCursats === "Batxibac") {
        this.IsBatxiBacOrCFGS = true
        this.ResetValues()
      } else {
        this.IsBatxiBacOrCFGS = false
        this.ResetValues()
      }
    },
    ShowErrors: function() {
      this.NotaAccesHasError = ((this.NotaAcces >= 5 && this.NotaAcces <= 10) ? false : true)
      this.NotaSeleGeneralHasError = ((this.NotaSeleGeneral >= 5 && this.NotaSeleGeneral <= 10) ? false : true)
      this.NotaEsp1HasError = ((this.NotaEsp1 >= 5 && this.NotaEsp1 <= 10) ? false : true)
      this.NotaEsp2HasError = ((this.NotaEsp2 >= 5 && this.NotaEsp2 <= 10) ? false : true)
    },
    ResetValues: function() {
      this.NotaAcces = ""
      this.NotaSeleGeneral = ""
      this.NotaEsp1 = ""
      this.NotaEsp2 = ""
      this.PondEsp1 = 0.2
      this.PondEsp2 = 0.2
      this.NotaAdmissio = 0
      this.NotaAccesHasError = false
      this.NotaSeleGeneralHasError = false
      this.NotaEsp1HasError = false
      this.NotaEsp2HasError = false
      this.HasMadeSeleEsp = true
    }
  }
}
</script>
