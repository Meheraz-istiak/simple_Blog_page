<script setup>
import axios from 'axios'
import {ref} from 'vue'
import PostId from './PostId.vue'

const PostData = ref({})
const PostByIddetails = ref({})

PostItems()
async function PostItems(){
     let url='https://basic-blog.teamrabbil.com/api/post-newest'
     let res = await axios.get(url)
     console.log(res.data)
     if(res.status == 200){
        PostData.value=res.data

     }else{
        alert('Data not found')
     }
}
PostById()
async function PostById(id){
    let url='https://basic-blog.teamrabbil.com/api/post-details/'+id
     let res = await axios.get(url)
     console.log('post',res.data)
     if(res.status == 200){
        PostByIddetails.value=res.data

     }else{
        alert('Data not found')
     }
}

</script>
<template>
    <div class=" flex-row space-x-4 flex-container pt-6 px-2">

        <div v-for="item in PostData" :key="item.id" class="pt-3">

            <div  class=" pt-6 max-w-sm bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700">
                <a href="#">
                    <img class="rounded-t-lg" :src="item.img" alt="" />
                </a>
                <div class="p-5">
                    <a href="#">
                        <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
                            {{ item.title }}</h5>
                    </a>
                    <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">{{ item.short }}</p>
                    <a href="#"
                       @click="PostById(item.id)"

                        class="inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
                        Read more
                        <svg class="w-3.5 h-3.5 ml-2" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none"
                            viewBox="0 0 14 10">
                            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M1 5h12m0 0L9 1m4 4L9 9" />
                        </svg>
                    </a>
                </div>
            </div>

        </div>
    </div>
    <div>
        <PostId :PostByIddetails="PostByIddetails" />
    </div>
</template>



<style  scoped>
.flex-container {
  display: flex;
  flex-wrap: wrap;
}

</style>