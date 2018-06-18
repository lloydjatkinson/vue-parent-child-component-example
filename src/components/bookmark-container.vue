<template>
    <div style="border:1px solid black; margin: 10px;">
        <h1>Parent Component</h1>
        <button @click="toggleAll">Toggle All</button>
        <button @click="callApi">Mock API Call</button>
        <bookmark-item
            v-for="(item, index) in items" :key="index"
            v-on:bookmark-toggle="toggleBookmark"
            :id="item.id"
            :bookmarked="item.bookmarked" />
    </div>
</template>

<script>
import BookmarkItem from './bookmark-item';

export default {
    name: 'BookmarkContainer',
    components: {
        BookmarkItem
    },
    data () {
        return {
            items: []
        }
    },
    created () {
        // Mock API call here. In this case it's returned data but we only need for example one of the properties.
        const mockApiResponse = [
            { id: 1, author: 'Somebody', publishedYear: 2000 },
            { id: 2, author: 'Someone', publishedYear: 1994 },
            { id: 3, author: 'Something', publishedYear: 1999 },
            { id: 4, author: 'Somewhere', publishedYear: 2001 },
        ];

        this.items = mockApiResponse.map(item => ({
            id: item.id,
            bookmarked: false
        }));
    },
    methods: {
        toggleBookmark (itemId) {
            const foundItem = this.items.find(i => i.id === itemId);
            foundItem.bookmarked = !foundItem.bookmarked;
        },
        toggleAll () {
            for (const item of this.items) {
                item.bookmarked = !item.bookmarked;
            }
        },
        callApi () {
            // Mock API call here. This time we create a new array and only post relevant data.
            // Note how the local component state does not have to match 1:1 with any data from a GET or to a POST/PUT.
            const mockApiCall = this.items.map(item => ({
                id: item.id,
                bookmarked: item.bookmarked,
                favouriteNumber: Math.random(),
            }));

            console.log(mockApiCall);
        }
    }
}
</script>