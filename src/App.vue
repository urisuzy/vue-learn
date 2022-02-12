<template>
  <div id="app" style="display: flex; justify-content: center">
    <table border="1">
      <thead>
        <th>#</th>
        <th>Name</th>
        <th>Kelas</th>
        <th>Pic</th>
      </thead>
      <tbody>
        <tr v-for="(item, index) in orangs" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ item.nama }}</td>
          <td>{{ item.kelas }}</td>
          <td><img :src="item.foto" alt="" width="150px" /></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  data: () => ({
    orangs: []
  }),
  methods: {
    getUser(id) {
      axios
        .post(
          'https://siama.sekolahan.id/api/v2/16/profilsiswa?idsiswa=' + id,
          {},
          {
            headers: {
              Authorization:
                'Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJzaWFtYS5zZWtvbGFoYW4uaWQiLCJhdWQiOiIxMC4xMzAuMTMyLjI1MCIsImlhdCI6MTY0NDU4Mzc2MiwibmJmIjoxNjQ0NTgzNzcyLCJkYXRhIjp7ImlkIjpudWxsfX0.xIMMYSkrgPZPln2GJ2xpevg6XkQJ2xw_9auOLmwo1So'
            }
          }
        )
        .then((res) => {
          console.log(res)
          if (res.data.responseData.results.nis != null) this.orangs.push(res.data.responseData.results)
        })
        .catch((err) => {
          console.log(err)
        })
    },
    range(start, end) {
      let ids = []
      for (let i = start; i <= end; i++) {
        ids.push(i)
      }
      return ids
    }
  },
  mounted() {
    console.log('anjay')
    console.log(axios)
    const ids = this.range(4500, 5500)
    // this.getUser('6486')
    for (let i in ids) {
      this.getUser(ids[i])
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
