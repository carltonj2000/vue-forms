<template>
  <div>
    <h1>Create an event</h1>
    <form @submit.prevent="sendForm">
      <BaseSelect
        v-model="event.category"
        label="Select a category"
        :options="categories"
      />

      <h3>Name & describe your event</h3>

      <BaseInput v-model="event.title" label="Title" type="text" />

      <BaseInput v-model="event.description" label="Description" type="text" />

      <h3>Where is your event?</h3>

      <BaseInput v-model="event.location" label="Location" type="text" />

      <h3>Are pets allowed?</h3>
      <BaseRadioGroup v-model="event.pets" name="pets" :options="petOptions" />
      <pre>{{ JSON.stringify(event) }}</pre>
      <h3>Extras</h3>
      <div>
        <BaseCheckBox v-model="event.extras.catering" label="Catering" />
      </div>
      <div>
        <BaseCheckBox v-model="event.extras.music" label="Live music" />
      </div>

      <button class="button -fill-gradient" type="submit">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      categories: [
        'sustainability',
        'nature',
        'animal welfare',
        'housing',
        'education',
        'food',
        'community'
      ],
      petOptions: [
        { label: 'Yes', value: 1 },
        { label: 'No', value: 0 }
      ],
      event: {
        category: '',
        title: '',
        description: '',
        location: '',
        pets: 1,
        extras: {
          catering: false,
          music: false
        }
      }
    }
  },
  methods: {
    sendForm() {
      console.log(this.event)
      axios
        .post(
          'http://my-json-server.typicode.com/carltonj2000/vue-forms/events',
          this.event
        )
        .then(resp => console.log({ resp }))
        .catch(e => console.log({ e }))
    }
  }
}
</script>
