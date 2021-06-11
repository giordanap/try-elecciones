<template>
  <div class="home container">
    <table class="table table-hover">
      <thead>
        <tr>
          <th scope="col">Candidato</th>
          <th scope="col">Cantidad de Votos (al {{compute * 100}}%)</th>
          <th scope="col">% Votos</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="candidate in candidates" :key="candidate.name">
            <th scope="row">{{ candidate.name }}</th>
            <!-- <td>{{ candidate.numberOfVotes.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",") }}</td> -->
            <td>{{ toCommaFormat(candidate.numberOfVotes) }}</td>
            <td>{{ toPercentageFormat(candidate.numberOfVotes / totalVotes) }}</td>
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
    toCommaFormat(num) {
      return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
    toPercentageFormat(num) {
      return `${ (num * 100).toFixed(3) } %`;
    }
  },
}
</script>
