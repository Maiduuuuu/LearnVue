<template>
  <div class="card">
      <header class="card-header has-background-primary">
          <p class="card-header-title">
              <router-link :to="'/covid/' + country.Slug" >{{country.Country}}</router-link>
          </p>
      </header>
      <div class="card-content has-background-grey">
          <div class="content">
              <table class="table is-hoverable has-background-grey">
                  <tbody>
                        <tr>
                            <th>Total Confirmed:</th>
                            <td>{{country.TotalConfirmed}}</td>
                        </tr>
                        <tr>
                            <th>Total Deaths:</th>
                            <td>{{country.TotalDeaths}}</td>
                        </tr>
                        <tr>
                          <th>New Confirmed:</th>
                          <td>{{country.NewConfirmed}}</td>
                        </tr>
                        <tr>
                            <th>New Deaths:</th>
                            <td>{{country.NewDeaths}}</td>
                        </tr>
                  </tbody>
              </table>
          </div>
      </div>
  </div>
</template>

<script>
export default {
    props: ['country']
}
</script>

<style>

</style>