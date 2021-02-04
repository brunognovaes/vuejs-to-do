<template>
  <div class="tile flex-centered" :class="{checked: todo.checked}">
     <div class="tile-action">
         <button @click="$emit('remove', todo)" class="btn btn-link">
             <span class="text-error">
               <div class="tile-icon">
                  <i class="icon centered icon-delete"></i>
               </div>
             </span>
         </button>
     </div>
    <div class="tile-content">
        <div class="tile-subtitle"> {{ todo.description }}</div>
    </div>
    <div class="tile-action">
        <button @click="$emit('toggle', todo)" class="btn btn-link">
            <span v-if="todo.checked">Desmarcar</span>
            <span v-else>Concluído</span>
       </button>
    </div>
  </div>
</template>

<script>
export default {
    props: {
         todo: {type: Object, required: true},
    },
}
</script>

<style>
    .checked{
        text-decoration: line-through;
        color: lightgray;
    }
</style>