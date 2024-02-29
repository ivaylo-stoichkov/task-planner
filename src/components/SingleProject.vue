<template>
  <div
    class="project"
    :class="{ 'complete--border' : isComplete() }"
  >
    <div class="actions">
      <h3 @click="open = !open">
        {{project.id}}. {{project.title}}
      </h3>
      <div class="icons">
        <router-link :to="{ name: 'Edit Project', params: { id: project.id} }">
          <span class="material-icons">edit</span>
        </router-link>
        <span
          class="material-icons"
          @click="deleteItem"
        >delete</span>
        <span
          class="material-icons"
          @click="toggleComplete"
          :class="{ 'complete--tick' : isComplete() }"
        >done</span>
      </div>
    </div>
    <div
      v-if="open"
      class="details"
    >
      <p>{{project.details}}</p>
    </div>
  </div>
</template>

<script>
export default {
    props: ['project'],
    data() {
        return {
            open : false,
            uriid: 'http://localhost:3000/projects/' + this.project.id
        }
    },
    methods: {
        deleteItem() {
            fetch(this.uriid, { method: 'DELETE' } )
            .then(()=> this.$emit('delete', this.project.id ))
            .catch((err)=> console.log(err))
        },
        toggleComplete() {
            fetch(this.uriid, {
                method: 'PATCH',
                headers: { 'Content-type' : 'application/json'},
                body: JSON.stringify({complete : !this.project.complete })
                } )
                .then(()=> this.$emit('complete', this.project.id ))
                .catch((err)=> console.log(err))
        },
        isComplete() {
            return this.project.complete === true
        }
    }
}
</script>

<style lang="scss" scopped>
.project {
    margin: 20px auto;
    background-color: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
    border-left: 6px solid #e90074;
    h3{
        cursor: pointer;
    }
    .actions {
        display: flex;
        align-items: center;
        justify-content: space-between;
        .material-icons{
            font-size: 24px;
            margin-left: 10px;
            color: #bbb;
            cursor: pointer;
            &:hover {
                color: #777
            }
        }
    }
}
.complete{
    &--border {
        border-left: 6px solid #00ce89;
    }
    &--tick {
        color: #00ce89  !important;
        font-weight: bold;
    }
}
</style>