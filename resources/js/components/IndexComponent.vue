// IndexComponent.vue

<template>
  <div>
      <h1>services</h1>
        <div class="row">
          <div class="col-md-10"></div>
          <div class="col-md-2">
            <router-link :to="{ name: 'create' }" class="btn btn-primary">Create service</router-link>
          </div>
        </div><br />

        <table class="table table-hover">
            <thead>
            <tr>
                <th>id</th>
                <th>userid</th>
                <th>name</th>
                <th>descriptions</th>
                <th>minimumprice</th>
                <th>status</th>
                <th>actions</th>
            </tr>
            </thead>
            <tbody>
                <tr v-for="service in services" :key="service.id">
                    <td>{{ service.id }}</td>
                    <td>{{ service.userid }}</td>
                    <td>{{ service.name }}</td>
                    <td>{{ service.descriptions }}</td>
                    <td>{{ service.minimumprice }}</td>
                    <td>{{ service.status }}</td>
                    <td><router-link :to="{name: 'edit', params: { id: service.id }}" class="btn btn-primary">Edit</router-link></td>
                    <td><button class="btn btn-danger" @click.prevent="deleteservice(service.id)">Delete</button></td>
                </tr>
            </tbody>
        </table>
  </div>
</template>

<script>
  export default {
      data() {
        return {
          services: []
        }
      },
      created() {
      let uri = 'http://localhost/delete_jasa/public/api/getAll';
      this.axios.get(uri).then(response => {
        this.services = response.data.delete;
      });
    },
    methods: {
      deleteservice(id)
      {
        let uri = `http://localhost/delete_jasa/public/api/delete/${id}`;
        this.axios.delete(uri).then(response => {
          this.services.splice(this.services.indexOf(id), 1);
        });
      },
    },
  }
</script>