<template>
  <div class="hello">
    {{title}}
    <div class="row">
      <div class="col-6">
          <form v-on:submit.prevent="onSubmit">
            <input v-model="q" class="form-control" placeholder="most similar">
          </form>
              <div v-for="(key, value) in response">{{value}} : {{key}}</div>
      </div>
    </div>
  </div>
</template>

<script>

    import axios from 'axios';


export default {
  name: 'HelloWorld',
    methods: {
        onSubmit() {
            /*
                move to env dev and prod file
             */
            let url = 'http://35.186.150.121:8000/most_similar?q=' + this.q;
            axios.get(url).then(response => {
                if (response.status == 200) {
                    this.response = response.data;
                }
            })
        }
    },
    data(){
      return{
          title: 'Word2Vec',
          q:'',
          response: []
      }
    },
  props: {
    msg: String
  }
}
</script>
