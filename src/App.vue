<template>
  <div>
    <div>
      <label for="">Pesquise aqui: </label>
      <input type="text" name="name" id="name" v-model="search">
    </div>

    <div>
      <label for="">Pesquise o genero aqui </label>
      <select id="genero" name="genero" v-model="selected">
        <option value="">Selecione a opção</option>
        <option value="">Todos</option>
        <option value='Male'>Masculino</option>
        <option value="Female">Feminino</option>
        <option value="Genderfluid">Genero Fluido</option>
        <option value="Polygender">Poligênero</option>
      </select>

    </div>

    <div class="tete">
      <table>
        <thead>
          <tr>
            <td>ID</td>
            <td>NOME</td>
            <td>SOBRENOME</td>
            <td>MOEDA</td>
            <td>GENERO</td>
          </tr>
        </thead>

        <tbody>
          <tr v-for="dados in filtrarInput" :key="dados.id">
            <td>{{ dados.id }}</td>
            <td>{{ dados.primeiroNome }}</td>
            <td>{{ dados.sobreNome }}</td>
            <td>{{ dados.moeda }}</td>
            <td>{{ dados.genero }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {

  data() {
    return {
      banco: [],
      search: "",
      selected: ""
    }
  },

  mounted() {
    axios.get('http://localhost:3000/profiles').then((res) => {
      console.log(res.data)
      this.banco = res.data
    }).catch((err) => {
      console.log(err)
    })
  },

  computed: {
    filtrarInput() {
      if (this.selected == 'Male') {
        return this.banco.filter((dados) => dados.genero.includes(this.selected))
      } else if (this.selected == 'Female') {
        return this.banco.filter((dados) => dados.genero.includes(this.selected))
      } else if (this.selected == 'Genderfluid') {
        return this.banco.filter((dados) => dados.genero.includes(this.selected))
      } else if (this.selected == 'Polygender') {
        return this.banco.filter((dados) => dados.genero.includes(this.selected))
      } else {

        return this.banco.filter((dados) =>
          dados.primeiroNome.includes(this.search) ||
          dados.sobreNome.includes(this.search) ||
          dados.moeda.includes(this.search)
        )
      }

    }


  },



}
</script>

