<template>
    <div v-for="item in userExp" :key="item">
        <div style="display: flex;">
            <label for="name">Company</label>
            <input v-model="item.company" type="text" id="name">
        </div>
        <div style="display: flex;">
            <label for="year">experince</label>
            <input v-model="item.exp" type="text" name="year">
        </div>
    </div>       <button @click="addExp()">add exp +</button>
    <div>{{ userExp }}</div>

</template>

<script>
export default {
  name: 'dynamicInput',
  methods: {
    addExp () {
      this.userExp.push({
        company: '',
        exp: ''
      })
    }
  },
  data () {
    return {
      userExp: [
        {
          company: '',
          exp: ''
        }
      ]
    }
  }

}

</script>

<style scoped>
</style>
