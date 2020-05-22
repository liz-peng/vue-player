<template>
	<div>
		<SearchBar @searchTermChange="onSearchTermChange"></SearchBar>
	</div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
const API_KEY = 'AIzaSyBUSaxahFCy25CYIrSkopFfEzk0g7rhWZQ';

export default {
	name: 'App',

	components: {
		SearchBar
	},

	methods: {
		onSearchTermChange(newSearch) {
			// axios returns a promise
			axios.get('https://www.googleapis.com/youtube/v3/search', {
				params: {
					key: API_KEY,
					type: 'video', // type of search
					part: 'snippet', // the type of info we want to get back, 'snippet' is small piece of info
					q: newSearch // query
				}
			}).then(response => {
				console.log(response);
			});
		}
	}
};
</script>