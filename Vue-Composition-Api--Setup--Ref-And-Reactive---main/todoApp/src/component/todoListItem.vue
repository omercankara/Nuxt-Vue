        <template>
                        <section class="mt-4">
                                 <div class=" flex justify-between items-center even:bg-gray-600 px-2 p-1">
                                                  <label :for="`todo_${todo.id}_completed`">
                                                        <input v-model="todo.completed" type="checkbox" id="completed" class="mr-2">
                                                           <span class="text-lg">{{todo.title}}</span>
                                                  </label>
                                                <button  @click="deleteItem"  class="bg-indigo-500 py-1 p-2 rounded-md active:bg-indigo-800">Sil</button>
                                 </div> 
                               
                         </section>
        </template>



<script>
export default {
        props:{
                todo:Object,
        },

        setup(props, {emit} ){
              const deleteItem = (()=>{
                        emit("delete-event",props.todo)
              })

              return {deleteItem}
        }
}
</script>
