<script setup lang="ts">

  import {Gender, Popularity, Length, names} from '@/data'

  interface OptionsState {
    gender: Gender
    popularity: Popularity
    length: Length
  }

  const obj: OptionsState = {
    gender: Gender.GIRL,
    popularity: Popularity.UNIQUE,
    length: Length.LONG
  }

  const options = reactive<OptionsState>({
    gender: Gender.GIRL,
    popularity: Popularity.UNIQUE,
    length: Length.LONG
  })

  const computeSelectedNames = () => {
    const filteredNames = names
    .filter(name => name.gender === options.gender)
    .filter(name => name.popularity === options.popularity)
    .filter(name => {
      if (options.length === Length.ALL) {
        return true
      } else {
        return name.length === options.length
      }
    })

    selectedNames.value = filteredNames.map(name => name.name)
  }

  const selectedNames = ref<string[]>([])

  const optionsArray = [
    {
      category: 'gender',
      title: "1) choose a gender",
      buttons: [Gender.BOY, Gender.GIRL, Gender.UNISEX]
    },
    {
      category: 'popularity',
      title: "2) choose the name's popularity",
      buttons: [Popularity.TRENDY, Popularity.UNIQUE]
    },
    {
      category: 'length',
      title: "3) choose the name's length",
      buttons: [Length.LONG, Length.SHORT, Length.ALL]
    },
  ]

</script>

<template>
  <div class="container">
    <h1>baby name generator</h1>
    <p>choose your options and click the "find names" button below</p>
    <div class="options-container">
      <Option
        v-for="option in optionsArray" 
        :key="option.title" 
        :option="option" 
        :options="options" />

      <button class="primary" @click="computeSelectedNames">find names</button>
    </div>
    <div class="cards-container">
      <CardName v-for="name in selectedNames" :key="name" :name="name" />
    </div>
  </div>
</template>

<style>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

.container h1 {
  font-size: 3rem;
}

.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 4rem auto 0 auto;
  position: relative;
}

.option-container {
  margin: 0 0 2rem 0;
}

.primary {
  background-color: rgb(249, 87, 89);
  color: #fff;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin: 1rem 0 0 0;
  cursor: pointer;
}

.cards-container {
  display: flex;
  margin: 3rem 0 0 0;
  flex-wrap: wrap;
}
</style>