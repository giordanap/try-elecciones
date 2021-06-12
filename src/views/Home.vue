<template>
  <div class="home container">
    <table class="table table-hover">
      <thead>
        <tr>
          <th scope="col">Candidato</th>
          <th scope="col">Cantidad de Votos (al {{ toPercentageFormat(compute) }})</th>
          <th scope="col">% Votos</th>
          <th scope="col"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="candidate in candidates" :key="candidate.name">
            <th class="xpy-3" scope="row">{{ candidate.name }}</th>
            <td class="xpy-3">{{ toCommaFormat(candidate.numberOfVotes) }}</td>
            <td class="xpy-3">{{ toPercentageFormat(candidate.numberOfVotes / totalVotes) }}  </td>
            <td>
              <button class="btn btn-outline-info">Editar</button>
              <button class="btn btn-outline-danger ml-2">Eliminar</button>
            </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {
  },
  data() {
    return {
      compute: 0.99126,
      candidates: [
        {
          name: 'Pedro Castillo',
          numberOfVotes: 8819183
        },
        {
          name: 'Keiko Fujimori',
          numberOfVotes: 8759331
        }
      ]
    }
  },
  computed: {
    totalVotes() {
      return this.candidates.reduce((a, b) => a.numberOfVotes + b.numberOfVotes);
    }
  },
  methods: {
    toCommaFormat(num) { /// 123,456,789
      return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
    toPercentageFormat(num) { /// 57.890 %
      return `${ (num * 100).toFixed(3) } %`;
    }
  },
}
</script>
