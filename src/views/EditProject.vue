<template>
  <form @submit.prevent="handleEdit">
    <label for="title">Title:</label>
    <input
      name="details"
      type="text"
      id="title"
      required
      v-model="title"
    >
    <label for="details">Details:</label>
    <textarea
      name="details"
      id="details"
      cols="30"
      rows="10"
      required
      v-model="details"
    ></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
    props: [ 'id'], 
    data() {
        return {
            title: '',
            details: '',
            uriid: 'http://localhost:3000/projects/' + this.id,
        }
    },
    mounted() {
        fetch(this.uriid)
        .then( res => res.json())
        .then(data => {
            this.title = data.title,
            this.details = data.details
        })
    },
    methods: {
        handleEdit() {
            fetch(this.uriid, {
                method: 'PATCH',
                headers: { 'Content-type' : 'application/json'},
                body: JSON.stringify({
                    title: this.title,
                    details: this.details
                 })
            })
            .then(() => {
                this.$router.push('/')
            })
            .catch(err => console.log(err))
        }
    }
}
</script>

<style lang="scss" scoped>
form {
    background: white;
    padding: 20px;
    border-radius: 10px;
    button { 
        display: block;
        margin: 20px auto 0;
        background: #00ce89;
        color: white;
        padding: 10px;
        border: 0;
        border-radius: 6px;
        font-size: 16px;
    }
  }
  label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0
  }
  input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
  }
 
</style>