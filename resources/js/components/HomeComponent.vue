<template>
    <div class="container">
        <div class="row">
            <div class="col-lg-12">
                <h1>Test Project [Mail Merge]</h1>
            </div>
        </div>
        <div class="row">
            <div class="col-lg-12">
                <b-form-group label="Import your CSV file" label-for="file-small" label-cols-sm="2" label-size="sm">
                  <b-form-file id="file-small" size="sm" @change="onChange"></b-form-file>
                </b-form-group>
            </div>
            <div class="col-6">

            </div>
            <div class="col-6">
                <template-component></template-component>
            </div>
        </div>
    </div>
</template>

<script>

export default {
  data() {
    return {
      file: null,
      parse_csv: [],
      parse_header: [],
      sortOrders: {},
    }
  },
  methods: {
    onChange(event) {
        this.file = event.target.files ? event.target.files[0] : null
        let vm = this
        let reader = new FileReader()
        reader.readAsText(this.file)
        reader.onload = function(event) {
          let csv = event.target.result;
          vm.parse_csv = vm.csvJSON(csv)
        };
        reader.onerror = function(evt) {
          if(evt.target.error.name == "NotReadableError") {
            alert("Canno't read file !");
          }
        }
    },

    csvJSON(csv){
      let vm = this
      let lines = csv.split("\n")
      let result = []
      let headers = lines[0].split(",")
      vm.parse_header = lines[0].split(",")
      lines[0].split(",").forEach(function (key) {
        vm.sortOrders[key] = 1
      })

      lines.map(function(line, indexLine){
        if (indexLine < 1) return // Jump header line

        let obj = {}
        let currentline = line.split(",")

        headers.map(function(header, indexHeader){
          obj[header] = currentline[indexHeader]
        })

        result.push(obj)
      })

      result.pop() // remove the last item because undefined values

      return result // JavaScript object
    },
  }
}
</script>

<style>

</style>
