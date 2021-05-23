<template>
  <div>
    <p v-if="$fetchState.pending">Loading...</p>
    <p> {{ $fetchState.pending }} </p>
    <table>
      <thead>
        <tr>
          <td>-</td>
          <td>Tag</td>
          <td>Name</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in res.items" :key="user.tag">
          <td><img :src="user.league.iconUrls.tiny" alt=""></td>
          <td>{{ user.tag }}</td>
          <td>{{ user.name }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

export default {
  data() {
    return { 
      res: [],
    };
  },
  async fetch() {
    this.res = await this.$axios
    .get(
      '/api',
      {
        headers: {
          'Authorization': process.env.KEY
        }
      }
    )
    .then(res => res.data)

  },
}
</script>

<style>

</style>