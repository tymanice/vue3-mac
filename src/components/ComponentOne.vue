<template>
    <div class="col-3 form-control" >
      <label for="date">Agency</label>
      <InputText type="text" id="agency" placeholder="Agency" @input='handleChange' />
    </div>
</template>

<script>
import InputText from 'primevue/inputtext'

export default {
    emits: ['agency-field'],
    components: {
        InputText
    },
    methods: {
            handleChange (event) {
              this.$emit("customChange", event.target.value.toUpperCase())
          },
    }
}
</script>