<template>
    <div style="border:1px solid black; margin: 10px;">
        <h3>Child Component #{{ id }}</h3>
        <div>
            <p>{{ bookmarked ? 'Bookmarked!' : 'Not bookmarked!' }}</p>
        </div>
        <div>
            <button @click="toggleBookmark">Toggle Bookmark</button>
        </div>
        <p></p>
    </div>
</template>

<script>
export default {
    name: 'BookMarkItem',
    props: {
        id: {
            required: true
        },
        bookmarked: {
            required: true,
            type: Boolean
        }
    },
    methods: {
        toggleBookmark () {
            this.$emit('bookmark-toggle', this.id);
        }
    }
};
</script>