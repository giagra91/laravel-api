<template>
    <div class="col-4">
        <div class="card p-3 my-2">
            <img :src="post.image_url" class="card-img-top img-fluid" :alt="`Image of ` + post.title">
            <div class="card-body">
                <h5 class="card-title">{{ post.title }}</h5>
                <p class="card-text">{{ post.content.substring(0, 100) + "..." }}</p>
            </div>
            <div class="card-body">
                <p>Created: {{ post.created_at.substring(0, 10) }}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Post",
    props:["post"]
}
</script>

<style>

</style>