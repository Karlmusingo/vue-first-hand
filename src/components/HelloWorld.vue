<template>
  <div class="hello">
    <div>{{msg}}</div>

    <div class="input-form">
      <input
        v-model="values.input1"
        type="number"
        name="percentage1"
        id="percentage1"
        min="0"
        max="100"
      />
    </div>
    <div class="input-form">
      <input
        v-model="values.input2"
        type="number"
        name="percentage2"
        id="percentage2"
        min="0"
        max="100"
      />
    </div>
    <div class="input-form">
      <input
        v-model="values.input3"
        type="number"
        name="percentage3"
        id="percentage2"
        min="0"
        max="100"
      />
    </div>
    <span>Total: {{total}}</span>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      values: {
        input1: 100,
        input2: 0,
        input3: 0
      },
      total: 100
    }
  },
  methods: {
    // changeInput3: () => {
    //   this.input3 = this.input2
    // }
  },
  // computed: {
  //   propertyComputed: () => {
  //     console.log('I change when this.property changes.')
  //     return this.values
  //   }
  // },
  watch: {
    values: {
      handler: function (val, oldVal) {
        const valKeys = Object.keys(val)

        let total =
          parseInt(val.input1) + parseInt(val.input2) + parseInt(val.input3)

        if (total > 100) {
          const diff = total - 100
          let greaterKey = valKeys[0]
          let greaterVal = val.input1
          for (const input in val) {
            if (val.hasOwnProperty(input)) {
              const inputValue = val[input]
              if (inputValue > greaterVal) {
                greaterVal = inputValue
                greaterKey = input
              }
            }
          }
          this.values[greaterKey] = this.values[greaterKey] - diff
        } else {
          const diff = 100 - total
          let smallerKey = valKeys[0]
          let smallerVal = val.input1
          for (const input in val) {
            if (val.hasOwnProperty(input)) {
              const inputValue = val[input]
              if (inputValue < smallerVal) {
                smallerVal = inputValue
                smallerKey = input
              }
            }
          }
          this.values[smallerKey] = this.values[smallerKey] + diff
        }

        this.total = total
        // console.log(val, oldVal)
      },
      deep: true
    }
  },
  created () {
    this.property = 'Example property update.'
    console.log(
      'propertyComputed will update, as this.property is now reactive.'
    )
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.input-form {
  margin: 20px;
}
</style>
