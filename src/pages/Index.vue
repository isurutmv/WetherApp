<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
      <q-input v-model="search" placeholder="Search" dark borderless>
        <template v-slot:before>
          <q-icon name="my_location" />
        </template>

        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
    </div>
    <template v-if="wetherData">
      <div class="col text-white text-center">
        <div class="text-h4 text-weight-light">
          Gampaha
        </div>
        <div class="text-h6 text-weight-light">
          Rain
        </div>
        <div class="text-h1 text-weight-thin q-my-lg relative-position">
          <span>23</span>
          <span class="text-h4 relative-position degree">&deg;</span>
        </div>
      </div>

      <div class="col text-center">
        <img src="" alt="Bill" />
      </div>
    </template>
    <template v-else>
      <div class="col column text-center text-white">
        <div class="col text-h2 text-weight-thin">Find <br />Weather</div>
        <q-btn class="col" flat>
          <q-icon left size="3em" name="my_location" />
          <div>Find My Location</div>
        </q-btn>
      </div>
    </template>

    <div class="skyline"></div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      search: "",
      wetherData: null
    };
  }
};
</script>
<style lang="sass">
.q-page
  background: linear-gradient(to top, #74ebd5, #acb6e5)

  .degree
      top: -45px

  .skyline
    flex: 0 0 100px
    background: url(../assets/sky.png)
    background-size: contain
    background-position: center bottom
</style>
