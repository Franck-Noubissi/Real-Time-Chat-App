<template>
    <div class="bg-gray-500 mt-2 rounded-full text-white p-2 w-max" >
        {{message.user.name}}: {{message.message}}
    </div>
</template>

<script>
export default {
    props: ['message']

}
</script>