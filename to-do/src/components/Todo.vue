<template>
<div class="abTile" :class="darkTheme?'bg-primary':'bg-gray'">
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
        <div class="tile-subtitle" :class="darkTheme?'text-light':'text-dark'"> {{ todo.description }}</div>
    </div>
    <div class="tile-action">
        <button @click="$emit('toggle', todo)" class="btn btn-link" :class="darkTheme?'text-light':'text-dark'">
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
         darkTheme: {type: Boolean, required: true}
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

    .btn :focus{
        box-shadow: none;
    }
</style>