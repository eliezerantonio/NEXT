<template>
    <div id="job-new">
        <div class="container mt-2">
            <div class="row">
                <div class="col-12">
                    <h3>Novo Projeto</h3>
                    <hr>
                    <b-alert variant="danger" v-if="errorMessage" show>{{errorMessage}}</b-alert>
                    <JobForm @submit="onSubmit"></JobForm>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import JobForm from './forms/JobForm'
import { apiProtected } from '../services/apiService'
export default {
    components: {
        JobForm
    },
    data: () => ({
        errorMessage: ""
    }),
    methods: {
        async onSubmit(data) {
            try {
                const response = await apiProtected.post('job/', data)
                const job = response.data.data
                this.$router.push(`/jobs/${job.id}/show`)
            } catch (error) {
                console.error(error)
                this.errorMessage = "Erro ao tentar salvar os dados."
            }
        }
    },
}
</script>

<style>

</style>