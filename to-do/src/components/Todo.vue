<template>
<div class="abTile" :class="'bg-'+tilesTheme">
  <div class="tile flex-centered" >
     <div class="tile-action">
         <button @click="$emit('remove', todo)" class="btn btn-link">
             <span class="text-error">
               <div class="tile-icon">
                  <i class="icon centered icon-delete"></i>
               </div>
             </span>
         </button>
     </div>
    <div class="tile-content" :class="{checked: todo.checked}" >
        <div class="tile-subtitle" :class="'text-'+ textTheme"> {{ todo.description }}</div>
    </div>
    <div class="tile-action">
        <button @click="$emit('toggle', todo)" class="btn btn-link" :class="'text-'+ textTheme">
            <span v-if="todo.checked">Desmarcar</span>
            <span v-else>Concluído</span>
       </button>
    </div>
  </div>
</div>
</template>

<script>
export default {
    props: {
         todo: {type: Object, required: true},
         textTheme: {type: String, required: true},
         tilesTheme: {type: String, required: true}
    },
}
</script>

<style>
    .checked{
        opacity: 0.5;
    }

    .abTile{
        border-radius: 10px;
    }
</style>