<template>
	<div>
		<SearchBar @searchTermChange="onSearchTermChange"></SearchBar>
		<VideoList :videos="videosList"></VideoList>
	</div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
const API_KEY = 'AIzaSyBUSaxahFCy25CYIrSkopFfEzk0g7rhWZQ';

export default {
	name: 'App',

	components: {
		SearchBar,
		VideoList
	},

	data() {
		return {
			videosList: []
		};
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
				this.videosList = response.data.items;
			});
		}
	}
};
</script>