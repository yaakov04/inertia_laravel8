<template>
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Notas
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                
                    <div class="md:grid md:grid-cols-3 md:gap-6">
                        <div class="md:col-span-1">
                            <div class="px-4 sm:px0">
                                <h3 class="text-lg text-gray-900">Editar nota</h3>
                                <p class="text-sm text-gray-600">Edita esta nota</p>
                            </div>
                        </div>
                        <div class="md:col-span-2 mt-5 md:mt-0">
                            <div class="shadow bg-white md:rounded-md p-4">
                              <form @submit.prevent="submit">
                                  <label  class="block font-medium text-sm text-gray-700">
                                      Resumen
                                  </label>
                                  <textarea class="form-input w-full rounded-md shadow"
                                  v-model="form.excerpt">
                                  </textarea>
                                  <label  class="block font-medium text-sm text-gray-700">
                                      Contenid
                                  </label>
                                  <textarea class="form-input w-full rounded-md shadow"
                                  v-model="form.content"
                                  rows='8'
                                  >
                                  </textarea>
                                  <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md">Editar</button>
                                  <a href="#" @click.prevent="destroy" class="bg-red-500 hover:bg-blue-700 text-white font-bold py-2 px-4 ml-2 rounded-md">Eliminar</a>
                              </form>
                               <hr class="my-6">

                               <Link  :href="route('notes.index')">
                                    Volver
                               </Link>
                            </div>
                        </div>
                    </div>
                
            </div>
        </div>
    </app-layout>
</template>

<script>
    import { defineComponent } from 'vue'
    import AppLayout from '@/Layouts/AppLayout.vue'
    import Welcome from '@/Jetstream/Welcome.vue'
    import { Head, Link } from '@inertiajs/inertia-vue3'

    export default defineComponent({
        components: {
            AppLayout,
            Head,
        Link,
        },
        props: {
            note: Object,
        },  
        data () {
            return {
                form: {
                    excerpt: this.note.excerpt,
                    content: this.note.content,
                }
            }
        },
        methods:{
            submit(){
                this.$inertia.put(this.route('notes.update', this.note.id), this.form)
            },
            destroy(){
                if (confirm('¿Desea eliminar?')) {
                this.$inertia.delete(this.route('notes.destroy', this.note.id))
                }
            }
        }
    })
</script>